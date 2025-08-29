## COE Deploy Experience

Training repo on the usage of Github deploy keys and Git sparse checkouts. 

***
### Creating SSH Key
```bash
#Create SSH folder if needed
mkdir -p ~/.ssh

#Navigate to SSH Folder
cd ~/.ssh

#Create SSH Key to Use with Project Repo Only. Don't Set Password on Key
ssh-keygen -t ed25519 -f {project_name} -C "{project_comment}"
```
### Creating SSH Config file
```bash
#Create SSH Config 
vim ~/.ssh/config

#===== ~/.ssh/config ==========
# Host github-{project_name} 
#   HostName github.com
#   User git
#   IdentityFile ~/.ssh/{project_name}
#   IdentitiesOnly yes
#
# For SSH over HTTPs
#   HostName ssh.github.com
#   Port 443


#Set Required Permissons on Config
chmod 600 ~/.ssh/config
```
### Add Public Key to Repo
Github Repo -> Settings -> Deploy keys -> Add Deploy key
```bash
cat ~/.ssh/{project_name}.pub
```
### Add Public Keys of Github
```bash
ssh-keyscan github.com >> ~/.ssh/known_hosts
```
### Clone Repo and Configure Sparse Checkout
```bash
#Clone Repo Using No Checkout
git clone --no-checkout git@github-{project_name}:ucdavis/{repo_name}.git

#Move Into Repo Directory
cd {repo_name}

#Initiate Sparse Checkout
git sparse-checkout init --no-cone 

#Set Folder or Item to Checkout
git sparse-checkout set {current_directory_path_to_item}

#Checkout Item(s)
git checkout main

# Add Items to Sparse Checkout
echo "{current_directory_path_to_item}" >> .git/info/sparse-checkout
```