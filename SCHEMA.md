# Content-JSON-Schema (Warteschlange → Reelmaschine)

Jede Datei in `queue/` ist EIN Reel-Auftrag. Dateiname:
`<UTC-Zeitstempel>_<slug>.json`, z. B. `2026-06-21T1330Z_musiala-comeback.json`.

Der Mac zieht neue Dateien aus `queue/` in seine `inbox/` und rendert sie. Die
**Bild-Auswahl passiert auf dem Mac** gegen die echte Bildbibliothek – wähle hier
nur `search`-Begriffe/Motive, die in `bibliothek-index.json` vorkommen
(`tags`/`personen`). Spezial-Motive, die es dort nicht gibt → `"thematic": true`.

```json
{
  "slug": "musiala-comeback",
  "createdAt": "2026-06-21T13:30:00Z",
  "title": "Musiala zurück im Training",
  "script": "Gesprochener Text, Hook zuerst, ~70–90 Wörter.",
  "uploadCaption": "Text für den Upload-Post.",
  "uploadHashtags": "#DFB #WM2026 #Fussball",
  "images": [
    { "file": "musiala.jpg",   "search": "Jamal Musiala" },
    { "file": "training.jpg",  "search": "DFB Training" },
    { "file": "wirtz.jpg",     "search": "Florian Wirtz" },
    { "file": "stadion.jpg",   "search": "NRG Stadium" },
    { "file": "fans.jpg",      "search": "DFB Fans" },
    { "file": "nagelsmann.jpg","search": "Julian Nagelsmann" },
    { "file": "jubel.jpg",     "search": "DFB Jubel" },
    { "file": "kabine.jpg",    "search": "DFB Kabine" }
  ],
  "scenes": [
    { "type": "hook",  "text": "ER IST ZURÜCK.", "image": "musiala.jpg", "weight": 0.5 },
    { "type": "title", "eyebrow": "WM 2026", "title": "Musiala zurück", "image": "training.jpg", "weight": 0.7 },
    { "type": "image", "image": "musiala.jpg",  "name": "Jamal Musiala", "role": "Offensiv · 22", "weight": 0.8 },
    { "type": "image", "image": "nagelsmann.jpg","name": "Julian Nagelsmann", "role": "Bundestrainer", "weight": 0.8 },
    { "type": "stats", "title": "Zahlen", "stats": [{ "label": "Tore", "value": "12" }], "image": "training.jpg", "weight": 0.9 },
    { "type": "image", "image": "wirtz.jpg",    "name": "Florian Wirtz", "role": "Offensiv · 22", "weight": 0.8 },
    { "type": "image", "image": "stadion.jpg",  "weight": 0.8 },
    { "type": "image", "image": "kabine.jpg",   "weight": 0.8 },
    { "type": "image", "image": "jubel.jpg",    "weight": 0.8 },
    { "type": "image", "image": "fans.jpg",     "weight": 0.8 },
    { "type": "outro", "title": "Cliffhanger?", "subtitle": "Folgen für Teil 2", "image": "fans.jpg", "weight": 1.0 }
  ]
}
```

## Pflichtregeln

- **`createdAt`** (NEU): UTC-Zeitstempel der Erzeugung (ISO 8601, `…Z`). Wird für
  den Frische-Schutz beim geplanten YouTube-Upload genutzt – Content, der beim
  Rendern älter als ~18 h ist, geht nicht automatisch live. **Immer setzen.**
- **10–12 Szenen** pro Reel, davon **mind. 6 `image`-Szenen** (schnelle Schnitte).
- **≥ 8 Motive** im `images`-Array; dasselbe Bibliotheksbild wird nie zweimal im
  selben Reel verwendet → genug verschiedene Motive liefern.
- **Jede Szene hat ein `image`.** `image`-Szenen sind reine Vollbild-Motive ohne
  Text; sichtbarer Text gehört in `hook`/`title`/`stats`/`outro`.
- **Jedes Bild braucht ein `search`-Feld** (Personenname oder Motiv). Keine URLs,
  keine Websuche – nur Begriffe, die in `bibliothek-index.json` vorkommen.
- **Namensschild:** klares Spielerfoto → `name` + `role` setzen (nicht auf
  hook/outro).
- **`thematic: true`** nur bei Spezial-Motiven, die die Fußball-Bibliothek
  normalerweise NICHT hat (z. B. Giftschlange, Milchreis) – am besten beim Hook-
  Bild. Fehlt es, blockiert es die Produktion nicht (wird ersetzt + als Wunsch
  notiert).

## Viral-Regeln

- Hook mit Curiosity Gap in den ersten 2 Sekunden; konkrete **Zahlen** im Script
  (werden gold gehighlightet).
- Ein Hook, **einmal** – keine Wiederholung/Bild-Doppelung im Outro.
- Outro = **polarisierende, leicht beantwortbare Frage** (Kommentar-Bait).
- **Format-Rotation** (in Klammern ans Ende der themen-log-Zeile): News-Drama,
  Top-3-Liste, Geheimnis, Duell/Vergleich.
