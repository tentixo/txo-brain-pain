# Mac: SwDev environment set up for Python, PyCharm, Git and GitHub

This guide helps you to set up installations with Mac's package handler Homebrew and work with Git+GitHub to save your code. 
It also shows you how to use GitHub with PyCharm on Mac. You’ll learn how to install the right tools, keep track of your work, and organize your projects while collaborating with the team.  

## What is Homebrew?
Homebrew is a tool for Mac computers that helps you easily download and install the programs and tools (packages) you need. 
Instead of manually searching for and downloading software, you can use simple commands to install everything quickly. 
It’s like an automated app store, where you can you Terminal to get what you need.  

## Step-by-step guide

### Prerequisite
To be able to work as a developer on Mac, you need the basic tools that will help you work with and build your software.
This includes among other things compilers and build tools. Apple bundles these in a developer package.

### 1. Install Xcode (and Command Line Tools)
1. Go to [Apple Developer](https://developer.apple.com/download/applications/) website. 
2. Use your Apple/iCloud account and sign-up/sign-in.
3. Download the latest version of Xcode, and if you are on an Intel-based Mac, Xcode Command Line Tools.
4. Install. It will take a while...

### 2. Install Homebrew
[Brew](https://brew.sh/) home page.
1. Open Terminal by searching for `Terminal` in Spotlight (shortcut: `Cmd + Space`) or by using Finder and in the left pane
select Applications/Utilities/Terminal.  
2. Copy the commands below into Terminal and press Return.
   * `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" `
3. Verify the installation with `brew --version`.  
4. Make sure everything is updated with `brew update`

**Note**: Brew is using different directories for Intel-based and Apple-based Macs.  
Intel: `/usr/local/`  
Apple: `/opt/homebrew/`  
and this must be taken into account when extending your `.zshrc` and `.zprofile` configurations.

### 3. Install packages w/ Brewfile
For a rapid installation, you should create a file with the packages you want to install-a Brewfile.  
Below are recommended packages for a work as a developer and Dirt Remover.
1. Create a `Brewfile` in your home directory
   1. Open Terminal.
   2. Make sure you are in your home directory with `cd` + Return.
   3. Create a Brewfile with `vi` - the horrible text editor with `vi Brewfile` + Return
      1. Copy the Brewfile content below.
      2. Press `i` for insert.
      3. Past the content.
      4. Press `Esc` to get out of insert mode
      5. Press `:x` so save your file. 
      * To exit without saving: `:q!`
      * More `vi` commands [here](https://www.cs.colostate.edu/helpdocs/vi.html)
2. Install your bundle with `brew bundle install` + Return.
3. To handle Brew and update your packages in the future, use these commands:
   * Manually install another package found on the [Brew website](https://formulae.brew.sh/): `brew install <package_name>`
   * Update the repositories: `brew update`
   * Upgrade only brews: `brew upgrade`
   * Upgrade brews and casks: `brew upgrade --greedy`
   * Remove older versions: `brew cleanup`

#### Brewfile content
```text
tap 'homebrew/bundle'
tap 'homebrew/services'

brew 'awscli'
brew 'azure-cli'
brew 'dive'  # Tool for exploring each layer in a docker image
brew 'docker'
brew 'docker-completion'
brew 'icu4c@77'
brew 'git'
brew 'git-lfs'
brew 'gradle'
brew 'maven'
brew 'mas'  # Mac App Store CLI
brew 'openjdk'
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
cask 'logitune'
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
cask 'tunnelblick'
cask 'virtualbox'
cask 'visual-studio-code'
cask 'windows-app'
cask 'yubico-yubikey-manager'
cask 'yubico-authenticator'
cask 'zoc'
cask 'zoom'
```

### 4. Install and activate Zsh (recommended)    
Zsh is the default shell on macOS, but you may need to ensure it’s active and configure it for better productivity.  
1. If not done, install Zsh via Homebrew (It is included in above Brewfile): `brew install zsh`
   * Sadly, we cannot link the Brew shell to Mac without magic, so until later, choose the first option under 2.
2. Set Zsh as your default shell:  
   * Mac standard: `chsh -s /bin/zsh` <- Only this works for now
   * Intel-based: `chsh -s /usr/local/bin/zsh`
   * Apple-based: `chsh -s /opt/homebrew/bin/zsh`
3. Verify Zsh is active: `echo $SHELL`  
   * This should output `/bin/zsh` 

### 5. Install Zsh helpers: Oh-my-Zsh, 
[Oh-my-Zsh](https://ohmyz.sh/) home page.
1. Run the installation script.  
   * `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
2. The script manipulates your config Zsh files, so check out the settings: 
   * `cat ~/.zshrc`
   * `cat ~/.zprofile`
3. If not done, install helper files (they are included in above Brewfile):  
   * `brew install zsh-completions zsh-autosuggestions zsh-syntax-highlighting`  
Now you are ready to fix you Zsh config files. 

### 6. Set up .zshrc and .zprofile config file
To control Zsh's behavior there are five different file types, that can be both centrally stored `/etc` and in your home directory `~`.  
There are five file types, listed in the order → of read by Zsh when you start your iTerm/Terminal session:  
* `zshenv` →
* `zprofile` →
* `zshrc` →
* `zlogin` →
* `zlogout`

But the two that are important for "daily geeking" are `zprofile` → `zshrc`, and we will only use home directory 
storage, where we add a dot `.` prefix.
To simplify why we have these to files, we can say:  
* `.zprofile`: Settings/variables for humans and scripts, i.e. for everything for example:
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

### 7. Install & activate git and git-lfs
1. Install git and git-lfs: `brew install git git-lfs`
   Git LFS: Large File Support is used to avoid bloating your repo with non-compressible "fat" digital files.
2. Validate your installation
   * `git --version` 
   * `git lfs --version` 
3. Set up your global git parameters  
   * `git config --global user.name "<Firstname Lastname>"`
   * `git config --global user.email "<login_name>@example.com"` 
   * Mac: `git config --global core.autocrlf input`  # Git leaves LF untouched
   * Win: `git config --global core.autocrlf false`  # Git converts CRLF to LF on check-in, and LF back to CRLF on checkout
4. Verify your settings: `git config --global --list` 
5. Activate Git LFS globally in your workstation with `git lfs install`.  
   **Note**: What files that Git LFS will handle will be set by a `.gitattributes` file in each repository/project   
   (see below), so your digital files is not handled by Git (Git only works on text files).

### 8. Create & install your default SSH key pair
1. Start a terminal session. (Open iTerm)
2. Adapt the settings for your email and preferred name for your ssh key, then generate a new SSH key with: 
    ```text
    ssh-keygen -o -a 100 -t ed25519 -C “<login_name>@example.com" -f ~/.ssh/<nick>_default`
    ``` 
    where:   
    **-t ed25519**: Specifies the key type (modern and secure).  
    **-a 100**: Adds additional computational cost for better security.  
    **-C "<login_name>@example.com"**: Provides an identifier for your key.  
    **-f ~/.ssh/<nick>_default**: Specifies the filename to save the key at the correct place in your home directory.  
   **Note**: The command will create a secret file, without suffix and a public file with suffix `.pub`. Your secret file
   should **never** be shared and only copied to your 1Password. Make sure to always add your public part to services.
3. Follow the prompts to save the key (press Enter to save in the default location `.ssh/`)    
4. Create an SSH config file named `config`, so your applications like PyCharm, will be using your default SSH key.   
   Note: Change the name of the file in the config to your chosen name!  
   **Mac: .ssh/config**
   ```text
   Host *
     UseKeychain yes
     AddKeysToAgent yes
     IdentityFile ~/.ssh/<nick>_default
   ```
    **Win: .ssh/config**
   ```text
   Host *
     UseKeychain yes
     IdentityFile ~/.ssh/<nick>_default
   ```
5. Start and add the SSH key to the SSH agent:    
`eval "$(ssh-agent -s)"`
`ssh-add -K ~/.ssh/my_filename_`    
6. Copy the SSH key to your clipboard:  
`pbcopy < ~/.ssh/<my_filename_>.pub`  (*command specific to MacOS*)  
`clip < ~/.ssh/id_ed25519.pub` (*command specific to Windows*)  
7. Go to your GitHub account Settings/SSH and GPG keys/New SSH Key    
8. Paste the SSH key and click add SSH key  
9. Test SSH connection `ssh -T git@github.com`    
   If the SSH key is set up correctly and added to your GitHub account, you will see a message similar to:  
   *Hi <your_username>! You've successfully authenticated, but GitHub does not provide shell access.*  

### 9. Create a personal GitHub account and add your SSH public file
1. Go to [GitHub](https://github.com/join) and click Sign Up (This will be your private account)  
   * Do not use your any company email account-use your personal, like `<you>@gmail.com`.
2. Follow the prompts to create an account with your email and username    
3. Verify your account via email  
4. Add your public SSH key part to your user profile.
   1. Copy the SSH key to your clipboard:  
      * Mac: `pbcopy < ~/.ssh/<my_filename_>.pub`
      * Win: `clip < ~/.ssh/id_ed25519.pub` 
   2. Go to your GitHub account Settings -> SSH and GPG keys -> click New SSH Key    
   3. Paste the SSH key and click add SSH key  
   4. Test SSH connection `ssh -T git@github.com`      
      If the SSH key is set up correctly and added to your GitHub account, you will see a message similar to:    
      *Hi <your_username>! You've successfully authenticated, but GitHub does not provide shell access.*  

### 10. Create a GitHub repository in your personal profile
1. Create a repository and **only** add a `README.md`
   1. Log in to GitHub
   2. Click the + icon in the top-right corner
   3. Select New repository
   4. Enter a repository name (e.g., my-first-repo)
   5. Choose the visibility:
      * Public: Anyone can see it ← use this one to avoid costs
      * Private: Only you (and invited collaborators) can access it (€€€)
   6. Add a README file
   7. Click Create repository  
2. Branch from main/master branch and create a `develop` branch.

### 11. Install PyCharm and clone your repository
1. Create a folder in your home directory called `PycharmProjects`
2. Install PyCharm via the app JetBrains Toolbox.
   * If not delivered via you Brewfile: `brew install --cask jetbrains-toolbox`
3. Install plugins for .gitignore and .gitattributes.
4. Clone the created repository from step 10.
   * Save in your PycharmProjects/ folder
5. Change from `main/master` to the `develop` branch.
6. Create a .gitignore file in your project root with your plugin
   1. Right-click on your root folder
   2. Select New/.gitignore File/.gitignore File
   3. Select good stuff
   4. Click Create
7. Create a .gitattribues file in project root and paste the content below.
8. Commit and Push your new files.
9. Create a `uv` supported virtual environment 
   * vu is installed via Brewfile, if not run: `brew install uv`
   1. Go to PyCharm > Settings 
   2. In the settings window: your_project_name > Python Interpreter
   3. Switch to the virtual environment    
      1. Click the drop down list next to the list of Python interpreters
      2. Select Add Interpreter or Show All….depending on your version of PyCharm
      3. If you selected Add Interpreter , select Add Local Interpreter
      4. On the right side select uv
      5. When it is a new set up for virtual environment choose radio button next to New on row next ‘Environment:’
      6. It is already chosen default in most cases
      7. Next row at ‘Location:’ navigate to the location where your virtual environment is stored. It is usually in your project and it is named venv.
      8. It looks like this under your user ‘/Users/username/PycharmProjects/<your-project-name>/venv’
      9. Next row ‘Base interpreter:’ navigate to /venv/bin/python (on Windows venv\Scripts\python.exe) and select it as your interpreter.
      10. It looks like ‘/Users/username/venv/bin/python’ 
      11. Confirm the changes
          1. After selecting the virtual environment as the interpreter, click Apply and/or OK to confirm and close the window.
          2. Restart pyCharm
      12. In the terminal within PyCharm, enable the virtual environment if it is not already enabled (depending on your PyCharm version, this may happen automatically).
      13. Run the command  
        `‘python --version’`
        which shows something like ‘Python 3.12.5’ or       
        use command  
        `which python`  
        which shows    
        ‘/Users/username/PycharmProjects/Your-Project-Name/venv/bin/python’     
        - This ensures that the virtual environment's Python is used.      
        - The prompt in terminal window should look like *‘(venv) <username>@<alias-name-from-Git> <your-project> % ‘*    
        - When this is done your virtual environment for the project is automatically activated.    
        - Now your virtual environment is configured as Python interpreter for your project in PyCharm. Any Python modules you install while this interpreter is selected will be installed in your virtual environment.  

#### .gitattributes
```text
# Project specific
*.<anything binary not listed below>

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

## Old stuff - use it to make above parts more complete
  
#### Configuring virtual environment 
Create virtual environments and configure  

Configure Python interpreter in PyCharm to use a virtual environment  
1. Check if the virtual environment (venv) folder exists  
`ls -l | grep venv`
2. Check if the virtual environment is activated  
`echo $VIRTUAL_ENV`  
If activation works and you see venv in your terminal prompt, then the virtual environment exists.  
3. Open your project in PyCharm  
    Start PyCharm and open the project where you want to use the virtual environment.


**Activate virtual environment for the project**          
The virtual environment could at this stage already be activated.  If it is not then enter command:      
`source “venv”/bin/activate_`

**Deactivate virtual environment for the project**      
Open the terminal in PyCharm and deactivate your virtual environment with command: `deactivate`

**Re-activate the virtual environment again after deactivation**    
1. If you are not already in your project folder, navigate there with the ```cd``` command.  
Example:  
   `cd ‘/Users/<username>/PycharmProjects/<Your-Project-Name>’`
2. Open the terminal in PyCharm and deactivate your virtual environment with command:  
   `source venv/bin/activate`   

**Install certain packages for your virtual environment**    
Once the virtual environment is enabled, you can install Python packages specific to that project with command  
`pip install <package-name>`    

**Create and list your installed python packages and their versions in your virtual environment**    
1. Activate the virtual environment, if necessary with  
`source venv/bin/activate`    
2. Generate your ‘requirements.txt’ in terminal window with  
`pip freeze > requirements.txt`    
3. Verify the contents of ‘requirements.txt’:  
Open requirements.txt in PyCharm or a text editor to view its contents. It should look something like this:  
Flask==2.1.1  
requests==2.26.0  
numpy==1.21.0  
You should save your ‘requirements.txt’ for your project saved in Git to make your environment reproducible.  
#### Update installed packages
Update installed packages to latest version  
1. Open the terminal in PyCharm and activate your virtual environment with command if it is not done  
`source venv/bin/activate`
2. Update specific package to latest version  
`pip install --upgrade <packagename>_`
3. Update your requirements.txt file to reflect the latest versions  
`pip freeze > requirements.txt`
4. If you or someone else want to use updated requirements ‘requirements.txt’ to install on another system or into another environment run this command  
`pip install -r requirements.txt`

#### Project Collaboration - Git initialize/Repo Cloning    
To start developing or collaborating to an existing project on Github, you’ll need to clone an existing repository to work and contribute on a project.  However before cloning you need to check if git lfs is initialised.  
**Check for Git LFS Tracking**  
Check if Git LFS is being used to track certain file types    
`git lfs track`   
This will display a list of file types being tracked by LFS (e.g., *.iso, *.jpg, etc.). If no file types are being tracked, it will print an empty list.  
Look for .gitattributes file. 
Check if a .gitattributes file exists in your repository’s root directory. Git LFS uses this file to specify which file types should be tracked by LFS.   
`cat .gitattributes`  
If LFS is initialized, you should see entries like: 
`*.iso filter=lfs diff=lfs merge=lfs -text`  
This indicates that .iso files are being tracked by LFS.  

**Verify the Installation Globally**  
Check if Git LFS is installed globally    
`git lfs version`  
This will display the installed version of Git LFS if it’s installed correctly.

Git LFS commands list -  
* `git lfs track` Lists file types being tracked by Git LFS  
* `.gitattributes` Contains entries specifying LFS tracking rules  
* `git lfs version` Verifies if Git LFS is installed globally  

**Repository Cloning**  
1. Get URL of the GitHub repository to be cloned  
   1. Go to github account on browser>repo (to be cloned) and look for green CODE button (scroll to page top on right)
   2. Click on CLONE
   3. Copy the URL path from the SSH tab   
2. In PyCharm, select 'Get from Version Control' from the welcome screen.  
3. In the dialog box, paste the URL of the GitHub repository (e.g., git@github.com:username/repository.git).  
4. Select a directory to store the project and click Clone.
5. Authenticate and Open the Project
	1.	If prompted, select SSH Key Authentication.
	2.	If this is your first time, allow PyCharm to use SSH Agent.
	3.	Wait for the cloning process to complete.
	4.	Once cloned, PyCharm will open the project.
6. Repeat the steps for cloning wiki by copying path to clone wiki which you can find on the wiki page in browser at the bottom 
   
#### Create a .gitignore file for git repository/project   
The .gitignore file is used to exclude certain files to be attached to your ongoing project in git. The files could have other useful purposes.    
* Generate .gitignore **in PyCharm**  
  1. Open your project in PyCharm 
  2. Create a new .gitignorefile:  Right-click on your project root (where you want to create .gitignore the .file) in the Project Tool Window.
  3. Select New > File 
  4. Name the file .gitignore and press Enter 
* Choose .gitignore-template **using a plugin**:  
  If you already have a plugin .gitignore installed in PyCharm, you can use it to quickly generate one .gitignore based on different templates else follow as under.
  1. Menu > Settings > PyCharm > Settings… (or the the cogwheel at upper right corner in PyCharm and right click on it 
  2. Navigate to Plugins in the Settings menu to be sure it is installed 
  3. Settings > tab Marketplace (under plugins) > find .ignore. You can also select tab installed to search for plugin .ignore.   
  4. Install the plugin called .ignore (it handles .gitignore, .dockerignore, and similar files). 
  5. Restart PyCharm if prompted
  6. Generate .gitignore with template  
    After you install .ignore the plugin, return to your project view. Open the newly created .gitignore file if it is not already open. 
    In Open file locate green rectangle in the upper right corner of the PyCharm window "Add template… ”.  Choose the applicable template. 
     * List of added templates in this case
       * JetBrains template 
       * Xcode template 
       * Ansible template 
       * macOS template 
       * OpenSSL template 
       * Python template 
       * Vagrant template 
       * Txo best practices:
        
       ```
         ### txo-best-practices-general template
         """
         ${PROJECT_NAME} - ${NAME}
         Created by ${USER} on ${DATE} at ${TIME}.    
        
         def main():
         print("Template, ${NAME}!")

         if __name__ == "__main__":
         main()
         ## Txo Best Practice
         # General
         *tmp/
        
         # Credentials
         .vault_password
         *_vault.*
         *-secrets.*
        
        ```

* Customize .gitignore:    
You can now view and edit the contents of your .gitignore. Add or remove rows depending on the specific needs of your project.
* Save the file:  
When you are satisfied with your .gitignore, save the file.  
Your .gitignore file is now set and will be used by Git to ignore specific files and directories in your project.

### Install Ansible  
Ansible is an automation tool you’ll use to automate tasks in your Python project, such as server management or application deployment.  
**Prerequisite:** Ansible supports Python 3.8 or newer  
  
1. Activate the virtual environment  
`source venv/bin/activate`
2. Install Ansible using pip  
`pip3 install ansible`
3. Verify the installation  
`ansible --version`
4. Install Ansible-lint using pip for help checking your Ansible code for best practices and syntax errors  
`pip install ansible-lint`  
5. Test ansible installation  
`ansible localhost -m ping`  
You should see output confirming a successful connection.    
localhost | SUCCESS => {  
    "changed": false,  
    "ping": "pong"  
}    

---   

### Educational references 
#### Homebrew installation  
Homebrew simplifies the installation of necessary tools such as Git, Python, and other dependencies. The Brewfile simplifies tool management by bundling essential software installations into a single file. This guide covers the creation and usage of a Brewfile for setting up a macOS development environment with PyCharm and Ansible.  
The installation script will ask you to confirm the installation. You may need to enter your `administrator password` (one used to unlock your device) to continue.
The installation may also ask you to install the `Xcode Command Line Tools` if they are not already installed. This is a necessary step because Homebrew requires these tools.
After installation, the script can automatically add Homebrew to your PATH.   
If it doesn't, you can add it manually by running the following command in terminal:  
   ```echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile eval "$(/opt/homebrew/bin/brew shellenv)"```  
These commands ensure that Homebrew is available in your terminal session.
#### Cask    
A cask refers to a method for managing the installation of macOS applications that are distributed as binaries, typically in .dmg, .pkg, or .app formats. Casks are used for software that can be compiled from source and needs to be downloaded and installed as a pre-built package. When you install software via Homebrew Cask, it automates the process of downloading, installing, and managing these types of macOS applications.

#### Python and Pip install
* Python is needed for development and pip helps install Python libraries and dependencies.

#### Pycharm, Zsh, Virtual environments , JetBrains and ansible
* PyCharm provides tools like code completion, debugging, Git integration, and more to streamline Python development.
* ~/PycharmProjects/ directory is like having a special box where you keep all your PyCharm projects. It helps you stay organized while working with Git and GitHub.    
* Zsh - Apple has announced that in macOS 10.15 Catalina the default shell we be zsh. This does not say that bash is gone. Zsh is available Mojave and on older macOS versions. You can start testing zsh or even switch your default shell already. To see how it works just open a Terminal window and type ```zsh```. The reason Apple has not switched to these newer versions is that they are licensed with GPL v3. bash v3 is still GPL v2. If you are interested in depth about it see link: *Moving to Zsh*
* Zsh offers enhanced productivity features like autocompletion and Oh My Zsh further enhances the shell with plugins and themes.
* JetBrains toolbox is a collection of development tools and IDEs (Integrated Development Environments) which is a comprehensive collection of powerful and professional tools for developers, covering a wide range of programming languages and platforms. With tools like IntelliJ IDEA, PyCharm, WebStorm and many more, JetBrains Toolbox gives developers the tools they need to efficiently create high-quality software. JetBrain's Toolbox App makes managing these tools simple and centralized, improving productivity and facilitating work in complex development environments.
* Virtual environments help you manage dependencies and avoid conflicts between projects.
* Ansible is essential for automating tasks in your development workflow, such as managing environments and deployments.

#### What is the Purpose of Installing and Activating Zsh?
To talk to your computer, you need a special language—that’s called a shell.
Zsh (Z Shell) is smarter and faster version of the normal shell (which is called Bash). It helps you type commands more easily, gives you improved suggestions and makes process quicker.  
- Easier Typing – It autocompletes your commands if you type the initial of the command and press tab, similar to how your phone suggests words as you type a message.
- More Powerful – You can customize it with plugins to work faster.   
#### Advantages of using a virtual environment  
* Isolation: Each project can have its own versions of Python packages, avoiding conflicts between different projects.  
* Ease of management: You can easily keep track of and update dependencies specific to one project without affecting others.  
* Reproducibility: You can share your requirements.txt file with others, making it easy for them to install the same packages and versions you use in your virtual environment.

#### Difference Between .zshrc and .zprofile
Your computer is like a big playground and every time you open your playground (your terminal), you have different rules for how things work.  

**.zprofile** – The Playground Entrance Rules (One-Time Rules)  
* Think of .zprofile as the rules you follow when you enter the playground for the first time.  
* You only read these rules once when you step inside.  
* Example: If the rule says, “You must wear sneakers to play,” you put on sneakers before you start playing.  
* In the computer world, .zprofile sets things like where to find tools (PATH).

**.zshrc** – The Playground Game Rules (Every Time Rules)
* .zshrc is like the rules for every game you play inside the playground.
* Each time you start a new game (open a terminal tab), you read these rules again.
* Example: If the rule says, “Always start with a warm-up lap,” then every time you start a new game, you run a warm-up lap first.
* In the computer world, .zshrc is for shortcuts (aliases), colors, and fun settings.

**When to Use Each File**

| Feature | `.zprofile` | `.zshrc` |
|---------|------------|----------|
| **Login Shell** | ✅ Yes | ❌ No |
| **Interactive Shell** | ❌ No | ✅ Yes |
| **Runs on New Terminal Window** | ✅ First time only | ✅ Every time |
| **Used for Environment Variables** | ✅ Yes | ❌ No |
| **Used for Aliases & Functions** | ❌ No | ✅ Yes |

#### Git and GitHub
* Git lets you save different versions of your work on your own computer.
* GitHub is like an online bookshelf where you can store, share, and work on projects together with others from anywhere in the world!
* Git is a version control system that tracks changes in your codebase, allows you to manage version history and helps you collaborate with others. You will need Git to interact with GitHub repositories.
* Git allows you to push/pull code to and from GitHub.
* Proper Git configuration ensures that your commits are correctly attributed to you when using Git.
* Cloning a repository allows you to download and work on an existing project from GitHub.
* GitHub is a cloud-based platform for version control and collaboration, built on Git. It allows developers to store, track, and manage code changes efficiently.  

Key Concepts - GitHub:  
* Repository (Repo): A storage space for your project, containing files and version history.
* Commit: A saved change in a repository.
* Branch: A separate version of the code for development without affecting the main code. A branch is like having extra drawing sheets where you can test new ideas without messing up your original work.
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
- When you save a file on Windows, it may use CRLF. When you share that file with someone using Mac or Linux, Git automatically changes it to LF so it looks right on their system as CRLF is used on windows and not Mac/Linux.
- Problem: If Git changes it without asking, sometimes it breaks your code or makes it look different than you expected.  
#### SSH keys and its uses  
- SSH (Secure Shell) is a way for one computer to safely connect to another computer over the internet. It’s like a secure tunnel that keeps your information private and safe from hackers.    
- Secure Communication – No one can eavesdrop on your commands. 
- No Need for Passwords Every Time – It uses keys instead of typing a password every time.  
- Safe File Transfers – You can move files between computers safely.  
- Works Anywhere – **You can control your computer remotely from another device. Hence its important to keep it safe.**  
-----
## Morre's review comments about this documentation
### Structure/logical flow
I think this is a good structure:
1. Install & validate brew
2. Make sure zsh and Oh my Zsh is working
   1. The PATH working = right app starts (`which` is a good command)
   2. Is your shell showing the stuff
   3. The difference between `.zshrc` and `.zprofile` Chattan: https://chatgpt.com/share/e/67475d1a-34a0-8002-bd02-f0da7853fd3d
3. Initialize `git` and `git-lfs`
4. Create `.ssh/`, SSH key pair and setup `.ssh/config`
5. Set up your GitHub account and add the **public** SSH key
6. Create a repository in your personal GitHub account and branch
   1. Name: `<name>-playground`  with `README.md` (but not `.gitignore`)
   2. Branch `develop` from `main`and `add-gitignore`
   3. Turn on Wik
7. Create a directory for PyCharm: `~/PycharmProjects`
8. Install PyCharm Community via JetBrains Toolbox
9. Start PyCharm 
10. Install or validate that the .gitigore plugin is installed in PyCharm 
11. Clone the playground repository **and** its wiki
    1. Clone with ssh, not https!
    2. Make the wiki reside in the same PyCharm window
12. Choose the `add-gitignore` branch in the code repo (wiki repo will only have `main`)
13. Add a correct `.gitignore` and `gitatttribute` for Git LFS
14. Set up a Python environment in PyCharm for your project and add in the project root as `venv`
15. Commit and Push the two files to GitHub (`venv`should not be pushed thanks to the `.gitignore`)
16. Update `pip` package in your virtualenv if needed
17. Create a pull request from the playground branch to `develop`.
18. Merge without deleting the playground branch (so someone can validate things)
19. On GitHub, create a new (feature) branch from `develop` (as always) named `add-ansible`
20. Download/fetch the branch to PyCharm with `git fetch --all`
21. Select the branch and install Ansible via terminal in PyCharm
22. Create a `requirements.txt` and `pip freeze` you package list into it.
23. Commit, Push and Merge to `develop` via PR on GitHub 

### Markdown handling comments
* You have not been able to follow how the other files look.
* Things that has to be done in order should be in a numbered list, not bullet.
* If you want to start on a new line for readability, use double space in the end of the row above.
* You indent your list and other text when it should not, making numbering not working correctly, for example.
* You need to comment the first row in Brewfile, else it will not work: `# Brewfile`
* Three \``` is block text, one \` is line/word text only
* Git LFS is for handling large files, you clone repositories with Git
* Nowadays, you just write `python`, `pip` etc. without the 3, since Python 2 is "dead"
* See if it could be more of a step-by-step guide with links to education, to make the flow easier to see.