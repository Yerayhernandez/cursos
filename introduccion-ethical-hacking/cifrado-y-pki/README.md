# 1. Identificación digital

## 1.1. Aspectos generales

* **Cifrado con clave simétrica** -> Es una clave que solo conocen el emisor
del mensaje y el receptor del mismo para descifrar el mensaje.

* **Cifrado con clave asimétrica** -> Cada uno de los usuarios tienen dos
claves (privada y pública). La clave privada solamente la conoce el usuario y
la clave pública la conocen todos. Con la clave pública no se puede generar
la clave privada.

## 1.2. Clave simétrica vs Clave asimétrica

* Clave simétrica:
  - Más rápida
  - Necesarias buenas claves (aleatorias)
  - Necesidad de un canal seguro para transmitir la clave al receptor.

* Clave asimétrica:
  - Mucho más lenta.
  - Algoritmo para generar las parejas robusto.
  - Hay que estar seguro de que la clave pública es la correcta y pertenece al
emisor real.

## 1.3. Huella digital (hash)

* Mapea un mensaje de **cualquier longitud** en un código de **longitud fija**
* Función irreversible
* El menor cambio en el mensaje provoca un código muy diferente
* Muy difícil pero **no imposible** que con dos mensajes se obtenga el mismo
código
* Ejemplos: MD5, SHA, ...

## 1.4. Certificado digital

* Documento digital por el que una autoridad atestigua que una clave pública
pertenece a un sujeto. Contiene al menos:
  - Identificación del sujeto
  - Clave pública vinculada
  - Firma (digital) de la autoridad certificadora

# 2. PKI (Infraesctructura de clave pública)

Es una combinación de elementos que permiten cifrar, firmar y conseguir el
no repudio de comunicaciones electrónicas.

## 2.1. Elementos funcionales de una PKI

* Básicos
  - Autoridad de certificación (CA)
  - Autoridad de registro (RA)
  - Almacén de certificados y claves

* Opcionales
  - Autoridad de sellado de tiempo (TSA)
  - Servidor de revocación

### 2.1.1. Autoridad de certificación (CA)

* Tercero en quien se confía para:
  - Firmar y publicar certificados
  - Revocar certificados y publicar la revocación
  - Recoge funciones de gestión y fechado.

* Pueden ser públicas, privadas o individuales

* Firma los certificados su clave privada
  - Para confiar en su pública se certifica a si misma o la certifica otra CA.
Su clave pública viene preinstalada en el S.O o navegador en algunos casos o
será necesario descargarla e instalarla manualmente.

#### 2.1.2. Organización de una CA

* CA única
  - Facil de mantener pero punto vulnerable

* Jerarquía de CA
  - Arbol de confianza, cada CA certifica al nivel superior
  - La CA raíz se certifica a sí misma.

* Malla de CA
  - Las CA se certifican mutuamente.
  - El sujeto confía en su CA.

### 2.1.3. Autoridad de registro (RA)

* Autoridad delegada para algunas funciones:
  - Recibir solicitudes de certificados.
  - Generar las claves
  - Verificar la identidad del solicitante.
  - Entregar el certificado al solicitante.

### 2.1.4. Almacén de certificados y claves

* Los certificados son públicos:
  - Deben estar siempre disponibles y guardarse en histórico.

* Debe poderse comprobar que no están revocados
* Las claves privadas sí deben estar protegidas:
  - Si se comprometen se revocará el certificado.

### 2.1.5. Autoridad de sellado de tiempo

* La TSA proporciona sellos de tiempo:
  - Necesita que se registre el fechado
  - Documento que se asocia la huella digital de un documento a una fecha
y hora concreta
  - Permite el no repudio

### 2.1.6. Servidor de revocación

* Lugar donde se almacena la CRL (Lista de Revocación de Certificados)
  - Lista de números de serie que han sido revocados, ya no son válidos y en
los que no debe confiar ningún usuario del sistema.

## 2.2. Procedimientos

* Básicos
  - Emisión de certificado
  - Almacenamiento y uso de certificado
  - Renovación o expiración de cetificado
  - Revocación de certificado

* Opcionales
  - Sellado de tiempo.

### 2.2.1. Emisión del certificado

* Pasos:
  - Solicitud en la RA
  - Generación del par de claves, requiere un muy buen generador de números
aleatorios.
  - Verificación de identidad, puede ser presencial o no presencial.
  - Creación y entrega del certificado, tarea exclusiva de la CA y la entrega
depende del procedimiento de generación de clave y el nivel de seguridad del
certificado.
  - Publicación y respaldo del certificado. Publicado por parte de la CA
o del solicitante en almacenes públicos o diseminación con cada uso y copia
de respaldo en el almacén.

### 2.2.2. Almacenamiento y uso

* Almacenamiento
  - Solo la clave privada precisa protección

* Uso: validación del certificado
  - Debe estar vigente en plazo de validez sin estar revocado
  - La CA es de confianza para quien lo verifica
  - Las firmas son válidas
  - Su uso consistente con su política

### 2.2.3. Expiración, Renovación

* Expiracion: se agoa el plazo de validez, no requiere acción
* Actualización: solo de plazo de validez
* Renovación: También de claves
