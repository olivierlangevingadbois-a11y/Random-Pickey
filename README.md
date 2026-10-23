# Course de billes

A marble-race picker for the classroom. Every selected student is a marble; the first one across the finish line gets picked.

Open `index.html` in a browser (no build step).

## Use it

1. **Importer un fichier Excel**: each sheet becomes a group. The importer looks for a `Prénom` column (and `Nom` if present) in the first rows, so the class-list workbooks work as-is. Summary rows like "Moyenne de classe" are skipped.
2. Pick a group. Every student is in the race by default; tap a name to take it out.
3. **Lancer la course** (or press Space). The camera follows the leader through la forêt boréale, le Chemin du Roy, l’écluse de Lachine, les moulins de la seigneurie, les rapides du Long-Sault and la chute Montmorency.
   - **L’écluse de Lachine** holds the pack halfway down until 80 % of the marbles arrive (or 6.5 s pass), then drops everyone at once: an early lead is wiped out.
   - **Coups de théâtre** hit the second half every few seconds: *la foudre* sends the leader back up, *le portage* carries a marble from the back of the pack up behind the leaders, and *un barrage de castor* blocks the front group for a few seconds.
4. The winner is listed under *Déjà pigé·e·s* and, if the option is on, left out of the next races. *Remettre tout le monde* puts everyone back.

Speed (1×/2×/3×), sound and fullscreen toggles sit at the top right of the track. You can also paste a list (one name per line, `Nom, Prénom` or tab-separated) to create a group.

## Privacy

Student lists stay in the browser's `localStorage`; nothing is uploaded. The `.gitignore` keeps spreadsheets out of this public repo.

## Tech

Single HTML file. Physics with [Matter.js](https://brm.io/matter-js/) 0.19; spreadsheets read with [SheetJS](https://sheetjs.com/) 0.18.5, loaded only when you import. Winners come from the physics simulation, seeded with randomized start positions (`crypto.getRandomValues`).
