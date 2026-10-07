Vagrant.configure("2") do |config|
  config.vm.define "srv" do |srv|
    srv.vm.box = "debian/bookworm64"
    srv.vm.network "private_network", ip: "192.168.57.10", virtualbox__intnet: "intnet"
  end

  config.vm.define "printer" do |printer|
    printer.vm.box = "debian/bookworm64"
    printer.vm.network "private_network", ip: "192.168.57.111", virtualbox__intnet: "intnet"
  end

  config.vm.define "c1" do |c1|
    c1.vm.box = "debian/bookworm64"
    c1.vm.network "private_network", type: "dhcp", virtualbox__intnet: "intnet"
  end
end