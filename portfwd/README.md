# Simple port forwarder
This simple application has only one exact match table, matching on the incoming port, and correspondingly has one action, which does nothing special just forwards the packet to the intended port.

## How to use (example)
### compile
Assuming you want to compile to bmv2 software switch
`$ sudo p4c-bm2-ss portfwd.p4 -o portfwd.json`

### run
Assuming you have two interfaces (veth1, veth2), and you want to add each of them to the switch:
`$ sudo simple_switch -i 0@veth1 -i 1@veth2 portfwd.json`

### configure
Assuming you want to bridge the two ports:
 - set default action
```
RuntimeCmd: table_set_default MyIngress.port_exact drop
Setting default action of MyIngress.port_exact
action:              drop
runtime data:
```
 - add port forwarding rules
```
RuntimeCmd: table_add MyIngress.port_exact MyIngress.portfwd 0 => 1
Adding entry to exact match table MyIngress.port_exact
match key:           EXACT-00:00
action:              MyIngress.portfwd
runtime data:        00:01
Entry has been added with handle 0

RuntimeCmd: table_add MyIngress.port_exact MyIngress.portfwd 1 => 0
Adding entry to exact match table MyIngress.port_exact
match key:           EXACT-00:01
action:              MyIngress.portfwd
runtime data:        00:00
Entry has been added with handle 1

```

Now, if you send traffic towards one of its port, you will receive them back on the other.

