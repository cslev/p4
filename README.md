# p4
Collection of P4_16 programs

## Outline
Each directory here consists of a sample application with a correpsonding README file about aim, usage, and compilation

## What the programs here do
- P4 description of different use cases
- Once compiled, they can be fed to a P4 switch (e.g., software switch behavioral-model)
- When run, usually a control plane is necessary to populate the match+action tables, but usually they provided here

## What the programs here do not do
- neither provide any development environment, nor any compiler - this should be done yourself


## Usage
- In case you have already cloned the repository, get into the directory where the P4 program intended to run is located.
- Compile
  example: `$ sudo p4c-bm2-ss portfwd.p4 -o portfwd.json`
- run program/fed program to a P4 appliance
  example: `$ sudo simple_switch -i 0@veth1 -i 1@veth2 portfwd.json`
- populate match+action tables corresponding to the P4 program
  example: 
```
$ sudo simple_switch_CLI --thirft-port 9090 
RuntimeCmd: table_add MyIngress.port_exact MyIngress.portfwd 0 => 1
Adding entry to exact match table MyIngress.port_exact
match key:           EXACT-00:00
action:              MyIngress.portfwd
runtime data:        00:01
Entry has been added with handle 0
```

## How to proceed forward?
Get into the directory of the P4 application you want to use.
