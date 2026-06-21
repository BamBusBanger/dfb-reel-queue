# Cloud-Routine: 6×/Tag ein Reel-Auftrag

Diese Datei ist der **Auftrag für die geplante Cloud-Routine** (`/schedule`).
Sie läuft 6×/Tag und ist komplett PC-unabhängig – sie erzeugt nur den Content
und committet ihn; das Rendern macht der Mac, sobald er an/online ist.

## Zeitplan (Europe/Berlin)

Recherche ~0,5 h vor dem jeweiligen YouTube-Slot:
**07:30, 11:30, 14:30, 17:30, 19:30, 21:30**.
(Veröffentlichungs-Slots auf YouTube: 08:00, 12:00, 15:00, 18:00, 20:00, 22:00.)

## Prompt für die Routine

```
Du erzeugst EINEN viralen Kurzvideo-Auftrag zur Fußball-WM 2026 (Fokus deutsche
Nationalmannschaft) für die DFB-Reelmaschine.

1. Lies themen-log.md komplett. Wähle ein FRISCHES Thema, das dort noch NICHT
   vorkommt, und rotiere das Format (News-Drama / Top-3-Liste / Geheimnis /
   Duell-Vergleich) gegenüber den letzten Einträgen.
2. Recherchiere die aktuellsten DFB/WM26-News (heute) per Websuche. Nimm konkrete
   Fakten und Zahlen.
3. Lies SCHEMA.md und bibliothek-index.json. Baue ein VALIDES Content-JSON exakt
   nach SCHEMA.md. Wichtig:
   - createdAt = aktueller UTC-Zeitstempel (ISO 8601, endet auf Z).
   - 10–12 Szenen, ≥6 image-Szenen, ≥8 Motive im images-Array.
   - search-Begriffe: Bibliotheks-Motive (bibliothek-index.json, tags/personen)
     BEVORZUGEN. Lücken füllt der Renderer automatisch: echte Personen/Events mit
     echtem Suchbegriff → Web; konzeptionelle Spezial-Motive OHNE echte Person mit
     "thematic": true → KI-generiert (thematic NIE für echte Spieler).
   - Hook in den ersten 2 Sek., Zahlen im Script, Outro = polarisierende Frage.
4. Schreibe die Datei nach queue/<UTC-Zeitstempel>_<slug>.json
   (Zeitstempel-Format z. B. 2026-06-21T1330Z).
5. Hänge EINE Zeile an themen-log.md an:
   <YYYY-MM-DD> | <slug> | <Kern-Thema, Stichworte> (FORMAT)
6. git add -A && git commit -m "<slug>" && git push

Erzeuge pro Lauf genau EIN Reel. Bei Doppel-Trigger nichts überschreiben
(Zeitstempel im Dateinamen sorgt für Eindeutigkeit).
```

## Einrichtung (einmalig)

Per `/schedule` eine Routine gegen dieses Repo anlegen, 6× täglich zu den oben
genannten Zeiten, mit obigem Prompt. Die Routine braucht Schreib-/Push-Recht auf
das Repo.
