# Instalación de Arch vía UEFI

## Establecer teclado:
Español _latinoamérica_

```~# loadkeys la-latin1 ```

Para otras distribuciones de teclado escribir:

```~# ls /usr/share/kbd/keymaps/**/*.map.gz```

O visitar la documentación oficial de [_Arch Linux_](https://wiki.archlinux.org/index.php/Installation_guide)

## Conectar a Internet:

### Ethernet

Con solo enchufar el cable debe funcionar.

### Wifi

```~# ip link```

Vemos el que empieza con 
[docs](https://wiki.archlinux.org/index.php/Network_configuration/Wireless)

**Comprobar si tenemos internet: **

```~# ping archlinux.org``` o ```~$ ping github.com```

El output debe verse algo así:
``` 
    PING archlinux.org (numeros) ....
    64 bytes from (numeros)
    64 bytes from (numeros)
    64 bytes from (numeros)
    64 bytes from (numeros)
```

CTRL + C para interrumpir


## Establecer zona horaria NTP

```~# timedatectl set-ntp true```

Para corroborar:

```~# timedatectl status```

El output debería ser así:

``` 
               Local time: (Fecha actual) (Minutos) UTC
           Universal time: (Igual a lo anterior en fecha y minutos) UTC
                 RTC time: (Igual a lo anterior)
                Time zone: UTC (UTC,+0000)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no
```

## Crear particiones
### Vamos a hacerlo con 'fdisk'

Para listar las particiones:

```~# fdisk -l ```

El importante es el primero, el que tiene mayor tamaño.

Ahora para ingresar al menú de particiones:

```~# fdisk /dev/sda ```

Deberia haber un output así:

``` Command (m for help): ```

Apretamos *g* para hacer una particion _GPT_ y damos*Enter*.

Ahora apretamos *n* para una nueva partición.

Nos saldra lo siguiente:

```Partition number (1-120, default 1): ``` le damos *Enter* o *1*.

```First sector (2048-16777182, default 2048) ``` le damos a *Enter*.

```Last sector +/-sectors or +/-size{K,M,G,T,P} (2048-16777182, default 16777182): ``` Escribimos:

``` +550M ``` y damos *Enter*

El otput es un mensaje diciendo que se creo una particion del tipo "Linuz filesystem". Lo vamos a cambiar más adelante.

Repetimos. Damos *n* y *Enter*


```Partition number (1-120, default 2): ``` le damos *Enter* o *2*.

```First sector (1128448-16777182, default 1128448) ``` le damos a *Enter*.

```Last sector +/-sectors or +/-size{K,M,G,T,P} (1128448-16777182, default 16777182): ``` Escribimos:

``` +2G ``` y damos *Enter*

Debería salir un output con un "Linux filesystem"

Repetimos una útlima vez. Damos *n* y *Enter*

```Partition number (1-120, default 3): ``` le damos *Enter* o *3*.

```First sector (5322752-16777182, default 5322752) ``` le damos a *Enter*.

```Last sector +/-sectors or +/-size{K,M,G,T,P} (5322752-16777182, default 16777182): ``` Damos *Enter*

Debería salir un output con un "Linux fylesystem" y el espacio restante del disco.

Ahora para cambiar el formato de las primeras 2 particiones:

``` 
Command (m for help): t
Patition number (1-3, default 3): 1
Partition type or alias (type L to list all): 1

Changed type of partition 'Linux filesystem' to 'EFI System'

Command (m for help): t
Patition number (1-3, default 3): 2
Partition type or alias (type L to list all): 19

Changed type of partition 'Linux filesystem' to 'Linux swap'

Command (m for help): w
```

Una vez que salimos de "fdisk" vamos a ..


