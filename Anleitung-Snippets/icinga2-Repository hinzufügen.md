```bash
sudo su
apt update
apt -y install apt-transport-https wget

wget -O icinga-archive-keyring.deb "https://packages.icinga.com/icinga-archive-keyring_latest+ubuntu$(
 . /etc/os-release; echo "$VERSION_ID"
).deb"

apt install ./icinga-archive-keyring.deb

. /etc/os-release; if [ ! -z ${UBUNTU_CODENAME+x} ]; then DIST="${UBUNTU_CODENAME}"; else DIST="$(lsb_release -c| awk '{print $2}')"; fi; \
 echo "deb [signed-by=/usr/share/keyrings/icinga-archive-keyring.gpg] https://packages.icinga.com/ubuntu icinga-${DIST} main" > \
 /etc/apt/sources.list.d/${DIST}-icinga.list
 echo "deb-src [signed-by=/usr/share/keyrings/icinga-archive-keyring.gpg] https://packages.icinga.com/ubuntu icinga-${DIST} main" >> \
 /etc/apt/sources.list.d/${DIST}-icinga.list

apt update
exit
```
