# PHP Erfahrungen

## Debuging mit XDebug in Visual Studio Code (VSC) und Laragon

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

- Xdebug-helper in Firefox/Erweiterungen installieren.

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
- der Variableninhalt wird in der linken Spalte angezeigt

**!!! Wenn mehrere PHP-Versionen installiert sind, muss in jeder einzelnen Version die entsprechende Anpassung vorgenommen werden !!!**

letzte Änderung HR 2022-06-25  🕞 NK
