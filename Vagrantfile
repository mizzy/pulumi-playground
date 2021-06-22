Vagrant.configure('2') do |config|

  config.vm.box = "ubuntu/focal64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
  end

  config.vm.provision :shell, inline: <<-EOF
    if [ ! -f go1.16.5.linux-amd64.tar.gz ]; then
      wget https://golang.org/dl/go1.16.5.linux-amd64.tar.gz
      rm -rf /usr/local/go && tar -C /usr/local -xzf go1.16.5.linux-amd64.tar.gz
      cd /home/vagrant && curl -fsSL https://get.pulumi.com | su vagrant -c sh
    fi
    apt update
    apt install make gcc net-tools
    mkdir /opt/pulumi
    sudo chown vagrant /opt/pulumi
    echo 'export PATH=/opt/pulumi:/opt/pulumi/bin:$PATH:/usr/local/go/bin' >> /etc/profile
    echo 'alias kubectl='minikube kubectl -- ' >> /etc/profile

    # docker
    apt install apt-transport-https ca-certificates curl gnupg lsb-release
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
      | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    echo \
      "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
    apt update
    apt install docker-ce docker-ce-cli containerd.io

    # minikube
    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
    dpkg -i minikube_latest_amd64.deb
  EOF
end
