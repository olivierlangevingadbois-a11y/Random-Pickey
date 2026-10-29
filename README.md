# Course de billes

A marble-race picker for the classroom. Every selected student is a marble; the first one across the finish line gets picked.

Open `index.html` in a browser (no build step).

## Use it

1. **Importer un fichier Excel**: each sheet becomes a group. The importer looks for a `Prénom` column (and `Nom` if present) in the first rows, so the class-list workbooks work as-is. Summary rows like "Moyenne de classe" are skipped.
2. Pick a group. Every student is in the race by default; tap a name to take it out.
3. **Lancer la course** (or press Space). The camera follows the leader. Every race builds a new track: two random sections, the lock, three more random sections, then la chute Montmorency and the finish. Sections are sometimes mirrored.
   - Sections: la forêt boréale (pegs), le Chemin du Roy (zigzag ramps), les moulins à vent (spinners), les rapides du Long-Sault (bumpers), **la roue du moulin à eau** (a wheel whose cups carry marbles back up), **la batterie royale** (cannon cups that fire marbles back into the air), **le pont de glace** (frictionless tilting planks) and **les trappes de la citadelle** (trapdoors that open at random).
   - **L’écluse de Lachine** holds the pack halfway down until 80 % of the marbles arrive (or 6.5 s pass), then drops everyone at once.
   - **Coups de théâtre** are announced 3 seconds ahead (banner countdown, a target ring on the marble at risk, a storm cloud over the leader before lightning) and never repeat one of the last three: *la foudre* (leader sent back), *portage* (a back marble jumps up behind the leaders), *barrage de castor* (front group blocked), *embâcle* (leader frozen in ice), *la chasse-galerie* (last place flies to the front, rare), *troc de fourrures* (leader swaps places with a back marble), *tempête de neige* (top 3 slowed) and *le monde à l’envers* (gravity flips briefly).
4. The winner is listed under *Déjà pigé·e·s* and, if the option is on, left out of the next races. *Remettre tout le monde* puts everyone back.

Speed (1×/2×/3×), 3D, sound and fullscreen toggles sit at the top right of the track.

**3D run** (on by default): a real 3D marble race in the style of *Marble Race*. Marbles are spheres rolling through railed channels, spirals, conical funnels and tilted boards, bumping into each other in 3D. Each race strings together the start plate, two random sections, the lock, three more random sections and the final straight, linked by funnels:
- le Chemin du Roy (stacked switchback channels), la tour Martello (a banked spiral around a tower), le tourbillon du Saint-Laurent (a wide bowl marbles circle down), la forêt boréale (a steep board planted with pines), les moulins à vent (a board with turning paddles), les rapides du Long-Sault (a board of kicking bumpers) and les trappes de la citadelle (trapdoors that flash, then drop).
- The same twists apply, announced 3 seconds ahead. A broadcast camera follows the front of the pack at a fixed angle and cuts to a side-on photo-finish shot. A race clock and ▲▼ position changes sit above the standings.
- The **3D** button switches to the classic flat run (2D). If a computer renders under 14 frames per second, the next race runs in 2D.

The physics is a small purpose-built engine (sphere against boxes, capsules and funnel shells, plus marble-to-marble hits); three.js r160 renders it. Open the page with `#debug` to get `window.__race`, which steps the race without rendering (used for flow tests).

## Privacy

Student lists stay in the browser's `localStorage`; nothing is uploaded. The `.gitignore` keeps spreadsheets out of this public repo.

## Tech

Single HTML file. The 3D run uses its own physics and [three.js](https://threejs.org/) r160 (loaded only when 3D is on); the flat run uses [Matter.js](https://brm.io/matter-js/) 0.19; spreadsheets read with [SheetJS](https://sheetjs.com/) 0.18.5, loaded only when you import. Winners come from the physics simulation, seeded with randomized start positions (`crypto.getRandomValues`).
