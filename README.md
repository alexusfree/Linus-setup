# Linus-setup
curl -sSL https://raw.githubusercontent.com/alexusfree/Linus-setup/master/test-install.sh | bash

curl -sSL https://raw.githubusercontent.com/alexusfree/Linus-setup/master/xxx-install.sh | bash


https://raw.githubusercontent.com/nextcloud/nextcloudpi/master/install.sh



# check_distro 
grep -q -e "Debian GNU/Linux 9" -e "Raspbian GNU/Linux 9" /etc/issue || {
  echo "distro not supported"; 
  exit 1; 
}

# check installed software
type mysqld  &>/dev/null && echo ">>> WARNING: existing mysqld configuration will be changed <<<"

# get install code
echo "Getting build code..."
apt-get update
apt-get install --no-install-recommends -y wget ca-certificates sudo

pushd "$TMPDIR"
wget -O- --content-disposition https://github.com/nextcloud/nextcloudpi/archive/"$BRANCH"/latest.tar.gz \
  | tar -xz \
  || exit 1
cd - && cd "$TMPDIR"/nextcloudpi-"$BRANCH"

# install NCP
echo -e "\nInstalling NextCloudPi"
source etc/library.sh

install_script  lamp.sh
