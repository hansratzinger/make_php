# PHP Erfahrungen

## Debuging in Visual Studio Code (VSC)

### !!! Die nachstehende Prozedur MUSS für jede installierte php-Version getrennt gemacht werden !!!

- In VSC die Extension PHP Debug installieren
- phpinfo.php Datei erstellen:

    ```
    <?php
    phpinfo();
    exit;
    ```

- phpinfo.php in localhost ausführen, Ausgabe markieren und kopieren

- [Installation Wizard](https://xdebug.org/wizard) aufrufen und kopierte Ausgabe von phpinfo in das Eingabefeld des Wizards einfügen und absenden.

- Die dann angezeigten Instruktionen ausführen.

- Xdebug-helper in Firefox/Erweiterungen installieren.

- den Webserver auf localhost neu starten

- In VSC auf Debugging klicken (Dreieck mit Käfer)

- auf Zahnrad klicken (launch.json öffnen) und folgenden JSON Code einfügen:

```
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003
        },

```

- die zu debuggende Datei in VSC öffnen und links aussen neben der Zeilennummer durch Anklicken Breakpoints setzen. Das ist ein roter Punkt bei dem der Debugger stehen bleibt.

- auf "Listen for Xdebug" klicken (oben, linke Spalte)
- im Browser die Appikation bzw. Datei aufrufen die getestet werden soll
- wenn der Breakpoint in der zu untersuchenden Datei erreicht wurde bleibt der Debugger dort stehen.
- mit den Buttons oben kann dann in Einzelschritten oder Programmweise weitergesprungen werden.
- der Variableninhalt wird in der linken Spalte angezeigt

HR 2022-06-14  21:17 NK
