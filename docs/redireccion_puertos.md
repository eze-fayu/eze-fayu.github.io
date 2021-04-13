# REDIRECCION DE PUERTOS EN RED CONECTADA POR ZEROTIER

Primero hay que habilitar el puente entre las redes lan como en la [guia](https://eze-fayu.github.io/docs/lan-bridge-zerotier.html) especifica.  
Asegurarse de habilitar el fordward (deberia estar si se sigui la guia) en la maquina que recibe las cosas del "exterior"

```
sudo nano /etc/sysctl.conf

net.ipv4.ip_forward=1

sudo sysctl -p
sudo sysctl --system
```

Tiene que haber ping entre los distintos dispositivos.  

De nuevo en, en la maquina que recibe el trafico hay q redireccionar los puertos

Reemplazar eth0 con la interfaz del dispositivo (encontralo usando ip a) y ztklhql2jy por la interfaz de zerotier

```
# By default drop traffic  para que entre solo por el puerto 80 y 443 que habilito
sudo iptables -P FORWARD DROP

# Allow traffic on specified ports
sudo iptables -A FORWARD -i eth0 -o ztklhql2jy -p tcp --syn --dport 80 -m conntrack --ctstate NEW -j ACCEPT
sudo iptables -A FORWARD -i eth0 -o ztklhql2jy -p tcp --syn --dport 443 -m conntrack --ctstate NEW -j ACCEPT

# Allow traffic between ztklhql2jy and eth0
sudo iptables -A FORWARD -i ztklhql2jy -o eth0 -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
sudo iptables -A FORWARD -i ztklhql2jy -o eth0 -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# Forward traffic from eth0 to ztklhql2jy on specified ports LO MANDA A LA PC DESTINO (SERVIDOR)
sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to-destination 10.147.19.104
sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 443 -j DNAT --to-destination 10.147.19.104

# Forward traffic back to eth0 from ztklhql2jy on specified ports DEVUELVE A LA RASPBERRY
sudo iptables -t nat -A POSTROUTING -o ztklhql2jy -p tcp --dport 80 -d 10.147.19.104 -j SNAT --to-source 10.147.19.160
sudo iptables -t nat -A POSTROUTING -o ztklhql2jy -p tcp --dport 443 -d 10.147.19.104 -j SNAT --to-source 10.147.19.160
```

Para hacer los cambios persistentes...

```
sudo apt install netfilter-persistent
sudo netfilter-persistent save
sudo systemctl enable netfilter-persistent

sudo apt install iptables-persistent
# hit yes to save the current rules.
```


Tutorial basado en el de [Selfhosted.pro](https://selfhosted.pro/hl/wireguard_vps/)