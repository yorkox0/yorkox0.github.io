---
title:  "deauthAttack"
---
# ¿Que haces entrando aquí? 
# Vaya vaya, con que ahora quieres ser un Black Hat...

# Bueno pues estas en el lugar indicado, hace poco creé un file llamado 'deauth-attack.sh' el cual te permitía realizar ataques de deautenticación a cualquier cliente de una red.
## Os explico el funcionamiendo:

```bash
git clone https://github.com/yorkox0/deauth-attack
cd deauth-attack
chmod +x *.sh
sudo bash deauth-attack.sh
```

## Al inicio del script tendreis que seleccionar la antena de red inalambrica preferida para realizar el ataque, en mi caso seleccionaré 'wlan1'
## Seguidamente se pondrá la antena en modo monitor pasandose a llamar 'wlan1mon'

![img1](https://i.ibb.co/cLTppt3/Captura-de-pantalla-2022-09-05-12-53-38.png)

## El siguiente paso se trata de escanear todas las redes disponibles y seleccionar la que vamos a 'atacar'
## Tendremos que recordar el BSSID de la red i el canal.

![img2](https://i.ibb.co/YRR1DjT/Captura-de-pantalla-2022-09-05-12-54-34.png)

## Una vez seleccionado seguiremos realizando un escaneo de los dispositivos conectados a dicha red i seleccionaremos el BSSID del dispositivo que realizar el ataque.

![img3](https://i.ibb.co/4Y0SHCT/Captura-de-pantalla-2022-09-05-12-55-04.png)

## ¡Y finalmente ya estaremos expulsando el dispositivo de dicha red con nuestro script!
