IMAGE_NAME = "bento/ubuntu-22.04"
N = 2

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false

  # ─── Master ────────────────────────────────────────────
  config.vm.define "k8s-master" do |master|
    master.vm.box = IMAGE_NAME
    master.vm.network "private_network", ip: "192.168.56.10"
    master.vm.hostname = "k8s-master"
    master.vm.provider "virtualbox" do |v|
      v.name   = "k8s-master"
      v.memory = 1536   # économie RAM vs original (2048)
      v.cpus   = 2
    end
  end

  # ─── Workers ───────────────────────────────────────────
  (1..N).each do |i|
    config.vm.define "node-#{i}" do |node|
      node.vm.box = IMAGE_NAME
      node.vm.network "private_network", ip: "192.168.56.#{i + 10}"
      node.vm.hostname = "node-#{i}"
      node.vm.provider "virtualbox" do |v|
        v.name   = "node-#{i}"
        v.memory = 1536
        v.cpus   = 1   # workers n'ont besoin que d'1 vCPU
      end
    end
  end
end
