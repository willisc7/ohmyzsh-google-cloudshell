# ohmyzsh-google-cloudshell

1. Install zsh every time the cloudshell instance boots
```
touch $HOME/.customize_environment
cat << EOF >> $HOME/.customize_environment
# install zsh
sudo apt-get -yq install zsh
EOF
```
2. Install ohmyzsh and set default shell to zsh (for some reason this doesnt work properly if done in `.customize_environment` even when running ohmyzsh install using `--unattended`)
```
cat << EOF >> $HOME/.profile
# set default shell to zsh and install ohmyzsh
sudo chsh -s /bin/zsh $USER
sh -c "\$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
EOF
```
3. On the cloudshell page, click on the three dots in the upper right-hand corner, click **Restart**, select **Want clean VM state**, and click **Restart**
4. Open a cloudshell session and run `gcloud config set project PROJECT_ID`
  * I tried getting around this by putting `DEVSHELL_PROJECT_ID=$(bash -c "echo $DEVSHELL_PROJECT_ID")` into `.zshenv` but that doesnt update automatically for some reason if you open another cloudshell under another project.
