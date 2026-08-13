# 🏎️ RACER X (MikkelRacer)

Ein browserbasiertes **3D-Formel-1-Rennspiel**, gebaut mit [Three.js](https://threejs.org/) (WebGL) — komplett in einer einzigen `index.html`.

## Features

- **6 Teams** mit echten 3D-Automodellen: Ferrari, Red Bull, McLaren, Haas, Mercedes, ATOMIKS
- **3 Strecken**: L-Strecke, Monza, Großer G-Track
- **5 Kameras**: T-Cam, Verfolgung, Cockpit, TV-Cam, Top-Down (Taste `E` wechselt)
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

## Technik

- **Three.js 0.128** (via CDN, kein Build-Schritt nötig)
- 3D-Automodelle im `.glb`-Format im Ordner `models/`
- Strecken als Catmull-Rom-Splines, prozedural erzeugte Umgebung (Bäume, Tribünen, Leitplanken)
- Kein Framework, keine Abhängigkeiten außer Three.js — reines HTML/JS
