# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get -y upgrade

    # Install docker
    apt-get install ca-certificates curl
    install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
    chmod a+r /etc/apt/keyrings/docker.asc
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      tee /etc/apt/sources.list.d/docker.list > /dev/null
    apt-get update
    apt-get install -y docker-ce docker-ce-cli containerd.io

    # Install & configure samba + cifs
    apt-get install -y samba cifs-utils
    cat <<EOT > /etc/samba/smb.conf
[media]
  comment = Media
  path = /media
  read only = no
  browseable = yes
  guest ok = yes
  force user = vagrant
EOT
    systemctl restart smbd
  SHELL
end
