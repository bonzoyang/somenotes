# how to activate CHT ADSL (中華電信ADSL) static ip

## set pppoe [\[ref\]](http://note.drx.tw/2008/08/networkpppoe-adsl.html)
sudo apt-get install pppoeconf
sudo pppoeconf
#### settings in pppoeconf GUI
```
adsl user: 12345678@ip.hinet.net # for CHT static ip, 12345678 is HN number CHT gave you
           12345678@hinet.net    # for CHT DHCP ip
password: # default password CHT gave you
all other options: yes
```

## edit this file [\[ref\]](https://www.opencli.com/linux/ubuntu-18-04-netplan-setup-static-ip), [\[ref\]](https://askubuntu.com/questions/1029531/how-to-setup-a-static-ip-on-ubuntu-server-18-04)
sudo vim /etc/netplan/01-network-manager-all.yaml

#### origin content
```bash
network:
    version: 2
    vender: networkD
``` 
#### modify to this
```bash
network:
    ethernets:
        enp0s31f6:
            dhcp4: no
            addresses: [111.222.333.444/32]
            gateway4: 111.222.333.254
            nameservers:
                addresses: [168.95.1.1, 8.8.8.8, 8.8.4.4]
```
sudo netplan apply


