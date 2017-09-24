sudo ifconfig enp5s0 down
sudo ifconfig enp5s0 up
nmcli dev status


#wyłączenie interface w /etc/NetworkManager/NetworkManager.conf
[keyfile]
unmanaged-devices=
