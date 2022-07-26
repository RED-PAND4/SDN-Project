# SDN Project: Morphing Network Slices
<p align="center">
  <a>
    <img src="image/logo_black.png",  style="width: 30%;">
  </a>
  <h2 align="center">Morphing Network Slices</h2>

  <p align="center">
  Exam project for Softwarized and Virtualized Mobile Networks 
  <br>University of Trento - Prof. <a href="https://github.com/fabrizio-granelli">Fabrizio Granelli</a>
  </p>
</p>
<br>

### Download
```
git clone https://github.com/RED-PAND4/SDN-Project.git
```
### Prerequisites
* Linux OS (tested on [Ubuntu 20.04](https://releases.ubuntu.com/20.04/))
* [Ryu](https://ryu-sdn.org/)
* [Mininet](http://mininet.org/)
* [Python & Python3](https://www.python.org/)

## Comands for morphing :

***start controller***
```
ryu-manager morph_controller.py
```
***run network***
```
sudo python3 morph_network.py
```
_______________

*command*

```
 Enter command (bus, ring, star, cli, quit): bus
```

<div>
    <img src="image/Bus.png",  style="width: 50%;">
</div>

```
 Enter command (bus, ring, star, cli, quit): ring
```

<div>
    <img src="image/Ring.png",  style="width: 50%;">
</div>

```
 Enter command (bus, ring, star, cli, quit): star
```

<div>
    <img src="image/Star.png",  style="width: 50%;">
</div>

```
 Enter command (bus, ring, star, cli, quit): cli -> enter mininet CLI for mininet command
```

```
 Enter command (bus, ring, star, cli, quit): quit -> end all
```
_______________
*help*

you need to wait the spanning tree before trying to ping the hosts, it ends when you see the "/FORWARD" at the end of the line in the controller terminal or you can wait 40-50 seconds from when you decide the topology

## RYU-Api-Solution
1. Making sure Mininet is clear and all Ryu controllers instances are terminated:
```
sudo mn -c ; sudo fuser -k 6633/tcp
```
2. Starting the network with Mininet:
```
sudo mn --custom ryu_api_solution/network.py --controller remote --topo test --arp
```
3. Run Ryu controller with rest api:
```
python3 ryu_api_solution/run_controller.py 
```
That's how the **physical network** looks like:
<div>
    <img src="image/Net.jpg",  style="width: 50%;">
</div>

4. Run our app to slice the network
```
python3 ryu_api_solution/slice_topology.py 
```
Now the network has been sliced: "red" host can only communicate with "red" hosts and the same is for the "blue" ones
<div>
    <img src="image/Sliced.jpg",  style="width: 50%;">
</div>

5. Simulate a link down between s2 and s5
```
mininet> link s2 s5 down
```
6. Run our app to solve the broken link
```
python3 ryu_api_solution/solve_link_down.py
```
Finally we reprogrammed two of the switches, to overcome the use of the link between s2 and s5 and restore the functionality of the network.
<div>
    <img src="image/Link Down.jpg",  style="width: 50%;">
</div>

