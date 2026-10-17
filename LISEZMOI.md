<!--
  Nom      : LISEZMOI.md
  Objet    : Présentation du dépôt code (cryptanalyse et bataille navale cryptographique)
  Auteur   : Eric PERRET
  Date     : 2026-10-17
  Licence  : MIT
-->

# 🔐 Code

🇬🇧 [English version: README.md](README.md)

Deux outils autonomes (un fichier HTML chacun, aucune librairie, aucune installation). Interfaces en français.

| Outil | Lancer | Documentation |
|---|---|---|
| Multi-Cipher Cracker v3.1.1 | ▶️ **[multi_cipher_v3_1_1.html](https://ericperret.github.io/code/multi_cipher_v3_1_1.html)** | [multi_cipher_v3_1_documentation.odt](multi_cipher_v3_1_documentation.odt) · [revue v2 (PDF)](<Revue & Documentation – Multi‑cipher Cracker V2.pdf>) |
| Bataille navale cryptographique v6 | ▶️ **[bataille_navale_v6.html](https://ericperret.github.io/code/bataille_navale_v6.html)** | [BATAILLE NAVALE CRYPTOGRAPHIQUE V6.rtf](<BATAILLE NAVALE CRYPTOGRAPHIQUE V6.rtf>) |

---

## Multi-Cipher Cracker

![Multi-Cipher Cracker v3.1.1](screenshot.png)

Cryptanalyse automatique des chiffrements classiques : l'outil analyse le texte chiffré, estime le type de chiffrement, lance en parallèle les attaques adaptées et classe les textes clairs obtenus par vraisemblance linguistique (français et anglais). Fonctionne hors ligne : modèles de langue et lexiques sont intégrés au fichier sous forme compressée.

### Fonctions

| Fonction | Description |
|---|---|
| Analyse | Indice de coïncidence, nombre de signes, diagnostic du type probable, longueurs de clé probables (clic = imposer) |
| Chiffrements | César, Bi-ROT, Atbash, Affine, Reverse ; Substitution (lettres ou symboles), Homophonique (Zodiac) ; Vigenère, Beaufort, Beaufort variante, Porta, Gronsfeld, Autokey ; Playfair, Two-Square, Four-Square, Bifid, Hill 2×2 ; ADFGX / ADFGVX, Nihilist ; Rail Fence, Colonnes simples, inverses et doubles ; XOR + Base64 ; Cascade |
| Grille | Lecture d'un texte en colonnes (période, spirale…), recherche combinée période + homophonique, graphique des périodes, export PNG |
| Palette de symboles | Saisie de textes à symboles |
| Résultats | Affichage au fil de l'eau, meilleur en tête, résultats dépliables, bouton STOP |
| Session | Export / import de la session, exemples intégrés (dont Z408 et Z340) |
| Auto-test | 25 cas, lancé aussi par `?selftest` dans l'URL |

### Méthode

- Score unique : log-vraisemblance moyenne des quadrigrammes, calibrée par langue (0 % = aléatoire, 100 % = texte réel) ; pentagrammes pour l'homophonique ; lexique pour l'affinage et le départage.
- Polyalphabétiques : χ² par colonne puis optimisation de chaque lettre de clé ; Playfair, Bifid, carrés, colonnes doubles, substitution : recuit simulé réparti sur un pool de Web Workers (threads logiques − 1).
- Données : quadrigrammes FR/EN complets, pentagrammes FR/EN (11,9 M entrées) décompressés à la demande ; corpus Gutenberg ; lexiques FrequencyWords (H. Dave, CC BY-SA 4.0).

Jeu d'essai : [`jeu de test.txt`](<jeu de test.txt>) (un texte chiffré par méthode, avec sa clé).

---

## Bataille navale cryptographique

![Bataille navale cryptographique v6](screenshot_bataille.png)

Bataille navale 26 × 26 à deux joueurs, en pair à pair dans le navigateur.

| Fonction | Description |
|---|---|
| Connexion | WebRTC en LAN, ou en WAN via des serveurs STUN publics ; codes de connexion échangés par copier-coller (SMS, mail…) |
| Défi | Le mot de passe de chaque joueur est chiffré par la position de sa flotte : SHA-256(grille + horodatage + nonce1 + nonce2) ; il ne se révèle qu'en coulant toute la flotte |
| Anti-rejeu | Horodatage et nonces propres à chaque partie |
| Flotte | 5 navires, 17 cases, placement automatique au hasard |
| Armes spéciales | Bombe (porte-avions, croix de 5 cases), torpille (sous-marin, ligne entière), radar (destroyer, distance) |

Seul accès réseau : les serveurs STUN, en mode WAN.

---

## Historique

| Version | Évolution |
|---|---|
| Multi-Cipher 3.1.1 | Pool de workers = threads logiques − 1 |
| Multi-Cipher 3.1.0 | Pentagrammes, Z408 résolu, nouveaux chiffrements, recherche combinée, auto-test étendu |
| Multi-Cipher 3.0.0 | Refonte : worker unique, registre des chiffrements, score unifié, module Grille |
| Bataille navale 6 | Anti-rejeu |

La v2.5 de Multi-Cipher est retirée du dépôt (seule la dernière version est conservée).

## Licence

MIT

## Auteur

**Eric PERRET** — [GitHub](https://github.com/ericperret)
