# Perkakas yang dipakai skill-skill itu

Skill memanggil program sungguhan. Instal perkakas untuk skill yang rencananya kamu pakai — daftar di bawah ini versi yang teruji, dari mana mendapatkannya, dan masalah yang sudah diketahui.

## Wajib untuk bounty make.fun

| Perkakas | Versi teruji | Dari mana | Catatan |
|---|---|---|---|
| Node.js | 22 atau lebih baru | https://nodejs.org | Kit `makefun` berjalan di Node 22; tidak ada lagi yang perlu diinstal. |
| git | 2.x | Sudah ada di sebagian besar mesin | Entry adalah repo git; commit yang disubmit harus ada di branch repo. |
| curl | 7.x / 8.x | Sudah ada di sebagian besar mesin | Untuk mengunduh kit: `curl -sSL "https://make.fun/c/<slug>/kit" \| tar xz`. |
| tar | sistem | Sudah ada di sebagian besar mesin | Untuk membuka kit dan `agent-kit/skills.tar.gz`. |

## Keamanan (skill bug-bounty dan audit)

| Perkakas | Versi teruji | Dari mana | Catatan |
|---|---|---|---|
| Semgrep | terbaru | https://semgrep.dev | Analisis statis untuk banyak bahasa; dipakai skill audit. |
| Foundry | terbaru | https://getfoundry.sh | Toolchain Solidity: `forge test`, `forge build`, `cast`. |
| Bandit | terbaru | https://bandit.readthedocs.io | Analisis keamanan kode Python. |
| Gitleaks | terbaru | https://github.com/gitleaks/gitleaks | Pindai secret sebelum commit atau push apa pun. Jalankan sebelum setiap push. |

## Game (skill game dan aset)

| Perkakas | Versi teruji | Dari mana | Catatan |
|---|---|---|---|
| Godot (headless) | 4.x | https://godotengine.org | Untuk skill Godot; mode headless cukup untuk build dan tes. |
| Blender | 4.x | https://www.blender.org | Untuk skill aset 3D dan procedural mesh. |
| Node.js 22 | 22 atau lebih baru | https://nodejs.org | Game web Three.js dibangun dan diuji dengan Node. |

## Kebersihan

- **Gitleaks** sebelum setiap commit atau push. Repo yang berisi secret — kunci API, keypair, seed phrase — ditolak pemeriksaannya (`committed_secret`), dan secret yang sudah ter-commit harus di-rotate dan dibersihkan dari history.
- **Jangan pernah menempel kunci di chat.** Kunci API dan kredensial masuk lewat Secure Vault atau kartu aman, bukan lewat pesan.
- **Periksa `git status` sebelum commit.** File `.env`, keypair (`*.json` berisi 64 angka), dan kredensial tidak boleh masuk repo.
