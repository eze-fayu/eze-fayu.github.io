# COMO LINKEAR 2 REDES LAN CON ZEROTIER

1. Instalar zerotier en 2 dispositivos, uno por red. tiene que estar siempre conectados

2. Conectarlos a la misma red de zerotier

3. habilitar el redireccionado en ambas maquinas
    - sudo sysctl -w net.ipv4.ip_forward=1

4. obtener los nombres de las redes
    - PHY_IFACE=eth0; ZT_IFACE=zt7nnig26

5. poner ese codigo actualizado en la terminal

6. pasar los siguientes comandos que tomas las variables anteriormente asignadas
    - sudo iptables -t nat -A POSTROUTING -o $PHY_IFACE -j MASQUERADE
    - sudo iptables -A FORWARD -i $PHY_IFACE -o $ZT_IFACE -m state --state RELATED,ESTABLISHED -j ACCEPT
    - sudo iptables -A FORWARD -i $ZT_IFACE -o $PHY_IFACE -j ACCEPT

7. poner esto comandos para que sea persistente al reinicio
    - sudo apt install iptables-persistent
    - sudo su && bash -c iptables-save > /etc/iptables/rules.v4
8. crear los puentes de ida y vuelta en la pagina de zerotier
            Destination                 (Via)
            $PHY_SUB                   $ZT_ADDR

For example:

            Destination                  (Via)
        192.168.100.0/23                172.27.0.1



[Fuente](https://zerotier.atlassian.net/wiki/spaces/SD/pages/224395274/Route+between+ZeroTier+and+Physical+Networks)


