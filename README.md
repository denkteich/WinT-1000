# WinT-1000

ein Schwesterprojekt zu MacT-1000 (https://github.com/denkteich/MacT-1000)

Version 1.5.21 · Copyright © 2026 Harald Thomas · MIT-Lizenz

Terminal-Client für Windows: lokale Shell, SSH, Telnet, RDP, serielle Konsole, horizontal und vertikal teilbare Panes, Multi-Input und Multi-Paste, Makros, Datei-Browser, TFTP-/FTP-/HTTP-/SFTP-Server, gemeinsame Netzwerk-Konfiguration und Aufruf von außen.

Updates: [github.com/denkteich/WinT-1000](https://github.com/denkteich/WinT-1000)

## Zwei Varianten

| | Installierbar (Setup) | Portable |
|---|---|---|
| Datei | `WinT-1000-1.5.21-setup.exe` | `WinT-1000-1.5.21-portable.exe` |
| Installation | Assistent; Standardordner `%LOCALAPPDATA%\Programs\WinT-1000`, Ordner wählbar; Startmenü- und Desktop-Verknüpfung | keine – EXE an einen beliebigen Ort kopieren (z. B. `C:\Tools`, USB-Stick) und starten |
| Administratorrechte | nicht nötig (Installation nur für das eigene Benutzerkonto) | nicht nötig |
| `wint1000://`-Links | werden bei der Installation eingerichtet | im Hilfe-Dialog „Links für diese EXE einrichten“ |
| Updates | automatisch: Installer laden, SHA-256 prüfen, nach Rückfrage still installieren und neu starten | nur Hinweis; „Herunterladen“ öffnet die Release-Seite, die EXE ersetzt sich nicht selbst |
| Deinstallation | Einstellungen → Apps → WinT-1000 | EXE löschen |

Beide Varianten sind nicht signiert. Windows SmartScreen meldet beim ersten Start ggf. „Der Computer wurde durch Windows geschützt“ → „Weitere Informationen“ → „Trotzdem ausführen“.

Einstellungen, Sessions und Makros liegen bei beiden Varianten unter `%APPDATA%\WinT-1000` – sie bleiben beim Update und beim Wechsel zwischen Setup und portabler EXE erhalten. Daten der bisherigen Windows-Version (bis 1.5.20) werden beim ersten Start einmalig übernommen. Die portable EXE entpackt sich beim Start in einen temporären Ordner, der erste Start dauert daher einige Sekunden.

## Bedienung unter Windows

| Bereich | Windows |
|---|---|
| Lokale Shell | PowerShell 7 (`pwsh`), sonst Windows PowerShell, sonst `cmd.exe`; eigene Shell in den Einstellungen |

| SSH | eingebauter OpenSSH-Client (`C:\Windows\System32\OpenSSH\ssh.exe`); fehlt er: Einstellungen → System → Optionale Features → „OpenSSH-Client“ |
| Datei-Browser | per SFTP (eigene Verbindung, fragt Passwort/Passphrase selbst ab) |
| RDP | Remotedesktopverbindung (`mstsc.exe`) |
| Seriell | COM-Ports, z. B. `COM3 115200` im Quick Connect |
| Passwörter | werden mit der Windows-Benutzeranmeldung verschlüsselt gespeichert |
| Menü | Datei, Bearbeiten, Makros, Ansicht, Hilfe (Einstellungen unter Datei, Über/Updates unter Hilfe) |

## Tastenkürzel

Strg+Buchstabe bleibt für die Shell frei (Strg+C, Strg+D, Strg+R …). Programmfunktionen liegen auf Strg+Umschalt.

| Funktion | Kürzel |
|---|---|
| Kopieren / Einfügen | Strg+Umschalt+C / Strg+Umschalt+V (Strg+C kopiert, wenn Text markiert ist; Strg+V fügt ein) |
| Neuer Tab / Lokale Shell | Strg+Umschalt+T / Strg+Umschalt+L |
| Vertikal teilen (nebeneinander) | Strg+Umschalt+E |
| Horizontal teilen (untereinander) | Strg+Umschalt+O |
| Pane maximieren | Strg+Umschalt+X |
| Pane / Tab schließen | Strg+Umschalt+W |
| Quick Connect | Strg+Umschalt+K |
| Datei-Browser | Strg+Umschalt+D |
| Tab wechseln | Strg+Tab / Strg+Umschalt+Tab |
| Pane wechseln (über alle Tabs) | Alt+Umschalt+Pfeiltaste |
| Vollbild / Entwicklerwerkzeuge | F11 / F12 |
| Dialog bestätigen | Strg+Enter |

Die vollständige Liste zeigt das Menü; Tooltips in der Oberfläche nennen jeweils das Windows-Kürzel.

## Aufruf von außen

Hilfe → „Aufruf von außen…“ zeigt fertige Befehle zum Kopieren (mit dem Pfad der laufenden EXE). Beispiele für die installierte Version:

```bat
set W="%LOCALAPPDATA%\Programs\WinT-1000\WinT-1000.exe"
%W% --local --run "ipconfig"
%W% --ssh admin@10.0.0.1 --run "show version" --split right
%W% --serial COM3:115200
%W% --folder Rechenzentrum --multi
%W% --ssh admin@10.0.0.1 --run "show running-config" --log "%USERPROFILE%\Logs\core-sw01.log" --close 3
%W% --local --run "ipconfig /all" --quit
```

- Läuft WinT-1000 schon, öffnet sich ein neuer Tab im vorhandenen Fenster.
- Befehle aus Aufrufen von außen werden nur nach Rückfrage ausgeführt (abschaltbar je Aufruf: „künftig ohne Rückfrage“).
- `--close [SEK]`: nach dem letzten Befehl schließen, sobald SEK Sekunden (Standard 3) keine Ausgabe mehr kommt. Beendet sich die Sitzung sauber (z. B. `exit`), schließt das Pane sofort; Fehler bleiben sichtbar.
- `--log DATEI`: Ausgabe ohne Farbcodes an DATEI anhängen. Vollständiger Pfad nötig, z. B. `C:\Logs\sw.log`, `\\server\freigabe\sw.log` oder `~\Logs\sw.log` (`~` = Benutzerordner); fehlende Ordner werden angelegt.
- `--quit`: alle Ziele des Aufrufs schließen und WinT-1000 danach beenden – nur, wenn keine anderen Sessions oder Server mehr laufen.
- `--close` und `--log` sind bei RDP nicht möglich (eigenes Programm).
- Links: `wint1000://ssh/admin@10.0.0.1?run=show%20version&close=3`
- Vorlagen im Ordner `beispiele`: Batch-Datei und PowerShell-Skript. Für Verknüpfungen: Rechtsklick auf den Desktop → Neu → Verknüpfung → einen der Befehle als Ziel. Für zeitgesteuerte Abläufe die Aufgabenplanung mit demselben Befehl verwenden.

## Gemeinsame Netzwerk-Konfiguration

WinT-1000 legt im gewählten Ordner `WinT-1000-config.json` (plus Ordner `WinT-1000-Backups`) an. Liegt dort bereits die Konfigurationsdatei der Mac-Ausgabe, wird diese mitbenutzt, damit Macs und PCs denselben Stand teilen.

## Releases auf GitHub

Damit die Update-Prüfung und das automatische Update funktionieren, im Repository [denkteich/WinT-1000](https://github.com/denkteich/WinT-1000) je Version ein Release mit dem Tag `v<Version>` (z. B. `v1.5.21`) anlegen und diese Dateien anhängen:

- `WinT-1000-<Version>-setup.exe` – wird von der installierten Version automatisch geladen und installiert
- `WinT-1000-<Version>-portable.exe` – für die portable Variante (manuell)

## Hinweise

- Getestet wurde nur in einer Linux-Testumgebung (Oberfläche im Windows-Modus, Abläufe, Update-Logik mit Testserver); ein Test auf einem echten Windows-Rechner steht aus – auch für Installer und automatisches Update.
- Die Windows-Firewall fragt beim ersten Start eines Servers (TFTP/FTP/HTTP/SFTP) ggf., ob eingehende Verbindungen erlaubt werden.
