--- 
published: true 
layout: docs 
title: "Funcionalidad de la API" 
date: 2015-04-20 
permalink: /docs/functionality.html 
section: sidebar
category: starting 
category_title: Comencemos 
showInSideBar: true
order: 2
category_info:
  name: functionality
  title: Funcionalidad de la API
---

<h1 class="down">{{ page.title }}</h1>

Factus API Desktop para aplicaciones Desktop, es una librería desarrollada en C++ (COM) para sistemas operativos Windows de 32 y 64 bits. Esta disponible para Windows XP, Windows Vista, Windows 7, Windows 8 y Windows 8.1 en 32 y 64 bits.

<h2><center>Gráfico de clases</center></h2>
<img src="/assets/images/diagrama.png" alt=""/>
<br/><br/>
Factus expone los siguientes objetos:   

**Comprobante**, es el objeto principal que contiene la información del comprobante electrónico(Boletas, Facturas, Notas de Crédito y Notas de Débito), contiene información de cabecera, participantes, totales y objetos como Items, Impuestos, Documentos de Referencia, Montos Adicionales, Propiedades Adicionales y Atributos personalizados.

**Participante**, es el objeto que es usado para identificar al emisor y cliente(Receptor), este objeto no necesita ser inicializado y se usa de la siguiente forma: _comprobante.Emisor.TipoIdentidad = "6"_ y _comprobante.Cliente.TipoIdentidad = "6"_. Contiene datos obligatorios y opcionales.

<ul class="distancia">
<li>Item,</li> 
<li>Impuesto,</li>
<li>DescuentoCargo,</li>
<li>MontoAdicional,</li>
<li>PropiedadAdicional,</li>
<li>DocumentoReferencia,</li>
</ul>
<br>

**Respuesta**, este objeto es devuelto al invocar al método _Generar()_, contiene información como resultado de la generación del comprobante electrónico, cuando el código de error es cero, la generación fue correcta en caso contrario indica el error y mensaje de error. Por otro lado devuelve información sobre la ubicación del archivo XML generado, la firma, el hash y la imagen del código de barra.


A continuación mostramos un ejemplo en sintaxis C#, una factura con 1 item en el que registramos la glosa de monto en letras y la base imponible según especificación de la SUNAT.

Para utilizar **Factus COM** el primer paso es instanciar la clase principal Comprobante(Hay ejemplos para otros lenguajes):

<?prettify lang=C#?>
<pre class="prettyprint">

            Factus.Comprobante c = new Factus.Comprobante();
 </pre>

*****************

Identificamos los datos básicos del comprobante como el **_tipo de comprobante_**, en nuestro ejemplo al ser Factura se colocará “01”. ([_Según Documentación SUNAT – Tipos de documento_](https://s3.amazonaws.com/insc/Libros+y+Registros+Electronicos/Anexos+RS+199_2014/Nuevo+Anexo+8+-+Cat%C3%A1logos.pdf))   
El campo **_serie correlativo_** es el número asignado por el Emisor, este campo es el identificador único del comprobante.   
Colocamos también la **_fecha de emisión_** del comprobante en formato YYYY-MM-DD.   
Registramos el **_tipo de moneda_** del comprobante.   

<?prettify lang=C#?>
<pre class="prettyprint" >

            c.TipoComprobante = “01”;
            c.SerieCorrelativo = “F001-101”; 
            c.FechaEmision = “2015/01/01”; 
            c.TipoMoneda = "PEN"; 
 </pre>

*****************

Lo siguiente que haremos, es instanciar la clase **Participante**, ya que aquí colocaremos los datos tanto del Emisor como del Cliente.  


Colocamos el numero del **_tipo de documento del Emisor_**, según Documentación SUNAT (_Catalogo Nro.6_).([Ver Documentación SUNAT](https://s3.amazonaws.com/insc/Libros+y+Registros+Electronicos/Anexos+RS+199_2014/Nuevo+Anexo+8+-+Cat%C3%A1logos.pdf))

**Procedemos a llenar los demás campos del Emisor:**

<li><i>Numero identidad emisor:</i> Numero de identidad del emisor del Comprobante.</li>

<li><i>Nombre Comercial Emisor:</i> Nombre comercial del emisor del Comprobante.</li>

<li><i>Razon Social Emisor:</i> Razón social del emisor del Comprobante.</li>

<li><i>Ubigeo Emisor:</i> Código del UBIGEO del emisor del Comprobante.</li>([Según Catalogo Nro.13 Documentación SUNAT.](https://s3.amazonaws.com/insc/Libros+y+Registros+Electronicos/Anexos+RS+199_2014/Nuevo+Anexo+8+-+Cat%C3%A1logos.pdf))
([_Ver relación de UBIGEO para Lima_](http://www.indeci.gob.pe/oit/cua_ubigeo.pdf))

<li><i>País Emisor:</i> Código del País del emisor del Comprobante.</li>

<li><i>Departamento Emisor:</i> Departamento del emisor del Comprobante.</li>

<li><i>Provincia Emisor:</i> Provincia del emisor del Comprobante.</li>

<li><i>Distrito Emisor:</i> Distrito del emisor del Comprobante.</li>

<li><i>Dirección Emisor:</i> Dirección detallada del emisor del Comprobante.</li>
<br>

<?prettify lang=C#?>
<pre class="prettyprint">

            c.Emisor.TipoIdentidad = “6”;
            c.Emisor.NumeroIdentidad = “20543314529”;
            c.Emisor.NombreComercial = “ComplexLess”;
            c.Emisor.RazonSocial = “ComplexLess S.A.C.”;
            c.Emisor.Ubigeo =  "150141”;
            c.Emisor.Pais = "PE";
            c.Emisor.Departamento = "Lima”;
            c.Emisor.Provincia = “Lima”;
            c.Emisor.Distrito = “Surquillo”;
            c.Emisor.Direccion = “Av. Aramburu 856 Of. 302”;
 </pre>

**********

Ya habiendo registrado los datos del emisor, instanciamos la clase **Participante** nuevamente, para poder registrar los datos del Cliente.

Colocamos el numero del **_tipo de documento del Cliente_**, en este caso para el Documento Nacional de Identidad (DNI), se colocará _“1”_ ([Según Catalogo Nro.6 Documentación SUNAT](https://s3.amazonaws.com/insc/Libros+y+Registros+Electronicos/Anexos+RS+199_2014/Nuevo+Anexo+8+-+Cat%C3%A1logos.pdf))

<br/>**Procedemos a llenar los demás campos del Cliente:**

<ul class="distancia">
<li><i>Numero identidad cliente:</i> Numero de identidad del cliente.</li>

<li><i>Razón Social cliente:</i> Razón Social del cliente.</li>

<li><i>País cliente:</i> Código del país del cliente.</li>

<li><i>Distrito cliente:</i> Distrito del cliente.</li>

<li><i>Dirección cliente:</i> Dirección detallada del cliente.</li>
</ul>

<?prettify lang=C#?>
<pre class="prettyprint">

            c.Cliente.Tipoidentidad = "1"; 
            c.Cliente.NumeroIdentidad = “09574547”;
            c.Cliente.RazonSocial = "SUNAT";
            c.Cliente.Pais = "PE";
            c.Cliente.Distrito = "San Isidro";
            c.Cliente.Direccion = "Av los Sauces 321 Lince";
  </pre>

*************

Luego de haber registrado al Emisor y al Cliente, procedemos a registrar los campos de los Items.
Como se sabe, una Factura puede contener varios items, para este ejemplo solo añadiremos un item.


Para esto, procedemos a instanciar la clase Item.

<?prettify lang=C#?>
<pre class="prettyprint">

            Factus.Item it = c.NuevoItem(); 
 </pre>


En este caso el campo _**id**_ se registra de manera correlativa de acuerdo al numero de ítems que posea el comprobante.

Como en el caso anterior, completamos los campos del item: Cantidad, Descripción, Código del Producto, Precio Unitario, Base Imponible, Tipo precio e Impuesto Total de cada Ítem.

<?prettify lang=C#?>
<pre class="prettyprint">
          
            it.Id = “1”;
            it.Cantidad = 10;
            it.Descripcion = ”Televisor LG Full HD “;
            it.CodigoProducto = "10234";
            it.PrecioUnitario = 11.80;
            it.BaseImponible = 118.00
            it.TipoPrecio = "01";
            it.TotalImpuesto = ”18.00”;
 </pre>

Antes de que vayamos a agregar el _item_ a nuestra Factura, tenemos que tener en cuenta que cada _**Item**_, posee un _**impuesto**_, asi que:

_**Instaciaremos la clase Impuesto:**_

<?prettify lang=C#?>
<pre class="prettyprint">

            Factus.Impuesto imp = it.NuevoImpuesto();
 </pre>

Procedemos a registrar los campos del impuesto por item, en este caso supongamos que el item tenga como tipo de impuesto a "IGV". En este caso como es "IGV" se registra el campo **Id = “VAT”** , el campo **Nombre_ = “IGV”** y para este caso **SunatId = "1000"**.([Ver Catalogo Nro. 5 SUNAT para mayor información](https://s3.amazonaws.com/insc/Libros+y+Registros+Electronicos/Anexos+RS+199_2014/Nuevo+Anexo+8+-+Cat%C3%A1logos.pdf)).  
Hay que tener en cuenta de que un _item_ puede poseer varios _impuestos_, pero en este caso añadiremos un impuesto como ejemplo:

<?prettify lang=C#?>
<pre class="prettyprint">

            imp.Id = “VAT”;
            imp.Nombre = “IGV”;
            imp.SunatId = “1000”;
            imp.BaseImponible = 100.00;
            imp.TotalImpuesto = 18.00;
            imp.Porcentaje = 18;
 </pre>

_Después de haber registrado los campos agregamos el impuesto del ítem asi:_


<?prettify lang=C#?>
<pre class="prettyprint">

            it.AgregarImpuesto(imp);
 </pre>

*************

Cada Item tendrá un Descuento o un Cargo adicional en la Factura, aquí también cada item puede poseer varios _cargos_ o _descuentos_ según se decida aplicar, entonces:

<br>
_**Procedemos a instanciar la clase DescuentosCargos:**_
<br>

<?prettify lang=C#?>
<pre class="prettyprint">

            Factus.DescuentoCargo desCarIt = it.NuevoDescuentoCargo();
 </pre>


Y registramos los campos, donde:  
_**IdCd**_ es el identificador de los descuentos o cargos según se registre en el comprobante.  
_**MontoCd**_ es el monto de los descuentos o cargos según sea el caso.

<?prettify lang=C#?>
<pre class="prettyprint">

            desCarIt.IdCd = 1;  /* Para Cargos: id = 1, y para Descuentos: id = 2 */
            desCarIt.MontoCd= 180.20;
 </pre>
<br>

_Agregamos el descuento o cargo del ítem:_

<?prettify lang=C#?>
<pre class="prettyprint">

            it.AgregarDescuentoCargo(desCarIt);
 </pre>
<br>

_Finalmente procedemos a agregar este Ítem con el impuesto y Descuento o cargo del mismo._

<?prettify lang=C#?>
<pre class="prettyprint">

            c.AgregaItem ( it );
 </pre>


***********
<br>


Una vez registrado los impuestos  de cada Ítem , se sabe que tambien existe un impuesto a nivel general en la factura, para esto vamos a registrar el Impuesto General.  
Debemos recordar que pueden existir tambien varios impuestos a nivel general en la Factura, para este ejemplo añadiremos uno sólo.
 

_**Instanciamos la clase Impuesto (Impuesto General)**_

<?prettify lang=C#?>
<pre class="prettyprint">

            Comprobante.Impuesto impG = new Comprobante.Impuesto();
 </pre>

<br>
Y registramos los campos, donde:  
Como en el ejemplo se calcularon los items con "IGV" entonces, se registra el campo **Id = “VAT”**, el campo **Nombre = “IGV”** y **SunatId = “1000”**.([Ver Catalogo Nro. 5 SUNAT para mayor información](https://s3.amazonaws.com/insc/Libros+y+Registros+Electronicos/Anexos+RS+199_2014/Nuevo+Anexo+8+-+Cat%C3%A1logos.pdf)).  
El campo **TotalImpuesto** es la suma de los impuestos individuales de cada Ítem.  

<?prettify lang=C#?>
<pre class="prettyprint">

            impG.Id = ”VAT”;
            impG.SunatId = ”1000”;
            impG.Nombre = ”IGV”;
            impG.TotalImpuesto = 72.0;
 </pre>


 _Agregamos el impuesto general de la factura._

<?prettify lang=C#?>
<pre class="prettyprint">

            c.AgregarImpuesto ( impG );
 </pre>


 ************************************************


<br>
Al igual que los impuestos, también existen los Descuentos/Cargos a nivel general en la factura.
(Pueden existir varios _descuentos_ o _cargos_ en la factura a nivel general).  

_**Instanciamos la clase DescuentosCargos**_

<?prettify lang=C#?>
<pre class="prettyprint">

            Comprobante.DescuentosCargos desCarG = new Comprobante.DescuentosCargos();                                                            </pre>


<br>

 Y registramos los campos, donde:  
_**IdCd**_ es el identificador de los descuentos o cargos según se registre en el comprobante.  
_**MontoCd**_ es el monto de los descuentos o cargos según sea el caso.  


<?prettify lang=C#?>
<pre class="prettyprint">

            desCarG.IdCd = 2;         /*  Para Cargos: id = 1, y paraDescuentos: id = 2  */
            desCarG.MontoCd= 202.30;
 </pre>


_Y se procede a agregar el descuento o cargo general en el Comprobante._
 
<?prettify lang=C#?>
<pre class="prettyprint">

            c.AgregarDescuento ( desCarG );
 </pre>


************************************************

<br><br>
_**A continuación instanciamos la clase Monto adicional**_

<?prettify lang=C#?>
<pre class="prettyprint">

             Comprobante.MontoAdicional monto = new Comprobante.MontoAdicional();
 </pre>


Y registramos los campos:

MontoAdicional tiene como campos a _ID_, en este caso se coloca el **Id = “1001”** que es el identificador para el _Total valor de venta por Operación Gravada con el IGV_([Ver catalogo Nro. 14 Documentación SUNAT](https://s3.amazonaws.com/insc/Libros+y+Registros+Electronicos/Anexos+RS+199_2014/Nuevo+Anexo+8+-+Cat%C3%A1logos.pdf)).  
Y luego se procede a colocar el **Nombre** del monto adicional, **Monto Referencial**, **Importe total**, **Porcentaje** y **Monto total**.


<?prettify lang=C#?>
<pre class="prettyprint">

             monto.ID =  “1001”;
             monto.Nombre = “Monto adicional 1 ”;
             monto.MontoReferencial =  20.00;
             monto.ImporteTotal =  18.00;
             monto.Porcentaje = 18.00;
             monto.MontoTotal =  100.00; 
 </pre>
  

<br>

_Al completar los campos, se procede a registrar el Monto Adicional al comprobante._



<?prettify lang=C#?>
<pre class="prettyprint">

            c.AgregarMontoAdicional ( monto );
 </pre>


 ************************************************



<br><br>

_**Instanciamos la clase PropiedadAdicional**_  
(Donde puede registrarse informacion de cualquier tipo).


<?prettify lang=C#?>
<pre class="prettyprint">

             Comprobante.PropiedadAdicional propiedad = new Comprobante.PropiedadAdicional();                               </pre>



Y registramos los campos:

La clase PropiedadAdicional tiene como campos a _ID_ , _Nombre_ y _Valor._  
En este ejemplo se coloca en **ID = “9999”** que concierne a “Otros”. ([Según Documentación SUNAT](https://s3.amazonaws.com/insc/Libros+y+Registros+Electronicos/Anexos+RS+199_2014/Nuevo+Anexo+8+-+Cat%C3%A1logos.pdf)), luego se coloca el **Nombre**  y el **Valor** del concepto adicional.



<?prettify lang=C#?>
<pre class="prettyprint">

             propiedad.ID = “9999”;
             propiedad.Nombre  = “Propiedad Adicional 1”;
             propiedad.Valor = “Valor de propiedad adicional”;
  </pre>




_Registramos la propiedad adicional en el comprobante._

<?prettify lang=C#?>
<pre class="prettyprint">

              c.AgregarPropiedadAdicional ( propiedad );
 </pre>


************************************************




<br><br>
_**Instanciamos la clase DocumentoReferencia**_  
(Podemos añadir un documento de referencia a nuestra factura, por ejemplo, una Guía de Remisión).

<?prettify lang=C#?>
<pre class="prettyprint">

          Comprobante.DocumentoReferencia documento = new Comprobante.DocumentoReferencia();
 </pre>


Y registramos los campos, donde:  
**Id** es el numero del documento de referencia.  
**TipoDocumento** es el código del tipo de documento de referencia.([Ver catalogo Nro. 01 Documentación SUNAT](https://s3.amazonaws.com/insc/Libros+y+Registros+Electronicos/Anexos+RS+199_2014/Nuevo+Anexo+8+-+Cat%C3%A1logos.pdf)).  
**Fecha** es la fecha del documento de referencia.  
**DescripcionTipoDocumento** es la descripción del documento que se esta añadiendo como referencia.


<?prettify lang=C#?>
<pre class="prettyprint">

              documento.Id = "0044423"
              documento.Fecha = "2015/03/10"
              documento.TipoDocumento = "09"
              documento.DescripcionTipoDocumento = "Guía de remisión"
 </pre>

<br>
 _Agregamos el documento de referencia a la factura_

<?prettify lang=C#?>
<pre class="prettyprint">

             c.AgregarDocumentoReferencia( documento );
 </pre>



************************************************

<br><br>
Ya registrado los campos anteriores mencionados, se procede a registrar las cantidades totales de la factura como muestra a continuacion: 


<br>
<li>Total Cargos:</li> Importe total de cargos aplicados al total de la factura.
<?prettify lang=C#?>
<pre class="prettyprint">

            c.TotalCargos = "130.50"; 
  </pre>


<li>Total Descuento:</li> Total de los descuentos aplicados al total de la factura
<?prettify lang=C#?>
<pre class="prettyprint">

            c.TotalDescuento = "34.20"; 
  </pre>


<li>Total Impuesto:</li> Importe total de los impuestos aplicados en la factura
<?prettify lang=C#?>
<pre class="prettyprint">

            c.TotalImpuesto = "34.20"; 
  </pre>


<li>Importe Total:</li> Importe total a pagar 
<?prettify lang=C#?>
<pre class="prettyprint">

            c.ImporteTotal = "3024.20"; 
  </pre>
<br/><br/> 

*****************



Podemos agregar a nuestra factura otros atributos de tipo monetario, entonces:

_**Invocamos al método Otro Atributo**_


El método AgregarOtroAtributo tiene como parámetros el ID = “1000” ([Ver catalogo Nro. 15 Documentación SUNAT](https://s3.amazonaws.com/insc/Libros+y+Registros+Electronicos/Anexos+RS+199_2014/Nuevo+Anexo+8+-+Cat%C3%A1logos.pdf)), y el Valor, en este caso la Glosa expresado en letras el monto total de la Factura.
(Tengamos en cuenta que en este método pueden agregarse varios atributos)

<?prettify lang=C#?>
<pre class="prettyprint">

              c.AgregarOtroAtributo ( “1000” ,  
                                      “TRES MIL VEINTE Y CUATRO CON 20/100 NUEVOS SOLES”);
 </pre>


****************



<br><br>


Después de haber terminado con la asignación de valores de los campos de la Factura se usará el método _Generar_.


_**Para esto, instanciamos la clase Respuesta**_

<?prettify lang=C#?>
<pre class="prettyprint">

              Respuesta r;      
 </pre>



Este método genera el comprobante y lo devuelve en un objeto tipo Respuesta.

_Llamamos al método Generar._  

<?prettify lang=C#?>
<pre class="prettyprint">

              r = c.Generar();
 </pre>



<br>

El objeto **Respuesta** contiene los siguientes atributos:  

<ul class="distancia">
<li>CodigoError</li>
<li>MensajeError</li>
<li>ArchivoPDF417</li>
<li>ArchivoXML</li>
<li>Hash</li>
<li>ResultadoFirma</li>
</ul>

<br>
Esto puede ser utilizado de la siguiente forma:

<?prettify lang=C#?>
<pre class="prettyprint">

        If (r.CodigoError = 0 ) 
            MessageBox.Show(r.ArchivoPDF417)      /* Muestra ruta del PDF471 */
            MessageBox.Show(r.ArchivoXML)         /* Muestra ruta del XML */
            MessageBox.Show(r.Hash)                 /* Muestra valor del Hash */
            MessageBox.Show(r.ResultadoFirma)     /* Muestra valor de la Firma */

        Else
            MsgMessageBox.Show(r.MensajeError) /* Muestra mensaje en caso de presentar un error */
              
        End If
 </pre>


_**En este ejemplo evaluamos:**_  
Si CodigoError es igual a cero, quiere decir que **no hay error** por lo tanto el atributo _MensajeError_ vendrá vacío, pero los otros atributos tendrán valores como se describe a continuación: 



<br>
<li>Archivo PDF417:</li>
Devuelve una cadena de caracteres, que indica la ruta donde se guardó el _archivo PDF417_ como imagen en formato PNG (La ruta siempre será la que tenga mayor permiso para escritura, por defecto será el directorio Documentos). 


**Ejemplo:**


<?prettify lang=C++?>
<center>
<pre class="prettyprint">
  
C:\Users\Admin\Documents\20543314529_01_F001-101.PNG
 </pre>
</center>

Este atributo es el más importante, ya que nos entrega la ruta de la _imagen en formato PNG_ que debemos agregar a la representación impresa del comprobante como se muestra en la siguiente imagen de ejemplo:

<center><img src="/assets/images/ticket1.png" alt=""></center>



<br>
<li>Archivo XML:</li>
Devuelve una cadena de caracteres, que indica la ruta donde se guardó el _archivo XML_ que tendrá de acuerdo a la especificación de la SUNAT.

**Ejemplo:**

<?prettify lang=java?>
<pre class="prettyprint">

            C:\Users\Admin\Documents\20543314529_01_F001-101.XML
 </pre>


<br>
<li>Hash:</li>
Devuelve el valor de la cadena resumen calculado del archivo XML en una cadena de caracteres. Según la especificación de la SUNAT este valor se puede imprimir en la representación impresa del comprobante en vez de utilizar la imagen PDF417.

**Ejemplo:**

<?prettify lang=C#?>
 <center>
<pre class="prettyprint">

oXaHY4FXt643ktMb2xEEmrFW5jA=
 </pre>
</center>


_**Ejemplo de una representación impresa con Hash:**_


<center><img src="/assets/images/ticket2.png" alt=""></center>




<br>
<li>Firma:</li>
Devuelve el valor de la _firma digital_ calculada del archivo XML y utilizando el certificado digital asignado al emisor, en cadena de caracteres. 

**Ejemplo:**



<?prettify lang=C#?>

<pre class="prettyprint">

              LsNuE0mHnAtQsx5h5ZdWSOnvo3MCtcYfnc34BNsmBj3h+19At3ib5xeGcHt
              +ZT+Q4vZ/UGP9/fwFCMvtvpXu4zQMcYLIIqIkY4qTXGe/QBu5YG/1xZxCIQMc
              4cIhPV0unWt/dKwz5Yp4PgjgNr0+eVxQ7LNVSLFwj1aQ9YA3xtIEE/8U6K2UYv
              DI0HaKZelpnMjyoQn1l6u13+krt7226pwbjo4R/v/0x6wby5PVFrvsu88gEIXDoD
              rX6u1p2rpCAva3E0mzWWYSJvoE8AM1a/KkGt0LcMQ5ZrqHvKOTxYtR/VLurZs
              ylOZxJkWVTX3Y+oqp4jcdwgPsm1zK8DihQA==
 </pre>

