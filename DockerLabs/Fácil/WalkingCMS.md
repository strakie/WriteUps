# WalkingCMS

Link del laboratorio -> [WalkingCMS](https://dockerlabs.es)

## Tags

`eJPT`

## Despliegue

Desplegamos el laboratorio ejecutando el siguiente comando como root. `bash auto_deploy.sh walkingcms.tar`

![Despliegue](../../images/despliegue1.png)

Una vez desplegado el laboratorio hacemos su debido reconocimiento.

## Reconocimiento

Lanzamos un escaneo nmap con los siguientes parámetros: `nmap -p- --open -n -Pn -vvv 172.17.0.2 -oG allPorts`

`-p-` ⮞ Indica que quiere escanear <b>TODOS</b> los puertos.<br>
`--open` ⮞ Modifica el parámetro anterior filtrando por puertos <b>ABIERTOS</b>.<br>
`-n` ⮞ Declara que <b>NO</b> queremos que nos haga resolución DNS. (En estos casos, no es necesario ya que demoraría mucho el escaneo.)<br>
`-Pn` ⮞ <b>Obliga</b> a hacerse el escaneo, independientemente de si la IP está activa o no.<br>
`-vvv` ⮞ Te muestra <b>TODA</b> la información brindable del escaneo. El parámetro se puede calibar por `-v`, `-vv` y `-vvv`, este último indicando que  queremos que nos muestre <b>TODO</b> lo posible.<br>
`-oG` ⮞ Este parametro hace un guardado de toda la información recopilada en formato grepeable, haciendo así una mejor extracción de datos.<br>

![allPorts](../../images/nmapscan.png)

Aparentemente, hay solo 1 puerto abierto, el cual es el 80. Hacemos un segundo escaneo, ahora indicando que nos muestre información detallada sobre el puerto.

`nmap -p80 -sCV 172.17.0.2 -oN targeted`

`-p80` ⮞ Indica que únicamente queremos escanear el puerto 80 (HTTP).

`-sCV` ⮞ Es en realidad tres opciones combinadas:

    -sC ⮞ Usa scripts predeterminados de nmap (NSE - Nmap Scripting Engine) para detectar servicios, vulnerabilidades básicas, etc.

    -sV ⮞ Detecta versiones de los servicios corriendo en los puertos abiertos (por ejemplo, si es un Apache 2.4.52, etc.).

`-oN targeted` ⮞ Guarda el resultado del escaneo en un archivo de texto plano llamado targeted.
(El formato -oN es "normal output", fácil de leer a mano).

![targeted](../../images/targeted.png)

## Página Web

Nos dirigimos a su página web alojada en el puerto <b>80</b>. Esta es la página por defecto de Apache. Procedemos a hacer fuzzing web con gobuster.<br>
`gobuster dir -u https://172.17.0.2/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -t 20 --add-slash`

![gobuster](../../images/gobuster-walkingcms.png)

Nos arroja un estado <b>200</b> en el sub-dominio /wordpress. (El estado 200 significa que existe esa URL y de que podemos acceder a ella.)<br>
Vamos a `https://172.17.0.2/wordpress`. 

![web-invulnerable](../../images/web-invulnerable.png)

Esto nos muestra una página web basada en wordpress con el título "Web Invulnerable". Le pegamos un ojo a la página web y terminamos topando en 