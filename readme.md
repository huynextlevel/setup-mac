## Setup Mac

#### Automatically install environment and development tools for your machine.

### Prerequisites
1. Apple command line tools — run `xcode-select --install`.
2. [Homebrew](https://brew.sh/) — run `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`.
3. [Ansible](https://formulae.brew.sh/formula/ansible) — run `brew install ansible`.

### Installation
1. Clone this repo: `git clone https://github.com/huynextlevel/setup-mac`
2. Run `ansible-playbook -i hosts.yml ansible.yml`

The playbook will prompt for your sudo password once at the start (handled via `vars_prompt` in `ansible/initialize.yml`); no need to pass `--ask-become-pass`.

### Optional: setup MacBook as a local server
Run this only when you want to turn a machine into a local server (prevent sleep on lid close, enable SSH, install + configure Tailscale). It is **not** part of the main flow — invoke it manually when needed:

```bash
ansible-playbook -i hosts.yml ansible/server.yml
```

Notes:
- **Heat**: a closed-lid machine that keeps running will accumulate heat — place it on a ventilated stand.
- **FileVault**: if enabled, after reboot the machine is stuck at the unlock screen and SSH is unreachable until manually unlocked. Consider disabling it on a server-only machine.
- **Tailscale key expiry**: disable it in the admin console, otherwise the machine will disconnect after ~180 days.
- The first time Tailscale runs, it requires auth — the playbook prints a `sudo tailscale up ...` command. Run that, log in via browser, then re-run the playbook to verify.

### What gets installed

#### Folders
- `~/Sources`
- `~/Projects`

#### Homebrew packages
- `git`
- `openssl`
- `pnpm`

#### Shell environment
- `zsh` set as the default shell
- `oh-my-zsh` cloned to `~/Sources/oh-my-zsh` (symlinked from `~/.oh-my-zsh`)
- Plugins: `zsh-autosuggestions`, `zsh-syntax-highlighting`
- Theme: [Powerlevel10k](https://github.com/romkatv/powerlevel10k) cloned to `~/powerlevel10k`
- Fonts: `MesloLGS NF` (Regular / Bold / Italic / Bold Italic) installed to `~/Library/Fonts/` — required for p10k icons. Set this as the font in your terminal (iTerm2 → Preferences → Profiles → Text → Font).
- Static configs deployed to home: `~/.zshrc`, `~/.p10k.zsh`
- Homebrew `shellenv` appended to `~/.zshrc`

#### Node toolchain
- `nvm` v0.40.4 installed to `~/.nvm`
- Node `20.19.4` installed via nvm and set as default
- `eas-cli` installed globally via npm

#### React Native (`ansible/react-native.yml`)
- `watchman`
- `cocoapods`
- `zulu@17` (OpenJDK 17 cask)
- `JAVA_HOME`, `ANDROID_HOME`, and Android `emulator` / `platform-tools` PATH entries appended to `~/.zshrc`

#### Local server (`ansible/server.yml`, opt-in)
- `pmset` settings: disable sleep / disk sleep / Power Nap, enable Wake-on-LAN, auto-restart on power failure
- `systemsetup -setremotelogin on` (SSH)
- `tailscale-app` cask
