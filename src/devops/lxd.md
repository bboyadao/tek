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


##### Docker inside LXC.
```shell
lxc storage create tower btrfs
lxc storage volume create tower docker
lxc config device add tower tower disk pool=tower source=docker path=/var/lib/docker
lxc config set tower security.nesting=true security.syscalls.intercept.mknod=true security.syscalls.intercept.setxattr=true
lxc restart tower
```