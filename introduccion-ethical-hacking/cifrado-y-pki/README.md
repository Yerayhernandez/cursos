# Identificación digital

## Aspectos generales

* **Cifrado con clave simétrica** -> Es una clave que solo conocen el emisor
del mensaje y el receptor del mismo para descifrar el mensaje.

* **Cifrado con clave asimétrica** -> Cada uno de los usuarios tienen dos
claves (privada y pública). La clave privada solamente la conoce el usuario y
la clave pública la conocen todos. Con la clave pública no se puede generar
la clave privada.

## Clave simétrica vs Clave asimétrica

* Clave simétrica:
  - Más rápida
  - Necesarias buenas claves (aleatorias)
  - Necesidad de un canal seguro para transmitir la clave al receptor.

* Clave asimétrica:
  - Mucho más lenta.
  - Algoritmo para generar las parejas robusto.
  - Hay que estar seguro de que la clave pública es la correcta y pertenece al
emisor real.

## Huella digital (hash)

* Mapea un mensaje de **cualquier longitud** en un código de **longitud fija**
* Función irreversible
* El menor cambio en el mensaje provoca un código muy diferente
* Muy difícil pero **no imposible** que con dos mensajes se obtenga el mismo
código
* Ejemplos: MD5, SHA, ...

## Certificado digital

* Documento digital por el que una autoridad atestigua que una clave pública
pertenece a un sujeto. Contiene al menos:
  - Identificación del sujeto
  - Clave pública vinculada
  - Firma (digital) de la autoridad certificadora
