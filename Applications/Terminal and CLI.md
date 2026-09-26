# Terminal and CLI

Zsh and Neovim are the current choices; Nushell and Helix are possible successors. The rest of this page is a working tool list. Inclusion here does not make an application part of the base image.

## Shell

* Current: Zsh
* Future: Nushell (Structured Data)

## Text Editor

* Current: Neovim
* Future: Helix (Multi-Cursor)

## Modern CLI Replacements

* ripgrep (rg) → grep (fast, respects .gitignore)
* fd → find (simple syntax, fast)
* fzf → fuzzy finder for files/history/branches
* zoxide → cd + jump-by-frecency
* eza → ls (fork of exa)
* bat → cat (syntax highlighting, paging)
* delta → git diff pager (syntax-highlighted, readable diffs)

## Structured Text Processing

* jq, yq

## Document Conversion

* pandoc

## Markdown Reader

* frogmouth — https://github.com/Textualize/frogmouth

## Image Processing

* ImageMagick

## Terminal Productivity Apps
1. Browser — spegel
2. Email — aerc (https://aerc-mail.org/) or neomutt (https://neomutt.org/)
3. Calendar — calcurse (https://calcurse.org/) or khal (https://github.com/pimutils/khal)
4. Todo — taskwarrior (https://taskwarrior.org/)
5. Notes — frogmouth
6. Chat — weechat (IRC/Matrix/Slack via plugins) or gomuks (Matrix TUI, https://github.com/tulir/gomuks)
7. RSS — eilmeldung (from the original candidate list; still to evaluate) or newsboat (https://newsboat.org/)
8. Password Manager — rbw (unofficial Bitwarden CLI, https://github.com/doy/rbw) or pass (https://www.passwordstore.org/)
9. Link Manager — buku (https://github.com/jarun/buku)

## Office (Terminal)
1. Word Processor — wordgrinder (https://cowlark.com/wordgrinder/)
2. Spreadsheets — sc-im (https://github.com/andmarti1424/sc-im) — vim-like spreadsheet
3. PDF — termpdf.py (https://github.com/dsanson/termpdf.py) or pdftotext + less

## Media (Terminal)
1. Music — cmus (https://cmus.github.io/) or musikcube (https://musikcube.com/)
2. Images — viu (https://github.com/atanunq/viu) for inline terminal display, chafa for ASCII art
3. Video — mpv (plays in terminal with `--vo=tct` or sixel support)
4. Games — (not a terminal priority — use GUI apps)

## Analysis Tools (Terminal)
1. Text Editor/IDE — neovim (with LSP config) or helix
2. Debugger — gdb with TUI mode (`gdb -tui`) or cgdb (https://cgdb.github.io/)
3. Hex Editor — hexyl (https://github.com/sharkdp/hexyl) for viewing, xxd for editing
4. Network — termshark (https://github.com/gcla/termshark) — Wireshark TUI
5. Network scanning — nmap (CLI), rustscan (https://github.com/RustScan/RustScan)
6. DevTUI — https://github.com/skatkov/devtui
7. Virtualization — virsh (libvirt CLI), qemu direct invocation
8. Disassembly — objdump, radare2 (https://rada.re/)

## TUI Apps

* termshark — https://github.com/gcla/termshark

## Database TUI

* sqlit — https://github.com/Maxteabag/sqlit
* rainfrog — https://github.com/achristmascarl/rainfrog
* harlequin — https://github.com/tconbeer/harlequin

## Developer TUI

* lazygit — https://github.com/jesseduffield/lazygit
* REST client — https://github.com/unkn0wn-root/resterm/tree/main

## Video TUI

* ffdash — https://github.com/bcherb2/ffdash
* Youtube-TUI — https://siriusmart.github.io/youtube-tui/

## System Configuration TUI
1. Bluetooth — bluetui (https://github.com/pythops/bluetui)
2. WiFi — nmtui (built into NetworkManager) or impala (https://github.com/pythops/impala)
3. Systemd — sysz (https://github.com/joehillen/sysz) — fzf-based systemd unit browser

## Other

* wik (Encyclopedia) — https://github.com/yashsinghcodes/wik
* YouTube playlist to text — https://github.com/Ebrizzzz/Youtube-playlist-to-formatted-text
* Mosh (mobile shell) — https://mosh.org/

## Shell Configuration ToDo

* Zsh
* zsh-completion packages
* Starship terminal prompt enabled by default
