### BORRAR LOS ARCHIVOS TEMPORALES EN /TMP


#### Modo manual

 `sudo find /tmp -ctime +10 -exec rm -rf {} +`

#### Con systemd

Borrar archivos temporales en Linux

Abrimos nuestra consola, accedemos como root y hacemos una copia del archivo temp.conf.  

`sudo cp /usr/lib/tmpfiles.d/tmp.conf /etc/tmpfiles.d/tmp.conf`

Abrimos con nuestro editor favorito.  
`sudo nano /etc/tmpfiles.d/tmp.conf`

Lo que haremos es modificar esos valores, por los siguientes.  
```
D /tmp 1777 root root 1s
D /var/tmp 1777 root root 1s
```

No te preocupes por la primera letra de la linea, puede variar dependiendo de tu distribución linux y la versión instalada. Debes copiar y pegar tal como está en la linea superior.
