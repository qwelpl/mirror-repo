# mirror-repo

CLI tool to create paired GitLab + GitHub repos with push mirroring.

Run one command → get a private GitLab repo, a matching GitHub repo, and a push mirror that keeps them in sync automatically.

## Installation

### macOS

```sh
brew install qwelpl/tap/mirror-repo
```

Requires [Homebrew](https://brew.sh). `curl` and `jq` are installed automatically.

### Windows

mirror-repo is a bash script and requires a bash environment on Windows.

**Option A — WSL (recommended)**

1. [Install WSL](https://learn.microsoft.com/en-us/windows/wsl/install) (Ubuntu is fine)
2. Inside WSL:

```sh
sudo apt install -y curl jq
curl -fsSL https://raw.githubusercontent.com/qwelpl/mirror-repo/main/mirror-repo \
  -o ~/.local/bin/mirror-repo
chmod +x ~/.local/bin/mirror-repo
```

**Option B — Git Bash**

1. Install [Git for Windows](https://git-scm.com/download/win) (includes Git Bash)
2. Install [jq for Windows](https://jqlang.github.io/jq/download/) and add it to your PATH
3. In Git Bash:

```sh
curl -fsSL https://raw.githubusercontent.com/qwelpl/mirror-repo/main/mirror-repo \
  -o ~/bin/mirror-repo
chmod +x ~/bin/mirror-repo
```

## Setup

Run once to save your tokens:

```sh
mirror-repo setup
```

You'll need:
- A GitLab Personal Access Token with `api` scope — [generate here](https://gitlab.com/-/user_settings/personal_access_tokens)
- A GitHub Personal Access Token (classic) with `repo` scope — [generate here](https://github.com/settings/tokens)

## Usage

```sh
mirror-repo <repo-name>                   # create private repo pair
mirror-repo --public <repo-name>          # create public repo pair
mirror-repo --desc "My project" <name>    # set description
mirror-repo --keep-readme <repo-name>     # skip README deletion
mirror-repo help                          # show all options
```

## How it works

1. Creates a repo on GitLab (with README, then removes it)
2. Creates an empty repo on GitHub
3. Configures GitLab push mirroring to GitHub

Every `git push` to GitLab automatically syncs to GitHub. GitLab is the source of truth.
