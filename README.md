<!--
  Name     : README.md
  Purpose  : Overview of the code repository (cryptanalysis and cryptographic battleship)
  Author   : Eric PERRET
  Date     : 2026-10-27
  License  : CC BY-NC 4.0 — commercial use forbidden without the author's written permission (eperret@azs.fr)
-->

# 🔐 Code

🇫🇷 [Version française : LISEZMOI.md](LISEZMOI.md)

Two standalone tools (one HTML file each, no library, no installation). User interfaces in French.

| Tool | Launch |
|---|---|
| Multi-Cipher Cracker v3.24.0 | ▶️ **[multi_cipher_v3_24_0.html](https://ericperret.github.io/code/multi_cipher_v3_24_0.html)** |
| Cryptographic battleship v6 | ▶️ **[bataille_navale_v6.html](https://ericperret.github.io/code/bataille_navale_v6.html)** — manual (French): [BATAILLE NAVALE CRYPTOGRAPHIQUE V6.rtf](<BATAILLE NAVALE CRYPTOGRAPHIQUE V6.rtf>) |

---

## Multi-Cipher Cracker

![Multi-Cipher Cracker v3.24.0: Kryptos K4 section file and analysis](screenshot.png)

Automatic cryptanalysis of classical ciphers: the tool analyses the ciphertext, preselects the plausible ciphers, runs the matching attacks in parallel and ranks the candidate plaintexts by linguistic likelihood (French and English). Works offline, including from `file://`: language models and word lists are embedded in the file in compressed form.

### Usage

1. Open the link above (Chrome / Edge 90+, Firefox 113+, Safari 16.4+) and wait for "Prêt" (ready).
2. Paste the ciphertext, or a **section file** (template provided in the tool, opened on Kryptos K4), or pick an example.
3. **DÉCODE**: simple encodings only. **CRACK**: cryptanalysis of the ticked ciphers. **STOP** halts everything; results already found stay displayed.

### Features

| Feature | Description |
|---|---|
| Section file | `[CIPHERTEXT]`, `[KNOWN_PLAINTEXT]` / `[KNOWN_COMBINATIONS]` ("Position a-b : WORD", base 0 and 1 tested), `[INFO]`, `#` lines; template that can be copied for an AI |
| Analysis | Index of coincidence, symbol counts, diagnosis, likely key lengths (click = force) |
| Preselection | Ciphers ticked automatically from the text: encoding, number groups, ADFGVX, symbols, length, IC, χ², digrams, known plaintext |
| Direct decoders | Base64, Base32, hex, binary, decimal / octal ASCII, ROT13, ROT47, Atbash, reverse, executed Brainfuck; chained up to 3 layers; `FLAG{…}` flag brought to the top 🚩 |
| Monoalphabetic | Caesar, Bi-ROT, Atbash, Affine, Reverse, Substitution (letters or symbols) |
| Homophonic | Homophonic (Zodiac Z408 solved), symbol-words (nomenclator), null symbols, codes in number groups |
| Polyalphabetic | Vigenère, Beaufort, variant Beaufort, Porta, Gronsfeld, Autokey, Quagmire I to IV; known key, hints, CTF list, word list, brute force 1 to 7 letters; known plaintext imposed per column |
| Digraphic and fractionating | Playfair, Two-Square, Four-Square, Bifid, Hill 2×2, ADFGX / ADFGVX, Nihilist, Two 5×5 tables + seed (keyword or free) |
| Transpositions | Rail Fence, simple, inverse and double Columnar; grid transposition (rotations, serpentines, diagonals, spiral, period, toroidal diagonal); 3D block transposition |
| W segments | "W = separators" option (W and line breaks), per-segment view with known plaintext per column |
| Views | Grid (PNG export), isometric SVG 3D block (hover, path, PNG export), period chart, symbol palette |
| Results | Streamed, best first, expandable; continuous line + line split into words; minimum score 15 % |
| Session | Export / import, built-in examples (including Z408 and Z340), "?" help on every control |
| Self-test | Also started by `?selftest` in the URL |

### Method

- **Single score**: mean quadgram log-likelihood, calibrated per language (0 % = random, 100 % = real text); pentagrams and plaintext entropy for homophonic ciphers; word list for refinement and word splitting.
- **Polyalphabetic**: χ² per column then optimisation of each key letter, plus whole keys tested; a key is kept only if the plaintext contains real words.
- **Simulated annealing** (substitution, homophonic, Playfair, Bifid, squares, double columnar, two tables) spread over a pool of Web Workers (logical threads − 1); workload split into blocks (brute force, dictionary, widths, seeds); "∞" duration until STOP.
- **Proof of reading and stop**: null model (random text with the language's letter frequencies); a plaintext is proven if the chance probability of its words × keys tested < 10⁻⁸; enumeration stops at the first proven plaintext, annealing is confirmed by two agreeing seeds.
- **Data**: complete FR/EN quadgrams, FR/EN pentagrams (11.9 M entries) decompressed on demand; Gutenberg corpora (20 French, 27 English books); FrequencyWords 30,000-word lists (H. Dave, CC BY-SA 4.0); Z408 / Z340 (zodiackillerciphers.com, K. Gorman).

Test set: [`jeu de test.txt`](<jeu de test.txt>) (one ciphertext per method, with its key). The detailed version history (2.7 → 3.24.0) is in the header block of `multi_cipher_v3_24_0.html`.

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

## License

**Free for non-commercial use** — [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/), with mandatory credit of the source and the author:

> code — Eric PERRET — https://github.com/ericperret/code

Any commercial use is forbidden without the author's written permission, requested by e-mail: **eperret@azs.fr**.
Full terms (French / English): [LICENSE](LICENSE).

## Author

**Eric PERRET** — [GitHub](https://github.com/ericperret) — [www.azs.fr](https://www.azs.fr/)
