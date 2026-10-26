# chris-code.de

Website zur Domain chris-code.de. Hauptzweck: die Pflicht-URLs für den App Store
(Support, Datenschutz) für die App **CalTick**, plus Impressum.

## Arbeitsweise

- Antworten auf Deutsch.
- Saubere, getrennte Commits.
- Kein Build-Schritt: reines statisches HTML + eine `style.css`.

## Aufbau

| Pfad | Inhalt |
|---|---|
| `index.html` | Startseite, App-Kachel CalTick |
| `caltick/support/index.html` | Kontakt, FAQ |
| `caltick/datenschutz/index.html` | Datenschutzerklärung (App + Website) |
| `impressum/index.html` | Impressum nach § 5 DDG, § 18 Abs. 2 MStV |
| `caltick/icon.png` | App-Icon (256 px, aus dem CalTick-Projekt) |
| `style.css` | Farben als Tokens auf `:root`, Dunkelmodus per `prefers-color-scheme` |
| `CNAME` | `chris-code.de` (für GitHub Pages) |
| `.nojekyll` | GitHub Pages ohne Jekyll ausliefern |

Konventionen:
- Schöne URLs: Ordner mit `index.html`, Links absolut (`/caltick/support/`).
- Jede Seite: Deutsch oben, Englisch darunter in `<section id="en" lang="en">`.
  Die App-Store-Links fürs Englische zeigen auf `…/#en`.

## Kontaktdaten

Anschrift und E-Mail (`christian.halstrick@mailbox.org`) stehen in Support, Datenschutz und Impressum.
- Fürs Impressum ist eine ladungsfähige Anschrift nötig, kein Postfach.
- Beim Ändern der Datenschutzerklärung das „Stand“-Datum (de und en) anpassen.

## Hosting: GitHub Pages

- GitHub-Account `christian-halstrick`, Repo `christian-halstrick/chris-code.de`, Branch `main`.
- Commit-Identität im Repo: `Christian Halstrick <348430540+christian-halstrick@users.noreply.github.com>`.
  Keine privaten Mailadressen in Commits.

Erledigt am 26.10.2026: Push, Pages (Branch `main`, `/`), CNAME `chris-code.de`,
DNS bei INWX, Let's-Encrypt-Zertifikat (chris-code.de + www), HTTPS erzwungen.

Domain im GitHub-Konto verifiziert. Der TXT-Eintrag
`_github-pages-challenge-christian-halstrick` bei INWX muss dafür stehen bleiben.

Hinweis: Ändert man `cname` per API, committet GitHub die Datei `CNAME` selbst,
mit der Commit-Adresse aus dem GitHub-Konto. Danach `git pull`.

## DNS bei INWX

- Registrar und Nameserver: INWX (`ns.inwx.de`, `ns2.inwx.de`, `ns3.inwx.eu`).
- Kein Webspace bei INWX.
- Die alte INWX-Parkseite (`185.181.104.242`) ist entfernt. NS- und SOA-Einträge bleiben unverändert.
- Bei INWX pro Adresse ein eigener Eintrag, Name für die Hauptdomain leer lassen.

Der Nutzer setzt die Einträge selbst. Danach mit `dig` prüfen.

| Name | Typ | Wert |
|---|---|---|
| @ | A | 185.199.108.153, .109.153, .110.153, .111.153 |
| @ | AAAA | 2606:50c0:8000::153, 8001::153, 8002::153, 8003::153 |
| www | CNAME | christian-halstrick.github.io |

## Fakten zu CalTick (für Texte auf der Seite)

Quellcode: `~/dev/Apple/CalTick` (eigenes Repo, eigene Claude-Session). Dort `README.md` und `docs/AppStore.md` (Store-Checkliste).

**Die App:**
- Kompakte Apple-Watch-App (Ultra 2, watchOS 11+) mit iPhone-Begleit-App (iOS 17+).
- Zeigt Termine von heute bis übermorgen und nur fällige bzw. überfällige Erinnerungen.
- Bundle-IDs: `de.chris-code.caltick` (iPhone), `de.chris-code.caltick.watchkitapp` (Uhr).
- Sprachen der App: Deutsch, Englisch, Französisch, Japanisch, Chinesisch (vereinfacht).

**Datenfluss:**
- Liest Kalender und Erinnerungen per EventKit, nur auf dem Gerät.
- Kein Server, kein Konto, keine Analyse, kein Tracking.
- Abhaken auf der Uhr: watchOS erlaubt das Ändern von Erinnerungen nicht. Die Uhr schickt deshalb Kennung, Titel und Fälligkeit per WatchConnectivity an die iPhone-App, die die Erinnerung abhakt.
- Diagnose-Log bleibt auf dem Gerät. Es geht nur per „Log senden“ ans eigene iPhone und lässt sich von dort selbst teilen.

**Geburtstage:** Doppelte Geburtstage aus Kontakten, Google usw. werden zu einer Zeile zusammengefasst.
