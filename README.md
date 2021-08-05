# ohmyzsh-google-cloudshell

1. When the initial shell opens in bash, the `.bashrc` file will install zsh and ohmyzsh and set the default shell to zsh going forward. This means `.bashrc` shouldn't be invoked again.
```
cat << EOF >> $HOME/.bashrc
# install zsh and ohmyzsh and change default shell to zsh
sudo apt-get -y install zsh
sudo chsh -s /bin/zsh \$USER
sh -c "\$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended
EOF
```
2. Close the cloudshell instance and reopen it
3. Run `gcloud config set project PROJECT_ID`
    * I tried getting around this by putting `DEVSHELL_PROJECT_ID=$(bash -c "echo $DEVSHELL_PROJECT_ID")` into `.zshenv` but that doesnt update automatically for some reason if you open another cloudshell under another project.
