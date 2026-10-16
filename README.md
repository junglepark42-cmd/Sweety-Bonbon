# Sweety Bonbons

Jeu match-3 original pour le parc Sweety Sweety. HTML/CSS/JavaScript sans dépendance à l’exécution, sans publicité, compte, achat ni limite de temps.

## Jouer

Glisser un bonbon vers son voisin, ou toucher deux cases voisines. Aligner trois formes identiques. Un échange invalide ne coûte aucun coup. Quatre bonbons créent une ligne, cinq un arc-en-ciel, un T ou un L une explosion. Échanger deux bonus les combine. Le glaçage disparaît quand son bonbon est récolté ; les rubans se libèrent par un alignement adjacent ou une explosion. Les bonbons emprisonnés restent fixes jusqu’à leur libération.

Le premier niveau montre un échange valide. Un indice gestuel revient après 6,5 secondes d’inactivité et reste disponible au bouton. La progression, les meilleurs scores, les étoiles, la partie en cours et le son sont conservés dans le navigateur. Une nouvelle partie est toujours disponible immédiatement.

## Développement

- `npm ci`
- `npm test` : tests unitaires du moteur et des sauvegardes.
- `npm run balance` : 30 graines par niveau, politique d’objectifs et politique aléatoire. Génère un chemin de victoire rejouable pour chacun des 20 niveaux dans `evidence/balance.json`.
- `npx playwright install --with-deps chromium`
- `npm run test:browser` : essais tactiles CDP dans Chromium, prise en main, victoire, défaite, reprise, formats et hors ligne. Captures du vrai jeu dans `evidence/`.
- `npm run serve` : http://localhost:4173/Sweety-Bonbon/
- `node tools/build.cjs` : paquet `dist/` et empreintes SHA-256 dans `build.json`.

`js/engine.js` contient les règles, `js/app.js` les entrées et animations, `js/storage.js` les sauvegardes, `js/audio.js` les sons synthétisés originaux, `js/levels.js` les 20 aventures. Les ressources sont dans `assets/`.

## Publication et récupération

L’état initial du dépôt est le commit `42e7cd065cae41475385a980d937d87d014aecd6`. Le développement s’effectue sur `feat/sweety-bonbons`. Aucun autre dépôt n’est modifié.

Les workflows valident avant de déployer. `pages.yml` ne publie que `main`, après tests moteur, simulations et navigateur. Le contenu publié inclut la révision et les empreintes exactes dans `build.json`. Les captures et rapports sont conservés comme artefacts de workflow.

PWA : tous les fichiers du jeu sont mis en cache au premier chargement réussi. Le service worker ne touche qu’aux caches Sweety Bonbons et à son propre périmètre. Incrémenter sa version lors d’une mise à jour du contenu hors ligne. Le jeu fonctionne sous `/Sweety-Bonbon/` et utilise des chemins relatifs.

## Limites de la validation

Les simulations prouvent l’existence de chemins gagnants pour les graines testées, pas que chaque choix humain gagne ni que toute grille possible est résoluble. Le réglage enfant devra être confirmé par observation au parc. Chromium mobile émulé n’est pas un essai Android physique ; Safari et iOS nécessitent un essai séparé. Les sauvegardes peuvent être effacées avec les données du navigateur.

Voir `assets/README.md` pour la provenance des ressources.
