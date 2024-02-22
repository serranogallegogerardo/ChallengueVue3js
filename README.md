Capsula Challenge - App "vueShoes"
==================================

Descripción
-----------

App de muestra Front-end para evaluar habilidades puntuales.

Características Principales
---------------------------

*   **Tarjeta de Crédito:** Verifica y valida que el número de tarjeta sea válido y que la fecha de vencimiento esté en el futuro.
    
*   **Actualización del Precio en Bitcoin:** La aplicación muestra el precio en Bitcoin y lo actualiza automáticamente cada 5 segundos utilizando una API externa que proporciona el precio en tiempo real, además la información del precio se ve clara y fácilmente visible para el usuario.
    

Requisitos Técnicos
-------------------

Para ejecutar la aplicación, asegúrate de tener Docker instalado.
Si quieres ejecutarlo localmente sin docker debes tener node.js instalado.

Capturas de Pantalla
--------------------

![Captura 1](https://i.ibb.co/R4MGwFz/pre-Pre-Pago.png)
*Primera impresión*

![Captura 2](https://i.ibb.co/dL8hT9F/prePago.png)
*Rellenando los datos*

![Captura 3](https://i.ibb.co/1LmzvPR/postPago.png)
*Pago completado*

Instalación
-----------

Local sin docker:

`npm install`
`npm run build`
`npm run preview`

Si ya tienes docker no debes preocuparte por la instalación.

Uso
---

Para ejecutar el proyecto rapidamente aqui el .tar:
https://drive.google.com/file/d/1OMKhglrS8NM_dzg9HQqSKuYMVxrlMl7y/view?usp=sharing

Rellenar los datos y disfrutar, esperar a ver el cambio del precio en BTC.

Local sin Docker:
`http://localhost:4173/`
Usando Docker:
`http://localhost:5000/`


Créditos
--------

    * svg: https://github.com/aaronfagan/svg-credit-card-payment-icons
    * api precio bitcoin: https://api.blockchain.com/v3/#/unauthenticated/getTickers
    * creditcard.js: https://contaazul.github.io/creditcard.js/
    * font: https://fonts.google.com/specimen/Poppins


Pruebas Manuales
----------------

Fuente: [VCC Generator](https://www.vccgenerator.org/)

**Datos de Prueba CC VALID:**

_Funcionan:_

*   **Visa**
    
    *   4338 1037 6667 2528
    *   08/24
    *   290
*   **Amex / American Express**
    
    *   377800412811174
    *   02/27
    *   2753
*   **Mastercard**
    
    *   5471 7175 1937 2153
    *   09/27
    *   668
*   **Diners**
    
    *   38948717337071
    *   02/38
    *   335

**TARJETAS QUE NO DEBERÍAN FUNCIONAR**

*   **JCB**
    
    *   3567029229152507
    *   10/29
    *   208
*   **Discover**
    
    *   6011594826942936
    *   12/23
    *   6942