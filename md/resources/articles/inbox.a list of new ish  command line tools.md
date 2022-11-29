---
created: 1652786933653
desc: ''
id: yk0odeoc53rbsrv097ptwue
tags:
- articles
- webmark
title: A List of New Ish  Command Line Tools
updated: 1652815514958
---
   
Topics::  [linux](../../topics/linux.md)   
   
   
---   
   
# [A list of new(ish) command line tools](https://jvns.ca/blog/2022/04/12/a-list-of-new-ish--command-line-tools/)   
   
Hello! Today I asked [on twitter](https://twitter.com/b0rk/status/1513903221466664962) about newer command line tools, like `ripgrep` and `fd` and `fzf` and `exa` and `bat`.   
   
I got a bunch of replies with tools I hadn’t heard of, so I thought I’d make a list here. A lot of people also pointed at the [modern-unix](https://github.com/ibraheemdev/modern-unix) list.   
   
### replacements for standard tools   
   
   
- [ripgrep](https://github.com/BurntSushi/ripgrep/), [ag](https://github.com/ggreer/the_silver_searcher), [ack](https://github.com/beyondgrep/ack3) (grep)   
- [exa](https://github.com/ogham/exa), [lsd](https://github.com/Peltoche/lsd) (ls)   
- [mosh](https://mosh.org/) (ssh)   
- [bat](https://github.com/sharkdp/bat) (cat)   
- [delta](https://github.com/dandavison/delta) (a pager for git)   
- [fd](https://github.com/sharkdp/fd) (find)   
- [drill](https://www.nlnetlabs.nl/projects/ldns/about/), [dog](https://github.com/ogham/dog) (dig)   
- [duf](https://github.com/muesli/duf) (df)   
- [dust](https://github.com/bootandy/dust), ncdu (du)   
- [pgcli](https://www.pgcli.com/) (psql)   
- [btm](https://github.com/ClementTsang/bottom), [btop](https://github.com/aristocratos/btop), [glances](https://github.com/nicolargo/glances), [gtop](https://github.com/aksakalli/gtop), [zenith](https://github.com/bvaisvil/zenith) (top)   
- [tldr](https://tldr.sh/) (man, sort of)   
- [sd](https://github.com/chmln/sd) (sed)   
- [difftastic](https://github.com/Wilfred/difftastic) (diff)   
- mtr (traceroute)   
- [plocate](https://plocate.sesse.net/) (locate)   
- xxd, [hexyl](https://github.com/sharkdp/hexyl) (hexdump)   
   
### new inventions   
   
Here are some tools that are not exactly replacements for standard tools:   
   
   
- [z](https://github.com/rupa/z), [fasd](https://github.com/clvv/fasd), [autojump](https://github.com/wting/autojump), [zoxide](https://github.com/ajeetdsouza/zoxide) (tools to make it easier to find files / change directories)   
- [broot](https://github.com/Canop/broot), [nnn](https://github.com/jarun/nnn), [ranger](https://github.com/ranger/ranger) (file manager)   
- [direnv](https://github.com/direnv/direnv) (load environment variables depending on the current directory)   
- [fzf](https://github.com/junegunn/fzf), [peco](https://github.com/peco/peco) (“fuzzy finder”)   
- [croc](https://github.com/schollz/croc) and [magic-wormhole](https://github.com/magic-wormhole/magic-wormhole) (send files from one computer to another)   
- [hyperfine](https://github.com/sharkdp/hyperfine) (benchmarking)   
- [httpie](https://httpie.io/), [curlie](https://github.com/rs/curlie), [xh](https://github.com/ducaale/xh) (for making HTTP requests)   
- [entr](https://github.com/eradman/entr) (run arbitrary commands when files change)   
- [asdf](https://github.com/asdf-vm/asdf) (version manager for multiple languages)   
- [tig](https://github.com/jonas/tig), [lazygit](https://github.com/jesseduffield/lazygit) (interactive interfaces for git)   
- [lazydocker](https://github.com/jesseduffield/lazydocker) (interactive interface for docker)   
- [choose](https://github.com/theryangeary/choose) (the basics of awk/cut)   
- [ctop](https://github.com/bcicen/ctop) (top for containers)   
- [fuck](https://github.com/nvbn/thefuck) (autocorrect command line errors)   
- [tmate](https://tmate.io/) (share your terminal with a friend)   
- [lnav](https://github.com/tstack/lnav), [angle-grinder](https://github.com/rcoh/angle-grinder) (tools for managing logs)   
- [mdp](https://github.com/visit1985/mdp), [glow](https://github.com/charmbracelet/glow) (ways to display markdown in the terminal)   
- pbcopy/pbpaste (for clipboard <> stdin/stdout) maybe aren’t “new” but were mentioned a lot. You can [use xclip](https://stackoverflow.com/questions/5130968/how-can-i-copy-the-output-of-a-command-directly-into-my-clipboard/41843618#41843618) to do the same thing on Linux.   
   
**JSON/[languages.YAML](../../devlog/languages.YAML.md)/CSV things:**   
   
   
- [jq](https://stedolan.github.io/jq/) (a great JSON-wrangling tool)   
- [jc](https://github.com/kellyjonbrazil/jc) (convert various tools’ output into JSON)   
- [jo](https://github.com/jpmens/jo) (create JSON objects)   
- [yq](https://github.com/mikefarah/yq) (like `jq`, but for [languages.YAML](../../devlog/languages.YAML.md)). there’s also [another yq](https://github.com/kislyuk/yq)   
- [fq](https://github.com/wader/fq) (like `jq`, but for binary)   
- [htmlq](https://github.com/mgdm/htmlq) (like `jq`, but for HTML)   
- [fx](https://github.com/antonmedv/fx) (interactive json tool)   
- [jless](https://github.com/PaulJuliusMartinez/jless) (json pager)   
- [xsv](https://github.com/BurntSushi/xsv) (a command line tool for csv files, from burntsushi)   
- [visidata](https://www.visidata.org/) (“an interactive multitool for tabular data”)   
- [miller](https://github.com/johnkerl/miller) (“like awk/sed/cut/join/sort for CSV/TSV/JSON/JSON lines”)   
   
**grep things:**   
   
   
- [pdfgrep](https://pdfgrep.org/) (grep for PDF)   
- [gron](https://github.com/tomnomnom/gron) (make JSON greppable)   
- [ripgrep-all](https://github.com/phiresky/ripgrep-all) (ripgrep, but also PDF, zip, ebooks, etc)   
   
### less-new tools   
   
Here are a few of not-so-new tools folks mentioned aren’t that well known:   
   
   
- pv (“pipe viewer”, gives you a progress bar for a pipe)   
- vidir (from [moreutils](https://joeyh.name/code/moreutils), lets you batch rename/delete files in vim)   
- sponge, ts, parallel (also from moreutils)   
   
### some of my favourites   
   
My favourites of these that I use already are `entr`, `ripgrep`, `git-delta`, `httpie`, `plocate`, and `jq`.   
   
I’m interested in trying out `direnv`, `btm`, `z`, `xsv`, and `duf`, but I think the most exciting tool I learned about is `vidir`.