# ohmyzsh-google-cloudshell

1. Copy and paste the following block into your active cloudshell session
```
cat << EOF >> $HOME/.bashrc

# install zsh if its not installed
zsh --version > /dev/null
if [ \$? -ne 0 ]; then
  sudo apt-get -y install zsh
fi

# install ohmyzsh if its not installed and change default shell for user
if [[ ! -d "\$HOME/.oh-my-zsh" ]]; then
  sh -c "\$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended
  sudo chsh -s /bin/zsh \$USER
fi
EOF
```
2. Close the cloudshell instance and reopen it. This will install zsh and ohmyzsh and change your default shell to zsh. Since zsh will now be the default, `.bashrc` shouldn't be invoked again.
3. Run `gcloud config set project PROJECT_ID`
    * I tried getting around this by putting `DEVSHELL_PROJECT_ID=$(bash -c "echo $DEVSHELL_PROJECT_ID")` into `.zshenv` but that doesnt update automatically for some reason if you open another cloudshell under another project.
