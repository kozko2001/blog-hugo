
---
title: NVM fast in mac
date: 2021-01-08 00:00:00
---
---

I normally use `nvm` to have multiple node versions, a lot of projects need older versions of node etc...

but nvm makes zsh load extreamly slow... and this just irritates me xD

here are the steps to install nvm, and configure it to load nvm not in the start of the shell, but only when we execute node.

credits to https://til-engineering.nulogy.com/Slow-Terminal-Startup-Tip-Lazy-Load-NVM/


1. Install nvm with brew

```
brew install nvm
```

2. configure nvm in your `.zshrc`
```
lazynvm() {
  unset -f nvm node npm npx
  export NVM_DIR=~/.nvm
  [ -s "/usr/local/opt/nvm/nvm.sh" ] && . "/usr/local/opt/nvm/nvm.sh" # This loads nvm
}

nvm() {
  lazynvm 
  nvm $@
}
 
node() {
  lazynvm
  node $@
}
 
npm() {
  lazynvm
  npm $@
}

npx() {
  lazynvm
  npx $@
}

```
