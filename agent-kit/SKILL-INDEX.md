# Indeks skill — yang dikurasi, dengan repo sumbernya

Kit ini mengkurasi 25 skill: 23 salinan kata demi kata dari kit lain, ditambah 2 skill yang ditulis Renako untuk kit ini. Sebuah skill dipakai dengan memuat filenya sebelum pekerjaan yang dicakupnya, bukan sesudahnya.

Skill yang disalin kata demi kata tercantum dengan sumbernya di bawah. Skill lokal yang dirakit di kit asal tidak punya satu repo publik — indeks ini mengatakannya begitu adanya, bukan mengarang tautan yang tidak bisa diverifikasi. Skill yang ditulis Renako dilabeli begitu.

## Sumber

- **Skill make.fun** — https://make.fun/skill.md — loop bounty itu sendiri (mencari, membangun, submit, klaim). Dokumen resmi make.fun; baca langsung dari sana, bukan dari arsip ini.
- **Gamedev (upstream)** — https://github.com/gamedev-skills/awesome-gamedev-agent-skills
- **Kit asal (diperakit di sana, tanpa satu repo publik)** — https://github.com/Skyzee2704/makefun-getting-started — skill-skill lokal di bawah dirakit di kit itu (set bounty, set game, dan gabungan skill agent), jadi tercantum di sini dengan apa yang dilakukannya, bukan dengan tautan repo yang tidak bisa diverifikasi. Arsip di repo ini mengambil salinan kata demi kata dari kit itu.
- **Renako (ditulis untuk kit ini)** — ditulis oleh Renako, agent yang membangun repo ini, khusus untuk kit ini.

## make.fun — 3 skill

`makefun-bounty-workflow` (Renako), `makefun_recording_seal` (kit asal).

Skill make.fun sendiri — `makefun` — hidup di https://make.fun/skill.md dan dibaca dari sana.

## Bug bounty — 14 skill

`bug-bounty-starter` (Renako), `bug-bounty-null200ok`, `bb-methodology`, `evm-audit-skills`, `claude-cyber-security-skills`, `bugbountyrules`, `agentic-bug-hunter`, `bug-bounty`, `web2-recon`, `web2-vuln-classes`, `web3-audit`, `triage-validation`, `report-writing`, `bugcrowd-reporting` (kit asal).

Sub-skill di dalam koleksi besar:

- **EVM audit (20)** — muat `evm-audit-master` dulu, lalu yang dibutuhkan kontraknya: `evm-audit-access-control`, `evm-audit-assembly`, `evm-audit-bridges`, `evm-audit-chain-specific`, `evm-audit-defi-amm`, `evm-audit-defi-lending`, `evm-audit-defi-staking`, `evm-audit-dos`, `evm-audit-erc20`, `evm-audit-erc4337`, `evm-audit-erc4626`, `evm-audit-erc721`, `evm-audit-flashloans`, `evm-audit-general`, `evm-audit-governance`, `evm-audit-oracles`, `evm-audit-precision-math`, `evm-audit-proxies`, `evm-audit-signatures`. Semua ada di dalam folder `evm-audit-skills` di arsip.
- **Claude cyber security (30)** — `asset-discovery`, `ato-chains`, `auth-bypass`, `bugcrowd-reporting`, `business-logic`, `cache-poisoning`, `cloud-misconfig`, `content-discovery`, `continuous-monitoring`, `file-upload`, `fingerprinting`, `graphql`, `hackerone-reporting`, `http-smuggling`, `idor-hunting`, `js-analysis`, `jwt-attacks`, `llm-ai-security`, `mobile-recon-android`, `oauth-oidc`, `program-selection`, `scope-analysis`, `sqli`, `ssrf`, `ssti`, `subdomain-enum`, `subdomain-takeover`, `threat-modeling-mindmap`, `triage-validation`, `xss`. Semua ada di dalam folder `claude-cyber-security-skills` di arsip. Repo sumber koleksi ini, sebagaimana tercatat di file-file-nya, adalah https://github.com/0xGhostCAT/claude-cybersecurity-skills

## Game dan aset — 6 skill

`threejs-fundamentals`, `threejs-game-builder`, `ship-web-games`, `test-playable-web-games` (kit asal), `godot-2d-movement`, `roblox-studio-workflow` (gamedev upstream).

## Agent — 3 skill

`ultimate-orchestrator`, `agent-skill-integration`, `agent-evaluation` (kit asal).

## Cara router memilih

Deteksi bounty berjalan dulu. Tugas bounty tidak pernah lewat orchestrator umum — ia lewat `makefun-bounty-workflow` untuk bounty make.fun, atau `bb-methodology` → `bug-bounty-null200ok` → `evm-audit-skills` → `claude-cyber-security-skills` → `bugbountyrules` untuk bounty bug. Semua yang lain dirutekan menurut domainnya: game-3d, aset, Roblox, orkestrasi. Kalau skill untuk suatu pekerjaan tidak ada, router mengatakannya begitu saja, bukan menebak-nebak — skill yang hilang adalah fakta, bukan alasan untuk mengarang satu.
