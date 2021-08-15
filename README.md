# lancachedns
this is for dns lancache server

use this EXAMPLE code and modify to suit your needs

docker run --name lancache-dns -p 10.0.0.2(localhostip):53:53/udp -e USE_GENERIC_CACHE=true -e LANCACHE_IP=10.0.0.3(localhostip) lancachenet/lancache-dns:latest

PLEASE NOTE if your using a pihole or another dns server you will need to modify some settings or host will fail to build image

NOTE: you need to run this:  it disables ubuntu's resolved service that is running on the host system.
sudo systemctl disable systemd-resolved
sudo systemctl stop systemd-resolved

Then put the following line in the [main] section of your /etc/NetworkManager/NetworkManager.conf:

dns=default
Delete the symlink /etc/resolv.conf

rm /etc/resolv.conf
Restart NetworkManager

sudo systemctl restart NetworkManager

next if you need to add one or more upstream dns servers run this command

use the bellow command and editto suit your needs. in my case I have two piholes so you will need to do "pihole1ip:pihole2ip"

docker run --name lancache-dns -p insertlocalhip:53:53/udp -e USE_GENERIC_CACHE=true -e LANCACHE_IP=insertlocalip -e UPSTREAM_DNS= "192.168.2.25(pihole1);192.168.2.30(pihole2)"  lancachenet/lancache-dns:latest
