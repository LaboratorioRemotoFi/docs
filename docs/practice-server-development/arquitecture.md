---
sidebar_position: 2
---

# Cómo funciona

La interfaz web utiliza una conexión de webSockets para iniciar la comunicación con la práctica, en la base de datos de _Webapp_ se tiene la lista de prácticas que incluye:

- id
- Nombre de la práctica
- IP y puerto de conexión

La parte importante aquí es la dirección IP y el puerto de conexión de la práctica. Al momento de que el alumno quiera iniciar una práctica la interfaz solicita una conexión de webSocket a la dirección guardada en la base de datos.

El servidor instalado en la práctica recibe la solicitud y si la conexión es correcta envía la información _metadata_ de la práctica, este archivo es muy importante ya que aquí se definen varios aspectos de la práctica como instrucciones, dispositivos, acciones, etc. Esta información es recibida en la interfaz con la cual se construyen los elementos que aparecen en pantalla.

El servidor tiene un estado interno para indicar a la interfaz que ya está listo para iniciar la práctica. Una vez iniciada la práctica la interfaz muestra los pasos, acciones disponibles para ese paso e información que la práctica está enviando. El alumno puede ver los datos relevantes así como el vídeo de las cámaras web habilitadas.

El servidor de la práctica estará escuchando por nuevos comandos y enviando la información relevante hasta que el alumno termine todos los pasos de la práctica y esta termine en cuyo momento se cerrará la conexión.

## Hardware soportado

Este desarrollo requiere de un dispositivo donde se pueda tener acceso a internet y node js disponible por lo que no es posible instalarlo en una arduino o similares sino que se necesitará de un dispositivo que tenga un sistema operativo como una computadora o una raspberry pi.

## Notas

- El servidor de webSockets se realiza con la biblioteca socket.io la cual proporciona varias características extra de un webSocket normal como la re conexión automática y eventos estandar
