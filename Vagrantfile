Vagrant.configure("2") do |config|
  config.vm.define "srv" do |srv|
    srv.vm.box = "debian/bookworm64"
    srv.vm.network "private_network", ip: "192.168.57.10"
  end

  config.vm.define "printer" do |printer|
    printer.vm.box = "debian/bookworm64"
    printer.vm.network "private_network", ip: "192.168.57.50"
  end
end
