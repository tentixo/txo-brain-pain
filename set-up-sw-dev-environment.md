# Set Up Software Development Environment

<!-- TOC -->
* [Set Up Software Development Environment](#set-up-software-development-environment)
  * [Reference Pictures](#reference-pictures)
    * [GitHub](#github)
      * [Code tab](#code-tab-)
      * [How to create a new branch](#how-to-create-a-new-branch-)
      * [How to clone the repository](#how-to-clone-the-repository-)
    * [Pycharm](#pycharm)
  * [Mac](#mac)
  * [What is Homebrew?](#what-is-homebrew)
  * [Step-by-step guide](#step-by-step-guide)
    * [0. Prerequisite](#0-prerequisite)
    * [1. Install Xcode (and Command Line Tools)](#1-install-xcode-and-command-line-tools)
    * [2. Install Homebrew](#2-install-homebrew)
      * [Brew Installation Directory](#brew-installation-directory)
    * [3. Install Packages from Brewfile](#3-install-packages-from-brewfile)
      * [Good Brew commands](#good-brew-commands)
      * [Brew packages to install](#brew-packages-to-install)
    * [4. Start using iTerm instead of Terminal](#4-start-using-iterm-instead-of-terminal)
    * [5. Install and activate Zsh (recommended)](#5-install-and-activate-zsh-recommended)
    * [6. Install Zsh helpers: Oh-my-Zsh,](#6-install-zsh-helpers-oh-my-zsh)
    * [7. Set up .zshrc and .zprofile config file](#7-set-up-zshrc-and-zprofile-config-file)
      * [Apple-based .zprofile](#apple-based-zprofile)
      * [Intel-based .zprofile](#intel-based-zprofile)
      * [Apple-based .zshrc](#apple-based-zshrc)
      * [Intel-based .zshrc](#intel-based-zshrc)
    * [8. Install & activate git and git-lfs](#8-install--activate-git-and-git-lfs)
    * [9. Create & install your default SSH key pair](#9-create--install-your-default-ssh-key-pair)
    * [10. Create a personal GitHub account and add your SSH public file](#10-create-a-personal-github-account-and-add-your-ssh-public-file)
    * [11. Create a GitHub repository in your personal profile](#11-create-a-github-repository-in-your-personal-profile)
    * [12. Install PyCharm and clone your repository](#12-install-pycharm-and-clone-your-repository)
    * [13. Create and download your first ticket branch on GitHub](#13-create-and-download-your-first-ticket-branch-on-github)
    * [14. Install your package and keep them updated](#14-install-your-package-and-keep-them-updated)
    * [15. Start coding!](#15-start-coding)
  * [Reference Material](#reference-material)
    * [Educational references](#educational-references)
      * [Homebrew installation](#homebrew-installation)
      * [Cask](#cask)
      * [Python and Pip install](#python-and-pip-install)
      * [Pycharm, Zsh, Virtual environments , JetBrains and ansible](#pycharm-zsh-virtual-environments--jetbrains-and-ansible)
      * [What is the Purpose of Installing and Activating Zsh?](#what-is-the-purpose-of-installing-and-activating-zsh)
      * [Advantages of using a virtual environment](#advantages-of-using-a-virtual-environment)
      * [Difference Between .zshrc and .zprofile](#difference-between-zshrc-and-zprofile)
      * [Git and GitHub](#git-and-github)
      * [Why Does Git Change CRLF to LF?](#why-does-git-change-crlf-to-lf)
      * [SSH keys and its uses](#ssh-keys-and-its-uses)
<!-- TOC -->

## Reference Pictures

### GitHub
#### Code tab  
![](img/GitHub-view.png)  
#### How to create a new branch  
![](img/GitHub-branch.png)  
#### How to clone the repository  
![](img/GitHub-clone.png)

### Pycharm
![](img/PyCharm-view.png)

## Mac

This guide helps you to set up installations with Mac's package handler Homebrew and work with Git+GitHub to save your
code.
It also shows you how to use GitHub with PyCharm on Mac. You’ll learn how to install the right tools, keep track of your
work, and organize your projects while collaborating with the team.

## What is Homebrew?

Read up about [Brew](https://brew.sh/) on its home page.  
Homebrew is a tool for Mac computers that helps you easily download and install the programs and tools (packages) you
need.  
Brew has two levels:

* `brew install`: Brews are low-level packages, mostly CLI-based for SwDev development, like Python versions.
* `brew install --cask`: Casks are normal UI click-and-use applications, like Google Chrome.

The reason to use a package handler is that instead of manually searching for and downloading software, you can use
simple commands to install everything quickly.
It’s like an automated app store, where you can you Terminal to get what you need.

## Step-by-step guide

### 0. Prerequisite

To be able to work as a developer on Mac, you need the basic tools that will help you work with and build your software.
This includes among other things compilers and build tools. Apple bundles these in a developer package.

### 1. Install Xcode (and Command Line Tools)

1. Go to [Apple Developer](https://developer.apple.com/download/applications/) website.
2. Use your Apple/iCloud account and sign-up/sign-in.
3. Download the latest version of Xcode, and if you are on an Intel-based Mac, Xcode Command Line Tools.
4. Install. It will take a while...

### 2. Install Homebrew

1. Open Terminal by searching for `Terminal` in Spotlight (shortcut: `Cmd + Space`) or by using Finder and in the left
   pane select Applications/Utilities/Terminal.
2. Copy the commands below into Terminal and press Return.
   * `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" `
3. Verify the installation with `brew --version`.
4. Make sure everything is updated with `brew update`

#### Brew Installation Directory

Brew is using different directories for Intel-based and Apple-based Macs.  
Remember this information-you will need it for setting up `.zshrc` and `.zprofile`, Python interpreter in PyCharm and
more.

* Intel: `/usr/local/`
* Apple: `/opt/homebrew/`
* Apple's own installation directory: `/bin`

### 3. Install Packages from Brewfile

For a rapid installation, you should create a file with the packages you want to install, a Brewfile.  
Below are recommended packages for a work as a developer and Dirt Remover.
We are going to use `vi` as text editor, see its commands [here](https://www.cs.colostate.edu/helpdocs/vi.html).

1. Create a `Brewfile` in your home directory
   1. Open Terminal.
   2. Make sure you are in your home directory with `cd` + Return.
   3. Create a Brewfile with `vi` - the horrible text editor with `vi Brewfile` + Return.
      1. Copy the Brewfile content below.
      2. Press `i` for insert.
      3. Past the content.
      4. Press `Esc` to get out of Insert mode
      5. Press `:x` so save your file.
         * To exit without saving: `:q!`
2. Check your Brewfile with `brew bundle check`.
3. Install the content of your `Brewfile` bundle with `brew bundle install` + Return.
4. If you want to install additional packages you can create a named file and install its content with `brew bundle
   --file=~/path/to/additional-packages`

#### Good Brew commands

* `brew install <package_name>`: Manually install another package found on
  the [Brew website](https://formulae.brew.sh/):
* `brew update`: Update the repositories
* `brew upgrade`: Upgrade only Brews
* `brew upgrade --greedy`: Upgrade Brews and Casks:
* `brew cleanup`: Remove older versions:

#### Brew packages to install

`Brewfile` - our recommended Brews and Casks

```text
tap 'homebrew/bundle'
tap 'homebrew/services'

brew 'awscli'
brew 'azure-cli'
brew 'dive'  # Tool for exploring each layer in a docker image
brew 'docker'
brew 'docker-completion'
brew 'git'
brew 'git-lfs'
brew 'mas'  # Mac App Store CLI
brew 'postgresql@16'
brew 'python@3.13'
brew 'uv'
brew 'wireshark'
brew 'xz'  # General-purpose data compression with high compression ratio
brew 'yubikey-agent'
brew 'zsh'
brew 'zsh-completions'
brew 'zsh-autosuggestions'
brew 'zsh-syntax-highlighting'

cask '1password'
cask '1password-cli'
cask 'chatgpt'  # Only for Apple-based Mac
cask 'couchbase-server-enterprise'
cask 'cyberduck'  # FTP client
cask 'discord'
cask 'firefox'
cask 'google-chrome'
cask 'google-drive'
cask 'gpg-suite'
cask 'intune-company-portal'
cask 'iterm2'
cask 'jetbrains-toolbox'
cask 'omnigraffle'
cask 'omnidisksweeper'
cask 'omnioutliner'
cask 'omniplan'
cask 'omnipresence'
cask 'postman'
cask 'powershell'
cask 'signal'
cask 'slack'
cask 'sourcetree'
cask 'virtualbox'
cask 'visual-studio-code'
cask 'windows-app'
cask 'yubico-yubikey-manager'
cask 'yubico-authenticator'
cask 'zoom'
```

`additional-packages` - These might be good to add. Add if needed to Brewfile or manually install.

```text
tap 'homebrew/bundle'
tap 'homebrew/services'

brew 'icu4c@77'  # CLDR for multi-culture (m10e) development
brew 'gradle'  # Advance build tool for Java
brew 'maven'  # Basic, simple-to-use build tool for Java
brew 'openjdk'  # Java development kit
cask 'logitune'  # If you have Logitech hardware
cask 'tunnelblick'  # OpenVPN client for Mac
cask 'zoc'  # SSH Client and Terminal Emulator
```

### 4. Start using iTerm instead of Terminal

1. Go to Finder/Applications or search via Spotlight (Command + Space) for iTerm.
2. Start iTerm.
3. Find the iTerm icon in the Dock to the right.
4. Right-click on the icon and choose Options/Keep in Dock.
5. Move the icon to a good place in the Dock by dragging it.
6. Remove the Terminal icon fron the dock by dragging it up and away from the Dock.
7. When needing to work with CLI, click on the iTerm icon in the Dock.

### 5. Install and activate Zsh (recommended)

Zsh is the default shell on macOS, but you may need to ensure it’s active and configure it for better productivity.

1. If not done, install Zsh via Homebrew (It is included in above Brewfile): `brew install zsh`
   * Sadly, we cannot link the Brew shell to Mac without magic, so until later, choose the first option under 2.
2. Start iTerm.
3. In the Mac menu, choose iTerm2/Settings... and set the following settings:
   * Profiles
      * General
        * Command:Login Shell: `/bin/zsh`
      * Window
        * New windows: `160` columns by `50` rows (or larger)
      * Terminal
        * Character encoding: Unicode (UTF-8)
        * Environment: Use custom locale..., click Change... and set English (United States), UTF-8
          * Value shown below: `LANG=en_US.UTF-8`
4. Close the Settings window.
5. In a iTerm window, verify Zsh is active with command: `echo $SHELL`
   * Output: `/bin/zsh`
6. Tips: If you want more then one window, create a new tab with Command + T
   * Change between tabs by Command + <no.> or click in the top frame.

### 6. Install Zsh helpers: Oh-my-Zsh,

[Oh-my-Zsh](https://ohmyz.sh/) home page.

1. Run the installation script.
   * `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
2. The script manipulates your config Zsh files, so check out the settings:
   * `cat ~/.zshrc`
   * `cat ~/.zprofile`
3. If not done, install helper files (they are included in above Brewfile):
   * `brew install zsh-completions zsh-autosuggestions zsh-syntax-highlighting`

### 7. Set up .zshrc and .zprofile config file

To control Zsh's behavior there are five different file types, that can be both centrally stored `/etc` and in your home
directory `~`.  
There are five file types, listed in the order → of read by Zsh when you start your iTerm/Terminal session:

1. `zshenv`
2. `zprofile`
3. `zshrc`
4. `zlogin`
5. `zlogout`

But the two that are important for "daily geeking" are `zprofile` → `zshrc`, and we will only use home directory
storage, where we add a dot `.` prefix to hide them.
To simplify why we have these to files, we can say:

* `.zprofile`: Settings/variables for humans and scripts, i.e. for everything, for example:
   * PATH
   * EDITOR
* `.zshrc`: Settings for what humans need, for example:
   * prompt
   * command completion, correction, suggestion, highlighting
   * output coloring
   * aliases
   * key bindings
   * command history management

Below are recommended settings for each file for Apple vs. Intel Macs.

**Note**: Remove Java PATHs if you are not using it

#### Apple-based .zprofile

```text
# ~/.zprofile

# Initialize Homebrew environment
eval "$(/opt/homebrew/bin/brew shellenv)"

# Language and locale settings
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8

# Set JAVA_HOME for Homebrew-managed OpenJDK
export JAVA_HOME="/opt/homebrew/opt/openjdk"

# Set PATH: prioritize Homebrew, Python, OpenJDK, JetBrains Toolbox
export PATH="/opt/homebrew/opt/openjdk/bin:/opt/homebrew/opt/python@3.13/bin:/opt/homebrew/bin:/opt/homebrew/sbin:$PATH"
export PATH="$PATH:$HOME/Library/Application Support/JetBrains/Toolbox/scripts"
```

#### Intel-based .zprofile

```text
# ~/.zprofile

# Initialize Homebrew environment (Intel Macs use /usr/local)
eval "$(/usr/local/bin/brew shellenv)"

# Language and locale settings
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8

# Set JAVA_HOME for Homebrew-managed OpenJDK
export JAVA_HOME="/usr/local/opt/openjdk"

# Set PATH: prioritize OpenJDK, Python, Homebrew, JetBrains Toolbox
export PATH="/usr/local/opt/openjdk/bin:/usr/local/opt/python@3.13/bin:/usr/local/bin:/usr/local/sbin:$PATH"
export PATH="$PATH:$HOME/Library/Application Support/JetBrains/Toolbox/scripts"
```

#### Apple-based .zshrc

```text
# ~/.zshrc

# Add zsh completions
fpath=(/opt/homebrew/share/zsh-completions $fpath)

# Oh My Zsh setup
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME="robbyrussell"  # Change to your preferred theme
plugins=(git python docker brew postgres aws)  # Add/remove plugins as needed
source $ZSH/oh-my-zsh.sh

# Aliases for convenience
alias pycharm="open -a PyCharm"
alias venvactivate="source venv/bin/activate"
alias python='python3'
alias pip='uv pip'

# Shell Options
setopt autocd              # Automatically change to a directory without typing 'cd'
setopt correct             # Correct mistyped commands
setopt hist_ignore_dups    # Ignore duplicate commands in history

# History Configuration
HISTFILE=$HOME/.zsh_history
HISTSIZE=10000
SAVEHIST=10000
HIST_STAMPS="yyyy-mm-dd"

setopt appendhistory       # Append to history file instead of overwriting
setopt incappendhistory    # Add commands to history immediately
setopt sharehistory        # Share command history between all sessions
setopt hist_ignore_all_dups  # Remove duplicate commands from history
setopt hist_reduce_blanks    # Strip excess whitespace

# Enable auto-suggestions and syntax highlighting (if installed)
source /opt/homebrew/share/zsh-autosuggestions/zsh-autosuggestions.zsh
source /opt/homebrew/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

# Custom Functions (optional)
# function my_custom_function() {
#   echo "This is a custom function"
# }
```

#### Intel-based .zshrc

```text
# ~/.zshrc

# Add zsh completions
fpath=(/usr/local/share/zsh-completions $fpath)

# Oh My Zsh setup
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME="robbyrussell"  # Change to your preferred theme
plugins=(git python docker brew postgres aws)
source $ZSH/oh-my-zsh.sh

# Aliases for convenience
alias pycharm="open -a PyCharm"
alias venvactivate="source venv/bin/activate"
alias python='python3'
alias pip='uv pip'

# Shell Options
setopt autocd              # Automatically change to a directory without typing 'cd'
setopt correct             # Correct mistyped commands
setopt hist_ignore_dups    # Ignore duplicate commands in history

# History Configuration
HISTFILE=$HOME/.zsh_history
HISTSIZE=10000
SAVEHIST=10000
HIST_STAMPS="yyyy-mm-dd"

setopt appendhistory       # Append to history file instead of overwriting
setopt incappendhistory    # Add commands to history immediately
setopt sharehistory        # Share command history between all sessions
setopt hist_ignore_all_dups  # Remove duplicate commands from history
setopt hist_reduce_blanks    # Strip excess whitespace

# Enable auto-suggestions and syntax highlighting (if installed)
source /usr/local/share/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

# Custom Functions (optional)
# function my_custom_function() {
#   echo "This is a custom function"
# }
```

### 8. Install & activate git and git-lfs

1. Install git and git-lfs with `brew install git git-lfs`, if not already done via Brewfile
   Git LFS: Large File Support is used to avoid bloating your repo with non-compressible "fat" digital files.
2. Validate your installation
   * `git --version`
   * `git lfs --version`
3. Set up your global git parameters
   * `git config --global user.name "<Firstname Lastname>"`
   * `git config --global user.email "<login_name>@example.com"`
   * Mac: `git config --global core.autocrlf input`  # Git leaves LF untouched
   * Win: `git config --global core.autocrlf false`  # Git converts CRLF to LF on check-in, and LF back to CRLF on
     checkout
4. Verify your settings: `git config --global --list`
5. Activate Git LFS globally in your workstation with `git lfs install`.  
   **Note**: What files that Git LFS will handle will be set by a `.gitattributes` file in each repository  
   (see below), so your digital files is not handled by Git (Git only works on text files).

### 9. Create & install your default SSH key pair

1. Start a terminal session. (Open iTerm)
   **Note**: You shoule now be in your home directory. If unsure or using an old terminal session hit `cd`.
2. Adapt the settings for your email and preferred name for your ssh key, then generate a new SSH key with:
   **Note**: Use your email and use a good "nick" for your filename so you find it easily
    ```text
    ssh-keygen -o -a 100 -t ed25519 -C “name@example.com" -f ~/.ssh/name_default`
    ``` 
   where:
   * **-t ed25519**: Specifies the key type (modern and secure).
   * **-a 100**: Adds additional computational cost for better security.
   * **-C "name@example.com"**: Provides an identifier for your key.
   * **-f ~/.ssh/name_default**: Specifies the filename to save the key at the correct place in your home directory.  
     **Note**: The command will create a secret file, without suffix and a public file with suffix `.pub`.  
     Your secret file should **never** be shared and only copied to your 1Password. Make sure to always add your public
     part to services.
3. Follow the prompts to save the key (press Enter to save in the default location-your home dir `.ssh/`)
4. Create an SSH config file named `config`, so your applications like PyCharm, will be using your default SSH key.   
   Note: Change the name of the file in the config to your chosen name!  
   **Mac: .ssh/config**
   ```text
   Host *
     UseKeychain yes
     AddKeysToAgent yes
     IdentityFile ~/.ssh/name_default
   ```
   **Win: .ssh/config**
   ```text
   Host *
     UseKeychain yes
     IdentityFile ~/.ssh/name_default
   ```
5. Start and add the SSH **secret** key to the SSH agent:    
   `eval "$(ssh-agent -s)"`
   `ssh-add -K ~/.ssh/name_default`

### 10. Create a personal GitHub account and add your SSH public file

1. Go to [GitHub](https://github.com/join) and click Sign Up (This will be your private account)
   * Do not use your any company email account-use your personal, like `name@gmail.com`.
2. Follow the prompts to create an account with your email and username.
3. Verify your account via email.
4. **Set up MFA!**
5. Add your public SSH key part to your user profile.
   1. Copy the SSH public key to your clipboard:
      * Mac: `pbcopy < ~/.ssh/name_default.pub`
      * Win: `clip < ~/.ssh/name_default.pub`
   2. Go to your GitHub account Settings → SSH and GPG keys → click New SSH Key
   3. Paste the SSH key and click add SSH key
   4. Test SSH connection `ssh -T git@github.com`      
      If the SSH key is set up correctly and added to your GitHub account, you will see a message similar to:    
      *Hi <your_username>! You've successfully authenticated, but GitHub does not provide shell access.*

### 11. Create a GitHub repository in your personal profile

1. Create a repository and **only** add a `README.md`
   1. Log in to GitHub
   2. Click the + icon in the top-right corner
   3. Select New repository
   4. Enter a repository name
      in [kebab-case](https://medium.com/@kamlesh90/snake-case-vs-camel-case-vs-pascal-case-vs-kebab-case-understanding-the-differences-a23cb3d4ac67),
      like `miffo-first-repo`)
   5. Choose the visibility:
      * Public: Anyone can see it ← use this one to avoid costs
      * Private: Only you (and invited collaborators) can access it (€€€)
   6. Add a **only** a README file
   7. Click Create repository
2. Branch from main/master branch and create a `develop` branch.
   1. Click on `main` icon.
   2. In the Switch branches/tags field write `develop`.
   3. Click "Create `develop` from `main`"

### 12. Install PyCharm and clone your repository

1. Create a folder in your home directory called `PycharmProjects`.
2. Install PyCharm via the app JetBrains Toolbox.
   * If not delivered via you Brewfile: `brew install --cask jetbrains-toolbox`
3. Install plugins for .gitignore and .gitattributes.
   1. Choose menu PyCharm/Settings...
   2. In the left pane, choose Plugins
   3. In the middle area, choose Marketplace
   4. Search for and click the Install button after selection for
      * .gitignore
      * .gitattributes
      * mermaind
   5. If needed, Restart PyCharm
4. Clone the created repository from step 10.
   1. On GitHub, select your repository and click the gree Code button.
   2. Select SSH tab.
   3. Copy the URI for your repository, looks like `git@github.com:my-name/miffo-first-repo`
   4. Go back to PyCharm.
   5. Choose menu File/Project from Version Control...
   6. Fill in the data from GitHug
      * URL: `git@github.com:my-name/miffo-first-repo` ← Pasted from above
      * Directory: `/Users/my-user/PycharmProjects/miffo-first-repo` ← Make sure it is saved in your PycharmProjects
        dir.
   7. Click Clone.
   8. What a while. If the first time cloning:
      1. If prompted, select SSH Key Authentication.
      2. If this is your first time, allow PyCharm to use SSH Agent.
      3. Wait for the cloning process to complete.
      4. Once cloned, PyCharm will open the project.
   9. Open in New window and Trust Project
5. Change branch from `main` to the `develop`.
   1. Up to the left in your PyCharm window, find the git symbol with `main` after.
   2. Click the dropdown and select Remote/origin/develop/Checkout
6. Create a .gitignore file in your project root (require plugin install, see point 3. above).
   1. Right-click on your project root folder (the repository name on top).
   2. Select New/.gitignore File/.gitignore File (Git)
   3. Select the necessary templates
      * Always
         * Languages, frameworks
            - [x] Python
         * Global templates (OS, IDE…)
            - [x] JetBrains
            - [x] VirtualEnv
            - [x] VisualStudioCode
            - [x] Windows
            - [x] macOS
      * If needed
         * Global templates (OS, IDE…)
            - [ ] Ansible
            - [ ] Xcode
            - [ ] Vagrant
         * Toptal templates
            - [ ] PowerShell
   4. Click Create
   5. Add it to Git. (Normally PyCharm asks.)
   6. Open the `.gitignore` file and add the following lines to protect secrets files according to our naming standard:
      ```text
      ### Txo template
      # Protect secrets
      *-secrets.*
      *_vault.*
      ```
7. Create a `.gitattributes` file in project root and paste the content below.
   1. Right-click on your project root folder (the repository name on top).
   2. Select New/File
   3. Add it to Git. (Normally PyCharm asks.)
   4. Name it `.gitattributes`.
   5. Paste this content to `.gitattributes` as a good start, but remember to add you necessary binary file suffix.
      ```text
      # Images
      *.png filter=lfs diff=lfs merge=lfs -text
      *.jpg filter=lfs diff=lfs merge=lfs -text
      *.gif filter=lfs diff=lfs merge=lfs -text
   
      # Audio and Video
      *.mp3 filter=lfs diff=lfs merge=lfs -text
      *.mp4 filter=lfs diff=lfs merge=lfs -text
      *.avi filter=lfs diff=lfs merge=lfs -text
      *.mov filter=lfs diff=lfs merge=lfs -text
   
      # Compressed Archives
      *.zip filter=lfs diff=lfs merge=lfs -text
      *.tar.gz filter=lfs diff=lfs merge=lfs -text
      *.rar filter=lfs diff=lfs merge=lfs -text
   
      # Office Documents
      *.docx filter=lfs diff=lfs merge=lfs -text
      *.pptx filter=lfs diff=lfs merge=lfs -text
      *.xlsx filter=lfs diff=lfs merge=lfs -text
      *.pdf filter=lfs diff=lfs merge=lfs -text
      ```
   6. Tips: After adding "fat" files, you can validate LFS tracking with: `git lfs track`
8. Commit and Push your added files to `develop` branch
   1. In the left pane in PyCharm, click on Commit icon (normally second)
   2. Choose all files added to Git by selecting the group Changes.
   3. Write a commit message `Added .gitignore and.gitattributes`.
   4. In the bottom on the pane, click Commit and Push...
   5. Click Push. Now your `develop` branch is updated on GitHub.
9. Create a `uv` supported virtual environment (require `uv`, part of your Brewfile, if not installed, run:
   `brew install uv`
   1. Select menu PyCharm/Settings...
   2. In the left pane, select: Project: your_project_name/Python Interpreter
      1. Click the dropdown list next to the list of Python interpreters
      2. On the left side of Python Interpreter, Select Add Interpreter/Add Local Interpreter or Show All….depending on
         your version of PyCharm
         * Environment: Generate new
         * Type: uv
         * Base python: <copy your path to the latest python>, as example Python 3.13
            * Intel-based: `/usr/local/bin/python3.13`
            * Apple-based: `/opt/homebrew/bin/python3.13`
         * Path to uv:
            * Intel-based: `/usr/local/bin/uv`
            * Apple-based: `/opt/homebrew/bin/uv`
         * Click OK.
      3. Back in the first window, click OK.
   3. Validate that your PyCharm now has a Python interpreter and it is selected
      * Check in Project/files window that there is a `.venv` directory
      * I the bottom left of you PyCharm windows, check that you have a field with
        `uv (your_project_name) [Python 3.13.X]`
      * In the pane bottom left, click the Terminal symbol and run
         * `python --version` → Pyton 3.13.X
         * `which python` → ‘/Users/username/PycharmProjects/Your-Project-Name/venv/bin/python’
   4. From now on, you will never work directly in `develop` branch, just a "ticket branch" branched from `develop`

### 13. Create and download your first ticket branch on GitHub

1. GitHub: Crete a ticket branch from `develop`
   1. Click on the branches icon, often showing `main`, and select `develop` branch.
   2. In the Switch branches/tags field write `fixing-stuff`.
   3. Click "Create `fixing-stuff` from `develop`"
2. PyCharm: Download (fetch) your new ticket branch
   1. Open PyCharm
   2. In the menu, select Git/Update Project... and click OK.
      * Merge incoming changes to current branch
   3. Up in the left corner, click the branch dropdown, showing either `main` or `develop`.
   4. Scroll down and select Remote/origin/fixing-stuff/Checkout
   5. Validate that the branch selector now shows `fixing-stuff`
3. Start coding or create your Markdown files.

### 14. Install your package and keep them updated
1. In the left PyCharm frame, click on Terminal icon. 
2. Install packages via `pip install <package_name>`.
3. Validate and later update your packes under Python Package in the left frame.
4. Tips: Add to Git and check in these project file to help others install your project's needed packages:
   * pyproject.toml
   * uv.lock

### 15. Start coding!
Remember this:  
* Never directly commit/push anything to the primary branches `main` and `develop`, always use Pull Request with ticket 
  branch and code review. 
* Always create your ticket branch on GitHub from `develop`. Fetch it to PyCharm with Git/Update project...
* Documentation is a must!
  * Code comments and Docstrings-describing your code.
  * README.md: How to get the code to run.
  * Git wiki: Broader explanation about your code in the repo.
  * Project wiki: Needed if you have multi-repo project.
* If develop branch is way ahead of your ticket branch, rebase your ticket branch with develop as source.
* Always commit when you have working code! "I'm just going to..." is a terrible idea.

## Reference Material

### Educational references

#### Homebrew installation

Homebrew simplifies the installation of necessary tools such as Git, Python, and other dependencies. The Brewfile
simplifies tool management by bundling essential software installations into a single file. This guide covers the
creation and usage of a Brewfile for setting up a macOS development environment with PyCharm and Ansible.  
The installation script will ask you to confirm the installation. You may need to enter your `administrator password` (
one used to unlock your device) to continue.
The installation may also ask you to install the `Xcode Command Line Tools` if they are not already installed. This is a
necessary step because Homebrew requires these tools.
After installation, the script can automatically add Homebrew to your PATH.   
If it doesn't, you can add it manually by running the following command in terminal:  
```echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile eval "$(/opt/homebrew/bin/brew shellenv)"```  
These commands ensure that Homebrew is available in your terminal session.

#### Cask

A cask refers to a method for managing the installation of macOS applications that are distributed as binaries,
typically in .dmg, .pkg, or .app formats. Casks are used for software that can be compiled from source and needs to be
downloaded and installed as a pre-built package. When you install software via Homebrew Cask, it automates the process
of downloading, installing, and managing these types of macOS applications.

#### Python and Pip install

* Python is needed for development and pip helps install Python libraries and dependencies.

#### Pycharm, Zsh, Virtual environments , JetBrains and ansible

* PyCharm provides tools like code completion, debugging, Git integration, and more to streamline Python development.
* ~/PycharmProjects/ directory is like having a special box where you keep all your PyCharm projects. It helps you stay
  organized while working with Git and GitHub.
* Zsh - Apple has announced that in macOS 10.15 Catalina the default shell we be zsh. This does not say that bash is
  gone. Zsh is available Mojave and on older macOS versions. You can start testing zsh or even switch your default shell
  already. To see how it works just open a Terminal window and type ```zsh```. The reason Apple has not switched to
  these newer versions is that they are licensed with GPL v3. bash v3 is still GPL v2. If you are interested in depth
  about it see link: *Moving to Zsh*
* Zsh offers enhanced productivity features like autocompletion and Oh My Zsh further enhances the shell with plugins
  and themes.
* JetBrains toolbox is a collection of development tools and IDEs (Integrated Development Environments) which is a
  comprehensive collection of powerful and professional tools for developers, covering a wide range of programming
  languages and platforms. With tools like IntelliJ IDEA, PyCharm, WebStorm and many more, JetBrains Toolbox gives
  developers the tools they need to efficiently create high-quality software. JetBrain's Toolbox App makes managing
  these tools simple and centralized, improving productivity and facilitating work in complex development environments.
* Virtual environments help you manage dependencies and avoid conflicts between projects.
* Ansible is essential for automating tasks in your development workflow, such as managing environments and deployments.

#### What is the Purpose of Installing and Activating Zsh?

To talk to your computer, you need a special language—that’s called a shell.
Zsh (Z Shell) is smarter and faster version of the normal shell (which is called Bash). It helps you type commands more
easily, gives you improved suggestions and makes process quicker.

- Easier Typing – It autocompletes your commands if you type the initial of the command and press tab, similar to how
  your phone suggests words as you type a message.
- More Powerful – You can customize it with plugins to work faster.

#### Advantages of using a virtual environment

* Isolation: Each project can have its own versions of Python packages, avoiding conflicts between different projects.
* Ease of management: You can easily keep track of and update dependencies specific to one project without affecting
  others.
* Reproducibility: You can share your requirements.txt file with others, making it easy for them to install the same
  packages and versions you use in your virtual environment.

#### Difference Between .zshrc and .zprofile

Your computer is like a big playground and every time you open your playground (your terminal), you have different rules
for how things work.

**.zprofile** – The Playground Entrance Rules (One-Time Rules)

* Think of .zprofile as the rules you follow when you enter the playground for the first time.
* You only read these rules once when you step inside.
* Example: If the rule says, “You must wear sneakers to play,” you put on sneakers before you start playing.
* In the computer world, .zprofile sets things like where to find tools (PATH).

**.zshrc** – The Playground Game Rules (Every Time Rules)

* .zshrc is like the rules for every game you play inside the playground.
* Each time you start a new game (open a terminal tab), you read these rules again.
* Example: If the rule says, “Always start with a warm-up lap,” then every time you start a new game, you run a warm-up
  lap first.
* In the computer world, .zshrc is for shortcuts (aliases), colors, and fun settings.

**When to Use Each File**

| Feature                            | `.zprofile`       | `.zshrc`     |
|------------------------------------|-------------------|--------------|
| **Login Shell**                    | ✅ Yes             | ❌ No         |
| **Interactive Shell**              | ❌ No              | ✅ Yes        |
| **Runs on New Terminal Window**    | ✅ First time only | ✅ Every time |
| **Used for Environment Variables** | ✅ Yes             | ❌ No         |
| **Used for Aliases & Functions**   | ❌ No              | ✅ Yes        |

#### Git and GitHub

* Git lets you save different versions of your work on your own computer.
* GitHub is like an online bookshelf where you can store, share, and work on projects together with others from anywhere
  in the world!
* Git is a version control system that tracks changes in your codebase, allows you to manage version history and helps
  you collaborate with others. You will need Git to interact with GitHub repositories.
* Git allows you to push/pull code to and from GitHub.
* Proper Git configuration ensures that your commits are correctly attributed to you when using Git.
* Cloning a repository allows you to download and work on an existing project from GitHub.
* GitHub is a cloud-based platform for version control and collaboration, built on Git. It allows developers to store,
  track, and manage code changes efficiently.

Key Concepts - GitHub:

* Repository (Repo): A storage space for your project, containing files and version history.
* Commit: A saved change in a repository.
* Branch: A separate version of the code for development without affecting the main code. A branch is like having extra
  drawing sheets where you can test new ideas without messing up your original work.

- Safe Experiments – You can try new ideas without affecting the main drawing.
- Multiple People Can Work Together – Each person can work on their own branch without interfering.
- Merge When Ready – If the new idea looks great, you can combine it with the original drawing!

* Pull Request (PR): A request to merge changes from one branch to another.
* Merge: Combining code from different branches.
* Fork: Creating a copy of another user’s repository.
* Clone: Downloading a repository to your local machine.
* Issue: A way to report bugs, suggest features, or discuss changes.

Common Uses:

✅ Version control & code tracking  
✅ Team collaboration & code review  
✅ Open-source contributions

Basic Git Commands:

`git init`             # Initialize a new Git repository  
`git clone <repo>`     # Clone a GitHub repository  
`git add .`            # Add all changes to staging  
`git commit -m "msg"`  # Save changes with a message  
`git push origin main` # Upload changes to GitHub  
`git pull origin main` # Get latest changes from GitHub

Why Use GitHub?  
✅ Backup & version history  
✅ Collaboration & code review  
✅ Integration with CI/CD & DevOps tools

#### Why Does Git Change CRLF to LF?

- When you save a file on Windows, it may use CRLF. When you share that file with someone using Mac or Linux, Git
  automatically changes it to LF so it looks right on their system as CRLF is used on windows and not Mac/Linux.
- Problem: If Git changes it without asking, sometimes it breaks your code or makes it look different than you expected.

#### SSH keys and its uses

- SSH (Secure Shell) is a way for one computer to safely connect to another computer over the internet. It’s like a
  secure tunnel that keeps your information private and safe from hackers.
- Secure Communication – No one can eavesdrop on your commands.
- No Need for Passwords Every Time – It uses keys instead of typing a password every time.
- Safe File Transfers – You can move files between computers safely.
- Works Anywhere – **You can control your computer remotely from another device. Hence its important to keep it safe.**
