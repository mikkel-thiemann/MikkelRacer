# 🏎️ RACER X (MikkelRacer)

Ein browserbasiertes **3D-Formel-1-Rennspiel**, gebaut mit [Three.js](https://threejs.org/) (WebGL) — komplett in einer einzigen `index.html`.

## Features

- **6 Teams** mit echten 3D-Automodellen: Ferrrarri, Red Bull, McLaren, Haas, Mercedes, ATOMIKS
- **3 Strecken**: L-Strecke, Monza, Großer G-Track
- **5 Kameras**: T-Cam, Verfolgung, Cockpit, TV-Cam, Top-Down (Taste `E` wechselt)
- **Echter Tages- und Nachtverlauf**: Sonnenstand nach Datum, Uhrzeit und Standort — mittags hoch im Süden, Morgen- und Abenddämmerung zur richtigen Zeit, nachts Sternenhimmel mit Mond in seiner echten Position und Phase
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

## Tageszeit ausprobieren

Der Himmel richtet sich nach der echten Uhrzeit. Zum Anschauen der anderen
Tageszeiten kann man sie in der Adresszeile vorgeben:

| Adresse | Zeigt |
|---------|-------|
| `index.html?zeit=12:00` | Mittagssonne |
| `index.html?zeit=06:15` | Morgendämmerung |
| `index.html?zeit=20:45` | Abenddämmerung |
| `index.html?zeit=23:30` | Nacht mit Sternen und Mond |
| `index.html?zeit=12:00&datum=2026-12-21` | Mittag am kürzesten Tag |

Der Standort steht im Script bei `const ORT` (Vorgabe: Zürich).

## Technik

- **Three.js 0.128** (via CDN, kein Build-Schritt nötig)
- 3D-Automodelle im `.glb`-Format im Ordner `models/`
- Strecken als Catmull-Rom-Splines, prozedural erzeugte Umgebung (Bäume, Tribünen, Leitplanken)
- Kein Framework, keine Abhängigkeiten außer Three.js — reines HTML/JS
