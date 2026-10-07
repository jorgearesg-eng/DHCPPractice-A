En esta práctica hemos configurado un entorno automatizado con Vagrant utilizando una red interna de VirtualBox (192.168.57.0/24), donde disponemos de un servidor DHCP (srv), una impresora con IP fija (printer) y un cliente dinámico (c1).
1. Verificación del cliente dinámico (c1)
Para comprobar que el cliente ha obtenido una dirección IP de forma automática por DHCP, ejecutamos el siguiente comando:

vagrant ssh c1 -c "ip a"

Salida obtenida:

3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

    link/ether 08:00:27:04:db:7c brd ff:ff:ff:ff:ff:ff

    inet 192.168.57.50/24 brd 192.168.57.255 scope global dynamic eth1

       valid_lft 594sec preferred_lft 594sec
2. Comprobación de conectividad
Para verificar que el cliente tiene comunicación directa con el servidor DHCP (192.168.57.10), realizamos una prueba de red:

vagrant ssh c1 -c "ping -c 3 192.168.57.10"

Salida obtenida:

PING 192.168.57.10 (192.168.57.10) 56(84) bytes of data.

64 bytes from 192.168.57.10: icmp_seq=1 ttl=64 time=0.421 ms

64 bytes from 192.168.57.10: icmp_seq=2 ttl=64 time=0.385 ms

64 bytes from 192.168.57.10: icmp_seq=3 ttl=64 time=0.392 ms

--- 192.168.57.10 ping statistics ---

3 packets transmitted, 3 received, 0% packet loss, time 2045ms

rtt min/avg/max/mdev = 0.385/0.399/0.421/0.015 ms
3. Comprobación en el servidor DHCP
Para comprobar las concesiones activas desde el servidor, revisamos el archivo de arrendamientos:

vagrant ssh srv -c "sudo cat /var/lib/dhcp/dhcpd.leases"

Salida obtenida:

lease 192.168.57.50 {

  binding state active;

  next binding state free;

  rewind binding state free;

  hardware ethernet 08:00:27:04:db:7c;

  client-hostname "c1";

}
4. Reserva estática de la impresora
Para verificar que la impresora recibe su IP estática configurada (192.168.57.111), comprobamos sus interfaces:

vagrant ssh printer -c "ip a"

Salida obtenida:

3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000

    link/ether 08:00:27:8a:b2:12 brd ff:ff:ff:ff:ff:ff

    inet 192.168.57.111/24 brd 192.168.57.255 scope global static eth1
