Vagrant.configure('2') do |config|

  config.vm.box = "ubuntu/focal64"

  config.vm.provision :shell, inline: <<-EOF
    if [ ! -f go1.16.5.linux-amd64.tar.gz ]; then
      wget https://golang.org/dl/go1.16.5.linux-amd64.tar.gz
      rm -rf /usr/local/go && tar -C /usr/local -xzf go1.16.5.linux-amd64.tar.gz
      cd /home/vagrant && curl -fsSL https://get.pulumi.com | su vagrant -c sh
    fi
    apt update
    apt install make
    mkdir /opt/pulumi
    sudo chown vagrant /opt/pulumi
    echo 'export PATH=/opt/pulumi:/opt/pulumi/bin:$PATH:/usr/local/go/bin' >> /etc/profile
  EOF
end
