# (Nmap) Escaneado de puertos

Primero que todo vamos a escanear los puertos abiertos de la IP de la maquina.

Para ver que sistema operativo es habria que hacer un ping para ver la info que nos muestra el TTL:

![Untitled]((Nmap)%20Escaneado%20de%20puertos%2077d9d3bf6c1b4695a9312adbfd88ae3c/Untitled.png)

![Untitled]((Nmap)%20Escaneado%20de%20puertos%2077d9d3bf6c1b4695a9312adbfd88ae3c/Untitled%201.png)

En este caso como ejemplo si la maquina da un numero siminar al 64 estariamos con Linux.

Nunca pone el ttl original si estas por VPN poque no te comunicas directamente con la maquina victima ya que hay un nodo intermediario por el medio que es el VPN y disminuye un numero.

Para empezar el escaneo primero veremos el manual de nmap para hacernos una idea de como funciona por dentro:

```bash
man nmap
```

![Untitled]((Nmap)%20Escaneado%20de%20puertos%2077d9d3bf6c1b4695a9312adbfd88ae3c/Untitled%202.png)

Veremos que con el parametro -O podemos ver el sistema operativo pero es muy ruidoso y puede que te detecten a nivel de red, en base al TTL es mas normalito y en base a un numero lo podremos ver.

Para ver los puertos abiertos emplearemos nmap con el siguiente comando, y posteriormente podremos ir añadiendo mas opciones si deseamos otro tipo de información.

```bash
nmap $IP -p- --open -T5 -vvv -n -oN $FILE
# -p-       -> Escanea todo el rango de puertos 1-65535
# --open    -> Muestra todos los puertos abiertos
# -T        -> Regula el timing del escaneo 0<5
# -vvv      -> A medida que descubra puertos abiertos los muestra por consola
# -n        -> No aplica resolucion DNS y se demora menos tiempo
# -oN $FILE -> Exporta la informacion a un fichero
```

Para ver las versiones y servicios que corren en puertos especificios podremos usar un par de parametro tambien con nmap:

```bash
nmap -p$PORT1,$PORT2,$PORT3 -sC -sV $IP
```

![Untitled]((Nmap)%20Escaneado%20de%20puertos%2077d9d3bf6c1b4695a9312adbfd88ae3c/Untitled%203.png)

![Untitled]((Nmap)%20Escaneado%20de%20puertos%2077d9d3bf6c1b4695a9312adbfd88ae3c/Untitled%204.png)

### Escaneo de puertos manual

Para agilizar el escaneo siempre podemos nosotros escanear los puertos mediante un fichero creado por nosotros mismos:

```bash
#!/bin/bash
# ./portScan.sh <ip-address>

if [ $1 ]; then
    ip_address=$1
    for port in $(seq 1 65535); do
        timeout 1 bash -c "echo > /dev/tcp/$ip_address/$port" 2>/dev/null && echo "[*] Port $port is open"
    done
    wait
    echo -e "\n[*] Uso: ./portScan.sh <ip-address>\n"
    exit 1
fi
```

### Escaneo de equipos manual

Podemos escanear IP’s dentro de nuestra red mediante otro fichero manual en .sh:

```bash
#!/bin/bash
for i in $(seq 2 254); do
    timeout 1 bash -c "ping -c 1 10.10.10.$i > /dev/null 2>&1" && echo "Host 10.10.10.$i"
done
wait
echo "ACTIVE"
```
