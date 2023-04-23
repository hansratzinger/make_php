# Debuging mit XDebug in Visual Studio Code (VSC) und Laragon

### Update 23.04.2023 HR

Wenn während des Debuggings in VSC zugleich PHPMySqlAdmin geöffnet war trat mehrmals ein schwerer Fehler in PHPMySqlAdmin auf (webmozzart). Ich habe daher auf meinem RasperryPi4 innerhalb einer auf [DietPi](https://dietpi.com/#features) laufenden Dockerumgebung den mySQLServer installiert und frage diesen mittels [DBeaver](https://dbeaver.io/) auf dem PC die Datenbank ab. [mehr Info](https://hansratzinger.github.io/smartmeter-docker/)
-------------------------------------------------------------------------

Ich programmiere seit 7 Jahren in PHP als Autodidakt. Nach langem Suchen und vielen Irrwegen habe ich endlich die richtige Methode gefunden um die wunderbaren Vorzüge von **XDebug und Visual Studio Code** zu nutzen. Da es zu diesem Thema eine Vielzahl von irreführenden Infos im Web gibt, stelle ich hier den Weg vor, der bei mir funktioniert.

### meine Programmierumgebung

- Win 10
- Laragon WAMP Server (Apache, PHPMySqlAdmin)
- Visual Studio Code
- XDebug

### Setup

- In VSC die Extension *PHP Debug* installieren
- phpinfo.php Datei erstellen:

    ```
    <?php
    phpinfo();
    exit;
    ```

- phpinfo.php in localhost ausführen, Ausgabe markieren und kopieren

- [Installation Wizard](https://xdebug.org/wizard) aufrufen und kopierte Ausgabe von phpinfo in das Eingabefeld des Wizards einfügen und absenden.

- Die dann angezeigten Instruktionen ausführen. Im Punkt 2 sollte es heissen:<br>
Move the downloaded file to **C:\laragon\bin\php\die_jeweilige_Version\ext** and rename it to php_xdebug.dll<br>
(Falls ein anderer Web-Server verwendet wird, ist der Pfad entsprechend zu ändern)

- Wichtig! Damit XDebug in VSC funktioniert ist der Punkt 3 folgendermaßen zu ergänzen:<br>
*Update C:\laragon\bin\php\die_jeweilige_Version\php.ini and add the line:*
    ```
    xdebug.mode = debug 
    xdebug.start_with_request=yes  
    xdebug.idekey = VSCODE
    xdebug.log="C:\laragon\tmp\xdebug.log"
    xdebug.cli_color = 1

    zend_extension = xdebug
    ```

- den Webserver auf localhost neu starten

- In VSC auf Debugging klicken (Dreieck mit Käfer)

- auf Zahnrad klicken (launch.json öffnen), folgenden JSON Code einfügen und die Datei sichern:

```
{
    "version": "0.2.0",
    "configurations": [

        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003
        }
    ]
}
```

- die zu debuggende Datei in VSC öffnen und links aussen neben der Zeilennummer durch Anklicken Breakpoints setzen. Das ist ein roter Punkt bei dem der Debugger stehen bleibt.

- auf "Listen for Xdebug" klicken (oben, linke Spalte)
- im Browser die Appikation bzw. Datei aufrufen die getestet werden soll
- wenn der Breakpoint in der zu untersuchenden Datei erreicht wurde bleibt der Debugger dort stehen.
- mit den Buttons oben kann dann in Einzelschritten oder Programmweise weitergesprungen werden.


### Debug-Menü in VSC

#### Variablen
    
Der aktuelle Inhalt der Variablen und Konstanten:
-   local (die $Variablen des Scripts
-   Supgerglobals ($_SESSION, $_GET, $_Post, $_SERVER, usw.)
-   User defined constants (die im Script definierten Konstanten)
    
#### Überwachen

Variablen die im aktellen Debugging relevant sind, können hier mit + hinzugefügt werden. Bei vielen Variablen bietet das eine besere Übersichtlichkeit.
    
#### Aufrufliste

{main} - das in der URL aufgerufene Script
require - die durch *require* aufgerufenen includes.

Rechts wird die jeweilige Statement-Nummer angezeigt, bei der angehalten wurde
    
#### Haltepunkte

-   alle gesetzten Haltpunkte können durch anhaken aktiviert/deaktiviert werden
-   zusätzlich kann auch beim Auftreten von Notices, Warnings, Errors oder Execptions angehalten werden
    
### Nützliche Infos

- Wenn mehrere PHP-Versionen installiert sind, muss in jeder einzelnen Version die entsprechende Anpassung vorgenommen werden !
- Das Script kann im lokalen LAN auch von anderen Devices zum Testen aufgerufen werden. Das Debugging läuft am immer am Entwicklungsrechner. Es kann daher mit verschiedenen Endgeräten getestet werden.
    
    
letzte Änderung HR 2022-06-25 12:45 NK
