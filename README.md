<!--
  Name     : README.md
  Purpose  : Overview of the code repository (cryptanalysis and cryptographic battleship)
  Author   : Eric PERRET
  Date     : 2026-10-17
  License  : MIT
-->

# 🔐 Code

🇫🇷 [Version française : LISEZMOI.md](LISEZMOI.md)

Two standalone tools (one HTML file each, no library, no installation). User interfaces in French.

| Tool | Launch | Documentation (French) |
|---|---|---|
| Multi-Cipher Cracker v3.1.1 | ▶️ **[multi_cipher_v3_1_1.html](https://ericperret.github.io/code/multi_cipher_v3_1_1.html)** | [multi_cipher_v3_1_documentation.odt](multi_cipher_v3_1_documentation.odt) · [v2 review (PDF)](<Revue & Documentation – Multi‑cipher Cracker V2.pdf>) |
| Cryptographic battleship v6 | ▶️ **[bataille_navale_v6.html](https://ericperret.github.io/code/bataille_navale_v6.html)** | [BATAILLE NAVALE CRYPTOGRAPHIQUE V6.rtf](<BATAILLE NAVALE CRYPTOGRAPHIQUE V6.rtf>) |

---

## Multi-Cipher Cracker

![Multi-Cipher Cracker v3.1.1](screenshot.png)

Automatic cryptanalysis of classical ciphers: the tool analyses the ciphertext, estimates the cipher type, runs the matching attacks in parallel and ranks the candidate plaintexts by linguistic likelihood (French and English). Works offline: language models and word lists are embedded in the file in compressed form.

### Features

| Feature | Description |
|---|---|
| Analysis | Index of coincidence, symbol counts, diagnosis of the likely type, likely key lengths (click = force) |
| Ciphers | Caesar, Bi-ROT, Atbash, Affine, Reverse; Substitution (letters or symbols), Homophonic (Zodiac); Vigenère, Beaufort, variant Beaufort, Porta, Gronsfeld, Autokey; Playfair, Two-Square, Four-Square, Bifid, Hill 2×2; ADFGX / ADFGVX, Nihilist; Rail Fence, simple, inverse and double Columnar; XOR + Base64; Cascade |
| Grid | Reading a text written in columns (period, spiral…), combined period + homophonic search, period chart, PNG export |
| Symbol palette | Entry of symbol texts |
| Results | Streamed as they come, best first, expandable results, STOP button |
| Session | Session export / import, built-in examples (including Z408 and Z340) |
| Self-test | 25 cases, also started by `?selftest` in the URL |

### Method

- Single score: mean quadgram log-likelihood, calibrated per language (0 % = random, 100 % = real text); pentagrams for homophonic ciphers; word list for refinement and tie-breaking.
- Polyalphabetic ciphers: χ² per column then optimisation of each key letter; Playfair, Bifid, squares, double columnar, substitution: simulated annealing spread over a pool of Web Workers (logical threads − 1).
- Data: complete FR/EN quadgrams, FR/EN pentagrams (11.9 M entries) decompressed on demand; Gutenberg corpora; FrequencyWords lists (H. Dave, CC BY-SA 4.0).

Test set: [`jeu de test.txt`](<jeu de test.txt>) (one ciphertext per method, with its key).

---

## Cryptographic battleship

![Cryptographic battleship v6](screenshot_bataille.png)

26 × 26 battleship for two players, peer to peer in the browser.

| Feature | Description |
|---|---|
| Connection | WebRTC on a LAN, or over the Internet through public STUN servers; connection codes exchanged by copy-paste (SMS, mail…) |
| Challenge | Each player's password is encrypted by the position of their fleet: SHA-256(grid + timestamp + nonce1 + nonce2); it is revealed only by sinking the whole fleet |
| Anti-replay | Timestamp and nonces unique to each game |
| Fleet | 5 ships, 17 cells, random automatic placement |
| Special weapons | Bomb (aircraft carrier, 5-cell cross), torpedo (submarine, whole line), radar (destroyer, distance) |

Only network access: the STUN servers, in WAN mode.

---

## History

| Version | Change |
|---|---|
| Multi-Cipher 3.1.1 | Worker pool = logical threads − 1 |
| Multi-Cipher 3.1.0 | Pentagrams, Z408 solved, new ciphers, combined search, extended self-test |
| Multi-Cipher 3.0.0 | Rewrite: single worker, cipher registry, unified score, Grid module |
| Battleship 6 | Anti-replay |

Multi-Cipher v2.5 has been removed from the repository (only the latest version is kept).

## License

MIT

## Author

**Eric PERRET** — [GitHub](https://github.com/ericperret)
