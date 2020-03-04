# Materiale di studio per il corso di Tecniche di programmazione

Tutte le informazioni sul corso sono al link <http://bit.ly/tecn-progr>

# Tool

## Software necessario

Nota: per scelta didattica, tutto il software indicato è gratuito e quasi sempre open source.

* Java Development Kit (JDK), versione 11 LTS (per Mac OS X, consigliamo di installare la versione JDK 13)
* Eclipse
* Editor di interfacce utente Scene Builder
* Un database server MySQL
* Un front-end per MySQL
* La libreria `MySQL Connector/J` oppure `MariaDB Connector/J`
* La libreria `jGraphT`

Si veda il **documento con le istruzioni di installazione per [Windows](software-install-windows.pdf) e per [macOS X](software-install-macos.pdf)**

## Download opzionali

* JavaDoc relativo alla JDK ed a JavaFX, utile per avere l'auto-completamento e la documentazione disponibili in Eclipse quando non si è connessi ad Internet: <http://docs.oracle.com/javase/8/docs/> e selezionare (nella colonna di sinistra) il link "JDK 8 Documentation", poi scaricare `Java SE Development Kit 8u121 Documentation` e `JavaFX API Documentation`
* Libreria `c3p0` per implementare il *connection pooling* <http://www.mchange.com/projects/c3p0/>
* Libreria `SimpleLatLng` per i calcoli con latitudine e longitudine <https://github.com/JavadocMD/simplelatlng>

# Documentazione

## Lucidi del corso
* Vai alla cartella contenente i [lucidi del corso](https://github.com/TdP-2020/materiale/tree/master/slides)

## FAQ (domande frequenti e risposte a problemi ricorrenti)

*  [Come risolvere il problema `The server time zone value 'ora solare Europa occidentale' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.`](./faq/timezone.md)
* [Come risolvere un problema in cui le query che filtrano su una colonna di tipo `DATE` restituiscono il giorno *precedente* a quello voluto](./faq/conversione-date.md)

## Link di approfondimento

* API di JavaFX: consultazione on-line <http://docs.oracle.com/javafx/2/api/index.html>
* Diagrammi delle classi della libreria JavaFX <http://www.falkhausen.de/JavaFX/index.html>
* Esempi interattivi di JavaFX sono contenuti nel file "JDK 8 Demos and Samples" <http://www.oracle.com/technetwork/java/javase/downloads/index.html>
* Documentazione e tutorial JavaFX <http://docs.oracle.com/javase/8/javase-clienttechnologies.htm>
