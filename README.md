# dfb-reel-queue

Warteschlange zwischen der **Cloud-Routine** (erzeugt 6×/Tag Reel-Content,
PC-unabhängig) und dem **Mac** (rendert + lädt zu festen Zeiten auf YouTube).

```
Cloud-Routine (6×/Tag) ──commit/push──▶  queue/*.json  ──git pull──▶  Mac rendert
       (läuft immer)                     (diese Repo)                 (wenn an/online,
                                                                       holt verpasste nach)
```

## Inhalt

- `queue/` — neue Content-JSONs (Cloud schreibt, Mac liest). Schema: `SCHEMA.md`.
- `themen-log.md` — Dedup-Gedächtnis; die Routine liest es VOR und ergänzt NACH
  der Themenwahl eine Zeile.
- `SCHEMA.md` — verbindliches Content-JSON-Schema + Regeln.
- `bibliothek-index.json` — reduzierter Bildbibliotheks-Index (tags/personen),
  damit die Routine nur vorhandene Motive/`search`-Begriffe wählt.
- `ROUTINE.md` — Zeitplan + Prompt für die `/schedule`-Cloud-Routine.

## Mac-Seite

`dfb-viralmaschine/sync-queue.sh` zieht neue `queue/*.json` per `git pull` in die
lokale `inbox/` (read-only ggü. diesem Repo → keine Merge-Konflikte). Der
launchd-Agent `com.dfb.reel-sync` ruft es alle 30 Min + beim Boot auf und holt so
verpasste Läufe nach Schlaf/Offline/Neustart automatisch nach.
