# clip.exe

## Setup

***********************************************TODO***************************************************************

- make docker-build
- Load browser:
  - https://stuartleeks.com/posts/vscode-devcontainer-clipboard-forwarding/#launching-the-socat-listener
  - https://wsl.tips/book 😉
  - https://stuartleeks.com/posts/vscode-devcontainer-clipboard-forwarding/
  - https://code.visualstudio.com/docs/remote/remote-overview
  - https://code.visualstudio.com/docs/remote/containers


## Flow

### Windows/WSL

```bash
# In PowerShell:

echo hi |clip
# Ctrl + V

# up arrow + tab:
echo hi | clip.exe


# Repeat the above in WSL (pause on tab completion!)
# Calling Windows binary from WSL!

# simple replacement for xclip in WSL 
cat ./wsl/xclip.sh
alias xclip=$PWD/wsl/xclip.sh
echo -n Hello | xclip
```

### Containers

```bash

# Split terminal to run host + container side-by-side
make docker-run

# host:
socat tcp-listen:8221,fork,bind=0.0.0.0 EXEC:'clip.exe'

# container
ping host.docker.internal # resolves to Windows host (but WSL forwards to WSL!)
echo "hello from a container" | socat - tcp:host.docker.internal:8221

cat ./xclip.sh
alias xlcip=/demo/xclip.sh
echo "hello from a container" | xclip

```

### Going further

- Setup listener automatically
  - https://stuartleeks.com/posts/vscode-devcontainer-clipboard-forwarding/#launching-the-socat-listener
- Setup xclip automatically
  - dotfiles!
    - my main scenario for this is VS Code Dev Containers
    - overview of remote (WSL/SSH/Containers)
    - cool feature: clone + load dotfiles
  - 
