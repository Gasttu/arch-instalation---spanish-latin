# Instalación de Arch vía UEFI

## Establecer teclado:
Español _latinoamerica_

```~# loadkeys la-latin1 ```

Para otras distribuciones de teclado escribir:

```~# ls /usr/share/kbd/keymaps/**/*.map.gz```

O visitar la documentación oficial de [_Arch Linux_](https://wiki.archlinux.org/index.php/Installation_guide)

## Conectar a Internet:

### Ethernet

Con solo enchufar el cable debe funcionar.

### Wifi

``` agregar comandos para el wifi```

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

