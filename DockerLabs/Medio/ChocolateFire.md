# ChocolateFire

### Tags: 
`eJPTv2`

## Reconocimiento

Al haber desplegado el laboratorio haremos un escaneo completo de todos los puertos, para esto, emplearemos el comando `nmap -p- --open -n -Pn -vvv 172.17.0.2 -oG allPorts`.

![allPorts](https://github.com/TerrorAterrador/WriteUps/assets/146730674/edb8225a-071e-47d2-ba92-8cb06fa05d83)

Habremos percibido un puerto abierto un tanto curioso, el cual es el <b>9090</b>, llamado "<b>zeus-admin</b>".

![puertos-allPorts](https://github.com/TerrorAterrador/WriteUps/assets/146730674/edb8225a-071e-47d2-ba92-8cb06fa05d83)

## Página web

Probamos si este está alojando una página web ingresando a `172.17.0.2:9090`. Al ingresar, nos topamos con un panel de login de un tal servicio "openfire".

![panel-login](https://github.com/TerrorAterrador/WriteUps/assets/146730674/edb8225a-071e-47d2-ba92-8cb06fa05d83)

He intentado ingresar con las credenciales `user: admin password: admin` y me ha dejado ingresar.

![server-admin](https://github.com/TerrorAterrador/WriteUps/assets/146730674/edb8225a-071e-47d2-ba92-8cb06fa05d83)

He ojeado un poco y por aquí se pueden hacer cosas, pero a nosotros no nos interesan estos metodos, ya que, nuestro objetivo, como nos ha recomendado Mario (El creador de la máquina) es hacer intrusión con Metasploit.

## Intrusión con Metasploit

Ejecutaremos Metasploit y buscaremos un exploit para el servicio "openfire". Utilizaremos el que tiene plugin RCE.

![msfconsole](https://github.com/TerrorAterrador/WriteUps/assets/146730674/edb8225a-071e-47d2-ba92-8cb06fa05d83)

Luego, declararemos las siguientes variables:

![variables-msfconsole](https://github.com/TerrorAterrador/WriteUps/assets/146730674/edb8225a-071e-47d2-ba92-8cb06fa05d83)

Dejando así las opciones del exploit:

![options-msfconsole](https://github.com/TerrorAterrador/WriteUps/assets/146730674/edb8225a-071e-47d2-ba92-8cb06fa05d83)

Corremos el exploit y ya nos abre una sesión root.

![run&root](https://github.com/TerrorAterrador/WriteUps/assets/146730674/edb8225a-071e-47d2-ba92-8cb06fa05d83)