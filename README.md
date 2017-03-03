# Materiale di studio per il corso di Tecniche di programmazione

Tutte le informazioni sul corso sono al link <http://bit.ly/tecn-progr>

## Software necessario

Nota: per scelta didattica, tutto il software indicato è gratuito e quasi sempre open source.

1. Java Development Kit (JDK), versione 8: <http://www.oracle.com/technetwork/java/javase/downloads/index.html> (selezionare JDK e poi la versione del `Java SE Development Kit 8u121` corrispondente al vostro sistema operativo)
* Eclipse, versione Neon: <http://www.eclipse.org/downloads/>. Si suggerisce di selezionare `Get Eclipse Neon` e scegliere di installare `Eclipse IDE for Java Developers` (oppure `Eclipse IDE for Java EE Developers` se si intende sviluppare anche applicazioni Web con Java -- non necessario in questo corso).
* Plugin `e(fx)clipse` di Eclipse. Il plugin si installa dal Marketplace di Eclipse (menu Help): ricercare `javafx` e selezionare `e(fx)clipse 2.4.0`
* Editor di interfacce utente Scene Builder, scaricabile da <http://gluonhq.com/open-source/scene-builder/>
* Un database server MySQL, a scelta tra:
  * Oracle `MySQL Community Server` <http://dev.mysql.com/downloads/mysql/>, versione 5.7+
  * Il server `MariaDB` <https://downloads.mariadb.org/>, versione 10.1+ (nota: scegliere di *non* installare `HeidiSQL` in quanto è una versione vecchia)
  * Il pacchetto `XAMPP` (che contiene un server mySQL integrato) <https://www.apachefriends.org/download.html>, versione 5.6.30
* Un front-end per MySQL, a scelta tra:
  * `HeidiSQL` <http://www.heidisql.com/download.php>, leggero, veloce ma solo per Windows
  * `MySQL Workbench` <http://dev.mysql.com/downloads/workbench/>, più completo, con progettazione grafica delle tabelle, ma più complesso da usare e molto più lento, disponibile per tutti i sistemi operativi
  * `Sequel Pro` <http://www.sequelpro.com/>, per Mac OS X
* La libreria `MySQL Connector/J` <http://dev.mysql.com/downloads/connector/j/>
* La libreria `jGraphT` <http://jgrapht.org/> (comprende anche i JavaDoc)

## Download opzionali

* JavaDoc relativo alla JDK ed a JavaFX, utile per avere autocompletamento e documentazione in Eclipse quando non si è connessi ad Internet: <http://docs.oracle.com/javase/8/docs/> e selezionare (nella colonna di sinistra) il link "JDK 8 Documentation", poi scaricare `Java SE Development Kit 8u121 Documentation` e `JavaFX API Documentation`
* Libreria `c3p0` per implementare il *connection pooling* <http://www.mchange.com/projects/c3p0/>
* Libreria `SimpleLatLng` per i calcoli con latitudine e longitudine <https://github.com/JavadocMD/simplelatlng>

## Link di approfondimento

* API di JavaFX: consultazione on-line <http://docs.oracle.com/javafx/2/api/index.html>
* Diagrammi delle classi della libreria JavaFX <http://www.falkhausen.de/JavaFX/index.html>
* Esempi interattivi di JavaFX sono contenuti nel file "JDK 8 Demos and Samples" <http://www.oracle.com/technetwork/java/javase/downloads/index.html>
* Documentazione e tutorial JavaFX <http://docs.oracle.com/javase/8/javase-clienttechnologies.htm>

