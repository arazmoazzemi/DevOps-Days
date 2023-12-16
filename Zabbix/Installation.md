  Example for zabbix-6.4.6 **kvm** installation:

```bash
virt-install \
  --import --name zabbix \
  --memory 8192 \
  --vcpus 4 \
  --cpu host \
  --disk /var/lib/libvirt/images/zabbix-6.4.6.qcow2,format=qcow2,bus=virtio \
  --network bridge=virbr0,model=virtio \
  --osinfo detect=on,require=off \
  --graphics none \
  --noautoconsole \
```

----

Set static ip address:

___Use vi or nano for edit network interface:___

```bash
yum install nano
nano /etc/sysconfig/network-scripts/ifcfg-eth0

TYPE=Ethernet
NAME=eth0
BOOTPROTO=none
IPADDR="192.168.122.85"
NETMASK="255.255.255.0"
GATEWAY=192.168.122.1
DNS1=8.8.8.8
DNS2=1.1.1.1
DEVICE=eth0
ONBOOT="yes"
PEERDNS=no
```

```bash
systemctl restart network
```




