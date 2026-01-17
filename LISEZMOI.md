🔐 Code

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](#)
[![Pure HTML/JS](https://img.shields.io/badge/Pure-HTML%2FJS-blue.svg)](#)
[![Cryptography](https://img.shields.io/badge/Domain-Cryptography-red.svg)](#)

**Boîte à outils de cryptanalyse de chiffrements classiques** — Casser les chiffrements historiques par attaques statistiques.

![Screenshot](screenshot.png)

## 🚀 Fonctionnalités

- **Chiffre de Vigenère** — Examen de Kasiski, indice de coïncidence
- **Chiffre de Beaufort** — Analyse de chiffrement réciproque
- **Chiffre de César** — Analyse fréquentielle, force brute
- **Chiffre XOR** — Texte clair connu, crib dragging
- **Base64** — Utilitaires d'encodage/décodage
- **Validation par Dictionnaire** — Vérifier le texte clair contre des listes de mots
- **Web Workers** — Traitement en arrière-plan pour les textes longs

## 🛠️ Technologies

- HTML/CSS/JavaScript pur
- Web Workers pour le calcul parallèle
- Algorithmes d'analyse fréquentielle
- Aucune dépendance externe

## 📖 Utilisation

1. Ouvrir \`index.html\` dans un navigateur
2. Coller le texte chiffré
3. Sélectionner le type de chiffrement suspecté
4. Cliquer sur **Analyser** pour lancer les attaques
5. Examiner les textes clairs candidats

## 🎓 Techniques Implémentées

- **Analyse Fréquentielle** — Comparaison de distribution des lettres
- **Indice de Coïncidence** — Estimation de la longueur de clé
- **Examen de Kasiski** — Analyse des séquences répétées
- **Attaque par Dictionnaire** — Validation du texte clair
- **Test du Chi-deux** — Fitness statistique

## 📄 Licence

MIT

## 👤 Auteur

**Eric PERRET** — [GitHub](https://github.com/ericperret)
`