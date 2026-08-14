# 🏎️ RACER X (MikkelRacer)

Ein browserbasiertes **3D-Formel-1-Rennspiel**, gebaut mit [Three.js](https://threejs.org/) (WebGL) — komplett in einer einzigen `index.html`.

## Features

- **6 Teams** mit echten 3D-Automodellen: Ferrrarri, Red Bull, McLaren, Haas, Mercedes, ATOMIKS
- **3 Strecken**: L-Strecke, Monza, Großer G-Track
- **5 Kameras**: T-Cam, Verfolgung, Cockpit, TV-Cam, Top-Down (Taste `E` wechselt)
- **Tag-Nacht-Wechsel im Zeitraffer**: Sonne und Mond ziehen ihre echte Bahn, aber ein ganzer Tag dauert nur 8 Minuten — Sonnenaufgang, Mittag, Abendrot und Sternenhimmel mit Mond in seiner echten Phase, alles während des Fahrens
- **KI-Gegner** mit individuellen Fahrprofilen (Topspeed, Grip, Bremse, Aggressivität)
- Vollständiges **HUD**: Live-Leaderboard, Position, Rundenzeit, Tacho, Gang- und Power-Anzeige
- Startampel, 3 Runden, Ziel-Screen
- Steuerung per Tastatur **oder** Touch — funktioniert auch auf dem Handy

## Spielen

Wegen der 3D-Modelle (`models/*.glb`) muss die Seite über einen lokalen Webserver laufen — direktes Öffnen der Datei per Doppelklick funktioniert nicht.

```bash
# Im Projektordner:
python -m http.server 8000
```

Dann im Browser öffnen: <http://localhost:8000/index.html>

Alternativ unter Windows einfach `start_server.bat` doppelklicken.

## Steuerung

| Taste | Aktion |
|-------|--------|
| `W` / `↑` | Gas |
| `S` / `↓` | Bremse |
| `A` / `←` | Links |
| `D` / `→` | Rechts |
| `E` | Kamera wechseln |

## Tageszeit

Das Spiel startet zur echten Uhrzeit, danach läuft die Zeit **180-mal schneller**:
ein ganzer Tag dauert 8 Minuten, eine echte Sekunde sind 3 Spielminuten. Während
eines Rennens wandert die Sonne also sichtbar weiter.

Einstellen im Script:

- `const TAG_MINUTEN=8` — wie lange ein ganzer Tag dauert
- `const ORT` — Standort, bestimmt Sonnenhöhe und Auf-/Untergang (Vorgabe: Zürich)

Startzeit vorgeben in der Adresszeile:

| Adresse | Startet bei |
|---------|-------------|
| `index.html?zeit=06:15` | Morgendämmerung |
| `index.html?zeit=12:00` | Mittagssonne |
| `index.html?zeit=20:45` | Abendrot |
| `index.html?zeit=23:30` | Nacht mit Sternen |
| `index.html?zeit=12:00&datum=2026-12-21` | Mittag am kürzesten Tag |
| `index.html?tempo=1` | echte Zeit, kein Zeitraffer |

## Technik

- **Three.js 0.128** (via CDN, kein Build-Schritt nötig)
- 3D-Automodelle im `.glb`-Format im Ordner `models/`
- Strecken als Catmull-Rom-Splines, prozedural erzeugte Umgebung (Bäume, Tribünen, Leitplanken)
- Kein Framework, keine Abhängigkeiten außer Three.js — reines HTML/JS
