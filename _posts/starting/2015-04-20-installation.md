--- 
published: true 
layout: docs 
title: "Instalación" 
date: 2015-04-20 
permalink: /docs/installation.html 
section: sidebar
category: starting 
category_title: Comencemos 
showInSideBar: true
order: 2
category_info:
  name: installation
  title: Instalación
---

###MANUAL INSTALACION FACTUS 1.1

Este manual guiará paso a paso para la instalación de FACTUS 1.1 en su ordenador. Abrimos en ejecutable **FASTUS1.1-installer.exe** para iniciar la instalación.

IMAGEN

Al abrir el archivo nos muestra la siguiente pantalla de bienvenida

IMAGEN

Al dar click en siguiente nos mostrara el Contrato de Licencia. Si se está conforme, marcamos que aceptamos los términos y condiciones y damos click en siguiente.

IMAGEN

Elegimos la ruta de la instalación (Se recomienda instalar en el directorio por defecto mostrado)

IMAGEN

Durante la instalación de FACTUS 1.0, el asistente le pedirá su aprobación para instalar Microsoft Visual C++ Redistributable Package (x86), esencial para el funcionamiento óptimo de FACTUS 1.0, Aceptamos y damos click en Siguiente y se instalaran los componentes.

Le damos a finalizar y tenemos completada la instalación de FACTUS 1.0

En inicio tendremos algunos archivos de FACTUS 1.0
￼- -
- -
Configuración Factus: Ejecutable de configuración Factus 1.0
Documentación Factus: URL que le redirigirá a la Documentación
Factus.pe: Portal principal de FACTUS
Guía de Usuario : URL Factus con los documentos de ejemplos y/o Guías


Nos vamos al directorio donde se instaló FACTUS 1.0
(El directorio por defecto es C:\Program Files\Factus-1.0)
Como podemos ver se instaló en el directorio correctamente, procedemos a entrar a la carpeta


Ingresando al directorio de la Instalación, podemos visualizar los archivos y directorios de FACTUS 1.0

A continuación describiremos los directorios y archivos que conforman FACTUS 1.0:
- Keystore:
En este directorio se colocan los certificados digitales


- Templates:
En este directorio se encuentran las plantillas de generación de los archivos XML en formato Velocity. Estos archivos pueden ser modificables.


- Unistall Factus.exe : Archivo ejecutable para la desinstalación de FACTUS 1.0
- config.ini:
Este archivo contiene los datos correspondientes del Emisor(Empresa que va a facturar). El formato del config.ini es el siguiente:


Dónde:
TipoDocumento: Es el tipo de documento del Emisor/Empresa. Tipo de documento de
acuerdo a Documentación SUNAT
NumeroDocumento: Es el número de Documento del Emisor/Empresa, en este caso un R.U.C.
NombreComercial: Es el nombre comercial del Emisor/Empresa. RazonSocial: Razón social del Emisor/Empresa.
Ubigeo: Código de Ubigeo del Emisor/Empresa.
País: País del Emisor/Empresa.
Departamento: Departamento del Emisor/Empresa. Provincia: Provincia del Emisor/Empresa
Distrito: Distrito del Emisor/Empresa
Dirección: Dirección del Emisor/Empresa
Certificado: Aquí se colocan los datos de los Certificados Digitales: o FileKeyStore : Directorio del archivo de Certificación Digital o PasswordKeyStore: Contraseña del Certificado Digital
o AliasKey: Alias del Certificado Digital
o PasswordKey: Contraseña del Certificado.
