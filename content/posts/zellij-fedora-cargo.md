---
title: "Install Zellij Fedora With Cargo"
date: 2024-11-13T08:36:38+01:00
draft: false
tags: ["zellij", "fedora", "cargo"]
---

# How to install zellij on Fedora Linux using cargo

As it is said on zellij [webiste](https://zellij.dev/):
> Zellij is a terminal workspace. It has the base functionality of a terminal multiplexer (similar to tmux or screen) but includes many built-in features that would allow users to extend it and create their own personalized environment.

So, if you're looking for a modern screen or tmux replacement look no further.

# Installation
To get the latest version, it is best to install directly from cargo and in order to do so on Fedora Linux, we need to install some dependencies.  

1. First, install cargo using [rustup](https://rustup.rs):
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
2. Then, install development dependencies using dnf:
```bash
sudo dnf group install c-development development-tools
```
3. In order to build *zellij* from cargo, we also need two perl libraries:
```bash
sudo dnf install perl-FindBin perl-IPC-Cmd
```
4. Finnaly:
```bash
cargo install --locked zellij
```

Now grab a cup of cofee ☕️ and wait while it builds.

# Conclusion
I hope that you find this short post usefull. Happy hacking! 👩‍💻

