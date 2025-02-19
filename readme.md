## Setup Mac

#### Automatically install environment, development tools for your machine.

### Prerequisites:
1. Ensure Apple's command line tools are installed (xcode-select --install to launch the installer).
2. [Install Homebrew](https://brew.sh/). run `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`.
2. [Install Ansible](https://formulae.brew.sh/formula/ansible). run `brew install ansible`.

### Installation
1. Clone this repo to your local drive `git clone https://github.com/huynextlevel/setup-mac`
2. Run `ansible-playbook -i hosts.yml ansible.yml --ask-become-pass`

### Software list:
List of tools that will be install by Ansible..

#### Create folder
- [x] ~/Sources
- [x] ~/Projects

#### Essentials tools
- [x] Git
- [x] openssl
- [x] Terraform (super lightweight DevOps resource automation)
- [x] zsh (use as default shell), oh-my-zsh (~/Source/oh-my-zsh)
- [x] spaceship-operator-mono theme for Zsh
- [x] plugins for Zsh: suggestions, syntax highlighting, nvm

#### Developer tools
- [x] nvm (node version manager)
- [x] nodejs@20.15.0 (using `nvm`)
- [x] yarn (yet another node.js package manager)
- [ ] rvm (ruby version manager)

#### React Native tools
- [x] watchman
- [x] CocoaPods, we'll need to run `pod install cocoapods` on our own (it take too long time to run, so I don't think we want to have it installed by Ansible)

#### Other software that you may interest with (paid, not in scope of this Repo)k
