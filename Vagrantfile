Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "public_network", ip: "192.168.1.21"
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/chahad.pub"
  config.vm.provision "file", source: "~/Documents/vagrant/rancher/instance/docker-compose.yaml", destination: "~/docker-compose.yaml"
  config.vm.provision "shell",
    inline: "apt-get update -y && apt-get install -y vim tree net-tools curl git && \
            sudo apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common && \
            curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && \
            sudo apt-key fingerprint 0EBFCD88 && \
            sudo add-apt-repository 'deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable' && \
            sudo apt-get update -y && sudo apt-get install -y docker-ce docker-ce-cli containerd.io && \
            sudo curl -L \"https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)\" -o /usr/local/bin/docker-compose && \
            sudo chmod +x /usr/local/bin/docker-compose && \
            sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose && \
            sudo docker-compose -f /home/vagrant/docker-compose.yaml up -d && \
            sudo curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && sudo chmod +x minikube && \
            sudo ./minikube start --vm-driver=none && \
            sudo curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl && \
            sudo chmod +x kubectl && mv ./kubectl /usr/bin/kubectl && \
            cd /home/vagrant/.ssh && cat chahad.pub >> authorized_keys" 
  config.vm.provider "virtualbox" do |v|
    v.name = "docker-minikube-rancher"
    v.memory = 4096
    v.cpus = 2
  end
  config.vm.define "docker-minikube-rancher" do |node|
    node.vm.provision "shell", inline: "swapoff -a"
  end
end


