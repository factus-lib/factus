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

<h2 class="down">MANUAL INSTALACION FACTUS 1.1</h2>

Este manual guiará paso a paso para la instalación de **FACTUS 1.1** en su ordenador. Abrimos en ejecutable **FASTUS1.1-installer.exe** para iniciar la instalación.

<div class="cleaning img-top code">
	
</div>

Al abrir el archivo nos muestra la siguiente pantalla de bienvenida

<div class="cleaning img-top code"><h6 class="down">Pantalla de bienvenida</h6><img src="/assets/images/bienvenida.png"></div>

Al dar click en siguiente nos mostrara el Contrato de Licencia. Si se está conforme, marcamos que aceptamos los términos y condiciones y damos click en siguiente.

<div class="cleaning img-top code"><h6 class="down">Términos y condiciones</h6><img src="/assets/images/licencia.png"></div>

Elegimos la ruta de la instalación (Se recomienda instalar en el directorio por defecto mostrado)

<div class="cleaning img-top code"><h6 class="down">Ruta de instalación</h6><img src="/assets/images/directorio.png"></div>

Durante la instalación de **FACTUS 1.1**, el asistente le pedirá su aprobación para instalar Microsoft Visual C++ Redistributable Package (x86), esencial para el funcionamiento óptimo, Aceptamos y damos click en Siguiente y se instalaran los componentes.

<div class="cleaning img-top code"><h6 class="down">Requerimientos de Optimización</h6><img src="/assets/images/visual.png"></div>

Le damos a finalizar y tenemos completada la instalación de <b>FACTUS 1.1</b>

<div class="cleaning img-top code"><h6 class="down">Instalación terminada</h6><img src="/assets/images/listo.png"></div>

Terminada la instalación,estos son los archivos de inicio:
<ul class="distancia">
<li><b>Configuración Factus:</b> Ejecutable de configuración <b>FACTUS 1.1</b></li>
<li><b>Documentación Factus:</b> URL que le redirigirá a la Documentación</li>
<li><b>Factus.pe:</b> Portal principal de FACTUS</li>
<li><b>Guía de Usuario :</b> URL Factus con los documentos de ejemplos y/o Guías</li>
</ul>
<br>
Nos vamos al directorio donde se instaló <b>FACTUS 1.1</b>
(El directorio por defecto es C:\Program Files\Factus-1.1)
Como podemos ver se instaló en el directorio correctamente, procedemos a entrar a la carpeta


Ingresando al directorio de la Instalación, podemos visualizar los archivos y directorios de <b>FACTUS 1.1</b>

A continuación describiremos los directorios y archivos que lo conforman:

<ul class="distancia">
<li><b>Keystore:</b>En este directorio se colocan los certificados digitales</li>
<li><b>Templates:</b>En este directorio se encuentran las plantillas de generación de los archivos XML en formato Velocity. Estos archivos pueden ser modificables</li>
<li><b>Unistall Factus.exe :</b> Archivo ejecutable para la desinstalación de <b>FACTUS 1.1</b></li>
<li><b>config.ini:</b> Este archivo contiene datos correspondientes al Emisor(Empresa que va a facturar)</li>
</ul>
<br>
El formato del <b>config.ini</b> es el siguiente:

<ul class="distancia">
<li><b>TipoDocumento:</b> Es el tipo de documento del Emisor/Empresa. Tipo de documento de
  acuerdo a Documentación SUNAT</li>
<li><b>NumeroDocumento:</b> Es el número de Documento del Emisor/Empresa, en este caso un R.U.C.</li>
<li><b>NombreComercial:</b> Es el nombre comercial del Emisor/Empresa.</li>
<li><b>RazonSocial:</b> Razón social del Emisor/Empresa.</li>
<li><b>Ubigeo:</b> Código de Ubigeo del Emisor/Empresa.</li>
<li><b>País:</b> País del Emisor/Empresa.</li>
<li><b>Departamento:</b> Departamento del Emisor/Empresa.</li>
<li><b>Provincia:</b> Provincia del Emisor/Empresa</li>
<li><b>Distrito:</b> Distrito del Emisor/Empresa</li>
<li><b>Dirección:</b> Dirección del Emisor/Empresa</li>
<li><b>Certificado:</b> Aquí se colocan los datos de los Certificados Digitales: o FileKeyStore : Directorio del archivo de Certificación Digital o PasswordKeyStore: Contraseña del Certificado Digital
  o AliasKey: Alias del Certificado Digital
  o PasswordKey: Contraseña del Certificado. </li>
</ul>
