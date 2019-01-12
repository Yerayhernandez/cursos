# Netfilter e Iptables

**Netfilter** es un framework de linux que permite interceptar y manipular
paquetes de red. **Iptables** es su componente más popular y actúa como
cortafuegos.

## 1. Firewall
### 1.1. Descripción del Firewall (Cortafuegos)

**Un cortafuegos es un sistema** usado para *separar una subred protegida* de otra
de riesgo estableciendo políticas de control entre ambos entornos.

El **filtrado de paquetes** es un proceso que deniega o permite el flujo de
información y datos entre la red que se desea proteger (interna) del resto.

* Trabajan sobre las **cabecera de los paquetes IP.**

* Según las reglas podrá realizar distintos tipos de acciones (aceptar, rechazar..)
sobre los paquetes.

* Tipos de filtrado de paquetes:
  - **Estático:** analiza las cabecera de cada paquete sin establecer relación
  con otros.
  - **Dinámico:** permite el control de un flujo de datos relacionados dentro de una
  misma conexión TCP o varias conexiones haciendo uso de la memoria.

## 2. NAT

Mecanismo que altera las cabecera de los paquetes IP soliendo cambiar las
direcciones IP y puertos origen o destino.

* **Source NAT (SNAT):** Se altera el origen del datagrama, realizado después del
encaminamiento del mismo y antes de su reenvío.
* **Destination NAT (DNAT):** Se altera el destino del datagrama, realizado
antes del encaminamiento del mismo.

## 3. Procesamiento de paquetes

### 3.1. Filtado de paquetes

Con Netfilter e Iptables se puede realizar:

* Filtrado de paquetes
* Traducción de direcciones y puertos NAT
* Manipulación sobre datagramas IP
* Seguimiento de conexiones

Netfilter permite el uso de distintas tablas de IP para el filtrado:
*nat, filter, mangle y raw*

Funciona con IPv4 e IPv6

### 3.2. Cadenas (chains)

Netfilter gestiona el filtrado mediante tablas organizadas en cadenas y éstas
a su vez compuestas por reglas.

* Las cadenas son agrupaciones de reglas que se aplican a los paquetes en
momentos concretos.

- **INPUT:** acción a realizar cuando un paquete coincide con la regla a
la entrada de la interfaz. Se plica a paquetes destinados a la propia máquina.
- **OUTPUT:** acción a realizar cuando un paquete coincide con la regla, a
la salida de la interfaz. Se aplica a paquetes originados en la propia
máquina.
- **FORWARD:** cuando un paquete se envía de una interfaz a otra. Cadena
intermedia entre las dos siguientes.
- **PREROUTING:** primera acción a realizar antes de que el paquete entre en
el sistema.
- **POSTROUTING:** acción a realizar justo antes de enviar el paquete a la
interfaz destino.

![01](./images/Seleccion_001.png)

### 3.3. Tablas

Tipo de procesamiento que se debe aplicar a los paquetes.

* Tipos: filter, mangle, nat y raw

- **FILTER:** filtrado general de paquetes. Decido los paquetes que pasan
y los que no. Compuesta por las cadenas *input, output y forward*.
- **NAT:** traducción de direcciones. Permite cambiar las direcciones origen
y destino de los datagramas. Compuesta por las cadenas *prerouting,
postrouting y output*.
- **MANGLE:** analiza el paquete y lo etiqueta para que reciba un tratamiento
concreto. Compuesta por las cadenas *prerouting, input, forward y output*.

## 4. Reglas

Sintaxis del comando *iptables*:

- iptables [-t table] COMANDO CADENA condición acción [opciones]
|---------|----------|-------|------|---------|------|----------|
    1           2        3      4        5       6        7

1. Comando *iptables*
2. Tabla a usar: *filter, nat, mangle*
3. Comando sobre la cadena: *insertar, modificar, eliminar, reglas...*
4. Cadena a usar: *input, output, forward, prerouting o postrouting*
5. Condición: criterios que deben cumplir los campos
6. Acción a realizar (para los que cumplan la condición previa)
7. Opciones extra para ajustar la acción
