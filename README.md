# Course de billes

A marble-race picker for the classroom. Every selected student is a marble; the first one across the finish line gets picked.

Open `index.html` in a browser (no build step).

## Use it

1. **Importer un fichier Excel**: each sheet becomes a group. The importer looks for a `Prénom` column (and `Nom` if present) in the first rows, so the class-list workbooks work as-is. Summary rows like "Moyenne de classe" are skipped.
2. Pick a group. Every student is in the race by default; tap a name to take it out.
3. **Lancer la course** (or press Space). The camera follows the leader. Every race builds a new track: two random sections, the lock, three more random sections, then la chute Montmorency and the finish. Sections are sometimes mirrored.
   - Sections: la forêt boréale (pegs), le Chemin du Roy (zigzag ramps), les moulins à vent (spinners), les rapides du Long-Sault (bumpers), **la roue du moulin à eau** (a wheel whose cups carry marbles back up), **la batterie royale** (cannon cups that fire marbles back into the air), **le pont de glace** (frictionless tilting planks) and **les trappes de la citadelle** (trapdoors that open at random).
   - **L’écluse de Lachine** holds the pack halfway down until 80 % of the marbles arrive (or 6.5 s pass), then drops everyone at once.
   - **Coups de théâtre** fire every few seconds (more often after the lock), never repeating one of the last three: *la foudre* (leader sent back), *portage* (a back marble jumps up behind the leaders), *barrage de castor* (front group blocked), *embâcle* (leader frozen in ice), *la chasse-galerie* (last place flies to the front, rare), *troc de fourrures* (leader swaps places with a back marble), *tempête de neige* (top 3 slowed) and *le monde à l’envers* (gravity flips briefly).
4. The winner is listed under *Déjà pigé·e·s* and, if the option is on, left out of the next races. *Remettre tout le monde* puts everyone back.

Speed (1×/2×/3×), 3D, sound and fullscreen toggles sit at the top right of the track.

**3D view** (on by default): the same race drawn in 3D with shadows, rolling striped marbles and a camera that follows the leader, swoops in on each twist and closes in on the finish. The **3D** button switches back to the flat view; if a computer renders under 14 frames per second, the page drops to 2D on its own for that visit. You can also paste a list (one name per line, `Nom, Prénom` or tab-separated) to create a group.

## Privacy

Student lists stay in the browser's `localStorage`; nothing is uploaded. The `.gitignore` keeps spreadsheets out of this public repo.

## Tech

Single HTML file. Physics with [Matter.js](https://brm.io/matter-js/) 0.19 (the 3D view renders that same 2D simulation with [three.js](https://threejs.org/) r160, loaded only when 3D is on); spreadsheets read with [SheetJS](https://sheetjs.com/) 0.18.5, loaded only when you import. Winners come from the physics simulation, seeded with randomized start positions (`crypto.getRandomValues`).
