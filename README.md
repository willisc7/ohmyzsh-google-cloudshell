# ohmyzsh-google-cloudshell

1. Install zsh, change default shell for current user, and download ohmyzsh every time the cloudshell instance boots
```
touch $HOME/.customize_environment
cat << EOF >> $HOME/.customize_environment
# install zsh
sudo apt-get -yq install zsh
sudo chsh -s /bin/zsh $USER
git clone --depth 1 https://github.com/ohmyzsh/ohmyzsh.git /tmp/ohmyzsh
EOF
```
2. On the cloudshell page, click on the three dots in the upper right-hand corner, click **Restart**, select **Want clean VM state**, and click **Restart**
3. Install ohmyzsh
```
cat << EOF >> $HOME/.zshrc
# install ohmyzsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
EOF
```
4. Setup environment variables
```
touch $HOME/.zshenv
cat << EOF >> $HOME/.zshenv
# copy over env vars from cloudshell default bash
DEVSHELL_PROJECT_ID=$(bash -c "echo $DEVSHELL_PROJECT_ID")
EOF
```
5. Close the current shell session and open a new one
