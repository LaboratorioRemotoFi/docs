---
sidebar_position: 1
---

# PWM

El proyecto que estamos utilizando para habilitar el uso de los pines de entrada y salida se puede encontrar en [node-rpio](https://github.com/jperkin/node-rpio). Este proyecto soporta el uso de PWM en los pines que tienen habilitada esta funcionalidad por hardware.

## Deshabilitar audio

En este momento hay un problema con el audio y el pwm por lo que primero hay que deshabilitar este en el archivo `/boot/config.txt`. Esto lo podemos hacer editando el archivo como root.

```sh
sudo nano /boot/config.txt
```

Y comentando la línea:

```
# dtparam=audio=on
```

## Incluir la librería y configuración inicial

Para poder utilizar el PWM es necesario que la librería se configure para utilizar el sistema `/mem` en lugar del configurado por defecto `/gpiomem`. Esto lo podemos lograr con las siguientes líneas:

```javascript
var rpio = require("rpio");
rpio.init({ gpiomem: false });
```

Este cambio requiere que el programa sea ejecutado como usuario `root`.

```sh
sudo yarn dev
```

## Habilitar el pin y mandar el dato

Para poder utilizar el pin como PWM es necesario configurarlo así con la función `rpio.open` de la siguiente manera:

```javascript
rpio.open(13, rpio.PWM);
```

Y para colocar el pin en un valor en particular:

```javascript
// rpio.pwmSetData(pin, value);
rpio.pwmSetData(13, 1024);
```

:::caution Cuidado

Esto solo funciona para los pines que tienen la capacidad de usar PWM por hardware, revisar la especificación del raspberry para más detalles.

Los pines para esta librería se usan por número de pin, verificar esto correctamente.

:::

## Otras configuraciones de PWM

Tambien existen otros dos valores que se pueden configurar, el divisor para la frecuencia de PWM y el rango total, estos se puden configurar con:

```javascript
rpio.pwmSetClockDivider(8);
rpio.pwmSetRange(13, 1024);
```
