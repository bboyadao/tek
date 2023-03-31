---

##### Just in case ipv4 does not assign to container. 
```shell
sudo firewall-cmd --zone=trusted --change-interface=lxdbr0 --permanent
sudo firewall-cmd --reload
```


##### Prevent conflict with Docker.
```shell
iptables -I DOCKER-USER -i <network_bridge> -o <external_interface> -j ACCEPT
iptables -I DOCKER-USER -o <network_bridge> -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
```