# Analisi di un problema di conversione date 

## Premessa

In alcune condizioni, la selezione di un campo di tipo DATE potrebbe dare il risultato errato (ad esempio, selezionando una data, viene invece restituito il giorno precedente).
Questo è dovuto ad una _correzione del fuso orario_ compiuta automaticamente (e talvolta a sproposito) dal driver MySQL di Oracle.

## Descrizione del problema

### Sintomo

Ipotizziamo di avere una tabella che contiene delle colonne di tipo `DATE`.

| id (`INT`) | giorno (`DATE`) | valore (`INT`) |
|------------|-----------------|----------------|
| 1 | 2019-05-16 | 100 |
| 2 | 2019-05-17 | 200 |
| 3 | 2019-05-18 | 300 |
| 4 | 2019-05-19 | 400 |
| 5 | 2019-05-20 | 500 |
| 6 | 2019-05-21 | 600 |

Immaginiamo di volere selezionare le righe corrispondenti ad un range di date.

```sql
SELECT *
FROM giorni
WHERE giorni.giorno >= ?
AND giorni.giorno <= ?
```

Ad esempio vogliamo selezionare le righe comprese tra il 17/05/2019 ed il 19/05/2019:

```java
LocalDate data1 = LocalDate.of(2019, Month.MAY, 17) ;
LocalDate data2 = LocalDate.of(2019, Month.MAY, 19) ;
...
PreparedStatement st = conn.prepareStatement(sql) ; // v. sopra

st.setDate(1, Date.valueOf(data1)) ; // conversione java.time.LocalDate -> java.sql.Date
st.setDate(2, Date.valueOf(data2)) ;

ResultSet res = st.executeQuery() ;
```

Analizzando il ResultSet ... sorpresa! conterrà i giorni 16, 17 e 18 anziché 17, 18, 19.


### Cause

Si tratta purtroppo di un malfunziomanento noto da tempo. Vedi: https://bugs.mysql.com/bug.php?id=71084 (è un bug del 2013). Ad un certo punto dice:

```
Another issue [...] the methods get/setDate() without Calendar argument not only perform the time zone correction but also truncate time info, so as in your example:
   - '2013-11-20' >(tz correction)> '2013-11-19 23:00:00.0' >(truncate)> '2013-11-19' > stored in server.
   - get from server '2013-11-19' >(tz correction)> '2013-11-19 1:00:00.0' >(truncate)> '2013-11-19'
```

Il problema è avviene la seguente sequenza di eventi:

1. LocalDate `17/05/2019` viene convertita in java.sql.Date `17/05/2019` (fin qui ok)
1. il driver JDBC (SQL Connector/J di Oracle) riceve java.sql.Date `'17/05/2019'` e lo interpreta come `'17/05/2019 00:00'`
1. nel passare il valore al database il driver JDBC "_corregge_" il fuso orario, convertendolo in UTC (ossia sottraendo 1 o 2 ore, a seconda dell'ora legale). **Non dovrebbe farlo, visto che il campo è DATE e non DATETIME**.
1. al database arriva `'16/05/2019 22:00'` (UTC)
1. il database, giustamente, per un campo `DATE`, elimina (troncandolo) l'orario: arriviamo a `'16/05/2019'`

Si può verificare sperimentalmente, attivando il log delle Query di MariaDB (vedi https://mariadb.com/kb/en/library/general-query-log/ per attivarlo), che il database esegue proprio:

```sql
SELECT * FROM giorni WHERE giorni.giorno>='2019-05-16' AND giorni.giorno<='2019-05-18'
```
(da notare che le date sono sbagliate: va dal 16 al 18 anziché dal 17 al 19)

## Soluzioni possibili

### Passare le date come stringa (brutto, sconsigliato)

Una soluzione possibile è quella di evitare che il driver JDBC interpreti la data, e quindi passarla direttamente come stringa, sfruttando il fatto che il metodo `toString` di `LocalDate` fornisce già il formato `yyyy-mm-dd` che è quello richiesto da MySQL.

```java
st.setString(1, data1.toString()) ;
st.setString(2, data2.toString()) ;
```

La soluzione non è particolarmente elegante, in quanto si lavora con stringhe (avendo quindi meno controlli di coerenza) anziché con date. Ma in questo modo il driver JDBC "non sa" che la stringa passata corrisponde in realtà ad una data, e pertanto non attiverà la malefica procedura di correzione del fuso orario.

### Utilizzare il driver JDBC di MariaDB anziché quello di Oracle (soluzione suggerita)

Una seconda soluzione possibile è utilizzare un driver JDBC alternativo (ossia evitare il Connector/J di Oracle).

MariaDB fornisce un proprio driver JDBC (ovviamente compatibile), che si può installare come segue:
- visitare  [https://mariadb.com/kb/en/library/about-mariadb-connector-j/](https://mariadb.com/kb/en/library/about-mariadb-connector-j/)
- selezionare "Download MariaDB Connector/J"
- nella pagina successiva selezionare "Java 8 connector" e poi Download
- si ottiene il file `mariadb-java-client-2.4.1.jar`
- a questo punto è sufficiente utilizzare `mariadb-java-client-2.4.1.jar` al posto del (maledetto) `mysql-connector-java-8.0.15.jar` nei nostri progetti Eclipse (ricordare di cancellarlo dal Build Path).

La stringa di connessione non varia, in quanto il MariaDB connector riconosce il prefisso "`jdbc:mysql://`". Anzi, si può anche togliere il parametro `?serverTimezone=UTC` nella stringa di connessione, in quanto il fuso orario viene impostato correttamente già per default.

