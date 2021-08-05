# ohmyzsh-google-cloudshell

1. Copy and paste the following block into your active cloudshell session
```
cat << EOF >> $HOME/.bashrc

# install zsh if its not installed
zsh --version > /dev/null
if [ \$? -ne 0 ]; then
  sudo apt-get -y install zsh
fi

sudo chsh -s /bin/zsh \$USER

# install ohmyzsh if its not installed and change default shell for user
if [[ ! -d "\$HOME/.oh-my-zsh" ]]; then
  sh -c "\$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended
fi
EOF
```
2. Close the cloudshell instance and reopen it. This will install zsh and ohmyzsh and change your default shell to zsh. Since zsh will now be the default, `.bashrc` shouldn't be invoked again.
    * I tried doing this in `.customize_environment` but it ended up being too much of a hassle to maintain. Also, since it runs in parallel with your first login you end up with weird race conditions when using it in conjunction with `.bashrc` or `.profile`
3. Close the cloudshell instance again and reopen it. You'll now be in zsh.
4. Run `gcloud config set project PROJECT_ID`
    * I tried getting around this by putting `DEVSHELL_PROJECT_ID=$(bash -c "echo $DEVSHELL_PROJECT_ID")` into `.zshenv` but that doesnt update automatically for some reason if you open another cloudshell under another project.
