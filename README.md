# WinT-1000

Version 1.5.23 · Copyright © 2026 Harald Thomas · MIT-Lizenz

Terminal-Client für Windows: lokale Shell, SSH, Telnet, RDP, serielle Konsole, horizontal und vertikal teilbare Panes, Multi-Input und Multi-Paste, Makros, Datei-Browser, TFTP-/FTP-/HTTP-/SFTP-Server, gemeinsame Netzwerk-Konfiguration und Aufruf von außen.

Updates: [github.com/denkteich/WinT-1000](https://github.com/denkteich/WinT-1000)

## Zwei Varianten

| | Installierbar (Setup) | Portable |
|---|---|---|
| Datei | `WinT-1000-1.5.23-setup.exe` | `WinT-1000-1.5.23-portable.exe` |
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

## Datei-Browser und Kopieren (ab 1.5.23)

- **Synchron mit der Shell** (Standard: an): Wechselt man im SSH-Terminal mit `cd` das Verzeichnis, wechselt der Datei-Browser automatisch mit. Schalter **⇄** in der Werkzeugleiste des Browsers, unter ⋯ oder in den Einstellungen. Erkannt wird das Verzeichnis über die Pfad-Meldung OSC 7, sonst über die Prompt-Zeile (`user@host:~/pfad$`, `root@host:/etc#`) oder den Fenstertitel. Zeigt der Prompt keinen Pfad: ⋯ → „Pfad-Meldung in der Shell einrichten (bash/zsh)“ (gilt für die laufende Shell; dauerhaft dieselbe Zeile in `~/.bashrc` bzw. `~/.zshrc` auf dem Server eintragen). Selbst im Browser navigiert bleibt die Ansicht, bis die Shell das nächste Mal das Verzeichnis wechselt; ist das Shell-Verzeichnis nicht lesbar (z. B. nach `sudo -i`), bleibt die bisherige Liste mit Hinweis stehen.
- **Drag & Drop:** Dateien/Ordner aus dem Explorer in die Liste ziehen = Hochladen (auf einen Ordner gezogen landen sie dort). Einträge aus der Liste in den Explorer, auf den Desktop oder in eine andere App ziehen = Herunterladen: WinT-1000 lädt sie dafür erst in einen temporären Ordner; bei kleinen Dateien beginnt das Ziehen sofort, solange die Maustaste gedrückt bleibt. Wird sie vorher losgelassen (große Dateien), erscheint der Eintrag unter „Übertragungen“ mit „fertig – an das Ziel ziehen“ und lässt sich von dort ans Ziel ziehen.
- **Direkt zur Datei springen:** In die Liste klicken und tippen – z. B. `zus` markiert den ersten Eintrag, der mit „zus“ beginnt (sonst den ersten, der „zus“ enthält); nach einer Sekunde Pause beginnt die Suche neu. ↑/↓ markieren, Enter öffnet, Rücktaste = eine Ebene höher, Esc hebt die Markierung auf.
- **Kopieren beim Markieren:** Mit der Maus markierter Text in einem Session-Fenster landet sofort in der Zwischenablage („In die Zwischenablage kopiert“). Einstellung „Markierten Text automatisch in die Zwischenablage kopieren“, Standard an (mit 1.5.23 einmalig eingeschaltet, falls sie bisher aus war). In Programmen mit Mausbedienung (htop, mc) beim Markieren Umschalt gedrückt halten.

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
- Links: `wint1000://ssh/admin@10.0.0.1?run=show%20version&close=3`, `wint1000://ssh/admin@10.0.0.2?layout=core&slot=unten`
- Vorlagen im Ordner `beispiele`: Batch-Datei und PowerShell-Skript. Für Verknüpfungen: Rechtsklick auf den Desktop → Neu → Verknüpfung → einen der Befehle als Ziel. Für zeitgesteuerte Abläufe die Aufgabenplanung mit demselben Befehl verwenden.

### Feste Plätze im geteilten Fenster (ab 1.5.22)

Damit mehrere getrennte Aufrufe nacheinander in dasselbe geteilte Fenster kommen – z. B. der erste oben, der nächste unten –, bekommt der Tab einen Namen und jedes Ziel einen Platz:

```bat
%W% --ssh admin@10.0.0.1 --layout core --slot oben
%W% --ssh admin@10.0.0.2 --layout core --slot unten
```

| Option | Bedeutung |
|---|---|
| `--layout NAME` | Name des Layout-Tabs. Gibt es ihn noch nicht, wird er angelegt und gleich passend geteilt; leere Plätze zeigen „Wartet: unten“. Danach findet jeder Aufruf den Tab über den Namen – egal, welcher Tab oder welches Pane gerade aktiv ist. Ohne Angabe heißt das Layout „Layout“ |
| `--slot PLATZ` | `oben`, `unten` (Raster oben/unten), `links`, `rechts` (links/rechts), `oben-links`, `oben-rechts`, `unten-links`, `unten-rechts` (2×2), `1`–`4` (Reihenfolge wie beim Lesen) oder `next` = nächster freier Platz. Englische Namen (`top`, `bottom`, `left`, `right`, `tl` …) gehen auch. Ohne Angabe: `next` |
| `--grid RASTER` | `2h` = oben/unten, `2v` = links/rechts, `4` = 2×2. Nur nötig bei `next` oder Zahlen – sonst ergibt es sich aus dem Platz. Gilt nur beim Anlegen; ein vorhandener Layout-Tab behält sein Raster |
| `--busy WAS` | Wenn im Platz schon eine Session läuft: `fragen` (Standard), `ersetzen` (bisherige Session beenden), `neu` (Platz zusätzlich teilen, bisherige läuft weiter), `abbrechen` (nichts öffnen) |

- Frei ist ein Platz, solange er wartet oder seine Session beendet ist; beendete Sessions werden ohne Rückfrage ersetzt.
- `next` füllt zuerst wartende, dann beendete und dann geschlossene Plätze; sind alle belegt, öffnet der Aufruf einen neuen Tab.
- Wurde ein Platz geschlossen (auch durch `--close`), legt der nächste Aufruf für diesen Platz ihn an der richtigen Stelle wieder an. Wird der ganze Tab geschlossen, beginnt das Layout beim nächsten Aufruf von vorn.
- In wartenden Plätzen kann man auch selbst eine Verbindung öffnen – dann ist der Platz belegt.
- `--multi` schaltet Multi-Input für alle Bereiche des Layout-Tabs ein.
- Mit „Tabs und Split-Layout beim Start wiederherstellen“ bleiben Layout-Name und Plätze auch nach einem Neustart erhalten.
- Ganz ohne zusätzliche Parameter: Einstellung **Aufrufe von außen ohne Platzangabe** (oben/unten, links/rechts oder 2×2). Dann landen alle Aufrufe ohne `--split`, `--slot` oder `--layout` der Reihe nach im Layout-Tab „Aufrufe“.

## Gemeinsame Netzwerk-Konfiguration

WinT-1000 legt im gewählten Ordner `WinT-1000-config.json` (plus Ordner `WinT-1000-Backups`) an. Liegt dort bereits die Konfigurationsdatei der Mac-Ausgabe, wird diese mitbenutzt, damit Macs und PCs denselben Stand teilen.

## Releases auf GitHub

Damit die Update-Prüfung und das automatische Update funktionieren, im Repository [denkteich/WinT-1000](https://github.com/denkteich/WinT-1000) je Version ein Release mit dem Tag `v<Version>` (z. B. `v1.5.23`) anlegen und diese Dateien anhängen:

- `WinT-1000-<Version>-setup.exe` – wird von der installierten Version automatisch geladen und installiert
- `WinT-1000-<Version>-portable.exe` – für die portable Variante (manuell)

## Hinweise

- Getestet wurde nur in einer Linux-Testumgebung (Oberfläche im Windows-Modus, Abläufe, Update-Logik mit Testserver); ein Test auf einem echten Windows-Rechner steht aus – auch für Installer und automatisches Update.
- Die Windows-Firewall fragt beim ersten Start eines Servers (TFTP/FTP/HTTP/SFTP) ggf., ob eingehende Verbindungen erlaubt werden.
