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

###{{ page.title }}

Factus API Desktop para aplicaciones Desktop, es una librería desarrollada en C++❤ (COM) para sistemas operativos Windows de 32 y 64 bits. Esta disponible para Windows XP, Windows Vista, Windows 7, Windows 8 y Windows 8.1 en 32 y 64 bits.

Factus expone los siguientes objetos:

- Comprobante
- Ítem
- Impuesto
- DescuentosCargos
- Respuesta
- MontoAdicional
- PropiedadAdicional


Grafico de clases



A continuación mostramos un ejemplo de uso en C#.

Para utilizar Factus COM lo primero se debe instanciar la clase principal

<?prettify lang=C#?>
<pre class="prettyprint">

  Factus.Comprobante c = new Factus.Comprobante();
  c.TipoComprobante = “01”;


</pre>

Identificamos el tipo comprobante, en este caso si es Factura , se colocara “01” (Según Documentación SUNAT – Tipos de documento) 




c.SerieCorrelativo = “F001-101”; 



Este campo es único para cada factura y/o comprobante en general,  lo cual se convierte como un identificador único.




c.TipoIdentidademisor = “01”;



Este campo se refiere al tipo de documento de identificación del Emisor, en este caso para el Documento Nacional de Identidad (DNI), se colocará “01” (Según Catalogo Nro.6 Documentación SUNAT)



c.NumeroIdentidadEmisor = “20543314529”



Número de identidad del emisor del comprobante en este caso el R.U.C.




c.RazonSocial = “ComplexLess S.A.C.”


 
Razón social del emisor del comprobante




c.NumeroIdentidadCliente = “20100066603”

	

En este campo se coloca el número de identidad del Cliente en este caso el Cliente posee un R.U.C.




c.RazonSocialCliente= ”Sunat”


Razón social del Cliente.













Procedemos al llenado de Ítems


/* Instanciamos la clase Item y 
llenamos el primer campo */

Comprobante.Item it = new Comprobante.Item();

it.Id = “1”;




El id se llena de manera correlativa de acuerdo al numero de ítems que posea el comprobante.



it.Descripcion = ”Televisor LG Full HD “;
it.PrecioUnit = 11.80;
it.CodigoProducto = 10234;
it.Cantidad = 10;
it.TotalImpuesto = ”18”;
 


Se llena la descripción , precio unitario, código del producto , cantidad de cada Ítem , pero antes de registrarlo tenemos que llenar el impuesto individual de cada ítem : 



/* Instanciamos la clase Impuesto y 
llenamos los campos */

Item.Impuesto imp = new Item.Impuesto();

imp.Id = “VAT”;
imp.Nombre = “IGV”;
imp.SunatId = “1000”;
imp.BaseImponible = 100.00;
imp.totalImpuesto = 18.00;
imp.Porcentaje = 18;


En este caso supongamos que sea IGV , el id para IGV = “VAT” , el nombre = “IGV” y para este caso SunatId = “1000”, (Ver Catalogo Nro. 5 SUNAT ).
Luego agregamos el impuesto del ítem:


it.AgregaImpuesto ( imp );



Se procede a instanciar la clase DescuentosCargos para agregar los Descuentos y/o cargos del ítem en este caso:


/* Instanciamos la clase DescuentosCargos y 
llenamos los campos */

Item.DescuentosCargos desCarIt = new     Item.DescuentosCargos();

desCarIt.IdCd = 1;  /* Para Cargos: id = 1, y para                                                       	                     Descuentos: id = 2 
desCarIt.MontoCd= 180.20;






Luego agregamos el DescuentoCargo del ítem:


it.AgregaDesuentoCargo ( desCarIt );



Y procedemos a registrar este Ítem con el impuesto y Descuento cargo del mismo.


c.AgregaItem ( it );









Una vez llenado los impuestos  de cada Ítem , se procede a llenar el impuesto General . 


/* Instanciamos la clase Impuesto (Impuesto General) */

Comprobante.Impuesto impG = new Comprobante.Impuesto();




Como en este ejemplo se calculo mediante IGV , los campos serian : 


impG.Id = ”VAT”;
impG.SunatId = ”1000”;
impG.Nombre = ”IGV”;
impG.TotalImpuesto = 72.0;



El total impuesto es la suma de los impuestos individuales de cada Ítem,


Luego se procede a llenar los Descuentos Cargos Generales.


/* Instanciamos la clase DescuentosCargos y 
llenamos los campos */

Comprobante.DescuentosCargos desCarG = new                                Comprobante.DescuentosCargos();

desCarG.IdCd = 2;  /* Para Cargos: id = 1, y para                                                       	                      Descuentos: id = 2 
desCarG.MontoCd= 202.30;



Y se procede a registrar el descuento Cargo general
 

           c.AgregarDescuentoCargo ( desCarG );





Se procede a instanciar la clase  Monto adicional  


    /* Instanciamos la clase MontoAdicional y 
llenamos los campos */

   Comprobante.MontoAdicional monto = new                                
                    Comprobante.MontoAdicional();
   
   monto.ID =  “1001”;
   monto.Nombre = “Nombre1”;
   monto.MontoReferencial =  20.00;
   monto.ImporteTotal =  18.00;
   monto.Porcentaje = 18.00;
   monto.MontoTotal =  100.00;




MontoAdicional tiene como campos  a ID, en este caso se coloca el Id = “1001” que es el identificador para el Total valor de venta por Operación Gravada con el IGV (Según Documentación SUNAT).
Y luego se procede a colocar el Nombre, Monto Referencial, Importe total, Porcentaje y Monto total.

Al completar los campos, se procede a registrar  el Monto Adicional 


           c.AgregarMontoAdicional ( monto );




Instanciamos la clase PropiedadAdicional.



   /* Instanciamos la clase PropiedadAdicional y 
llenamos los campos */


   Comprobante.PropiedadAdicional propiedad = new                                
                    Comprobante.PropiedadAdicional();

   propiedad.ID = “9999”;
   propiedad.Nombre  = “nombre”;
   propiedad.Valor = “valor”;






La clase PropiedadAdicional tiene como campos a ID , Nombre y Valor .
En este ejemplo se coloca en ID = “9999” que concierne a “Otros”. (Según Documentación SUNAT) , luego se coloca el Nombre  y el Valor del concepto adicional.


Se procede a registrar propiedad adicional.


           c.AgregarPropiedadAdicional ( propiedad );





Luego agregamos “Otro Atributo”.


   c.AgregarOtroAtributo ( “1000” ,  
                          “SESENTA Y TRES CON 72/100 NUEVOS     
                          SOLES” );



El método AgregarOtroAtributo tiene como parámetros el ID = “1001” (Según documentación SUNAT) y el Valor, en este caso la Glosa expresado en letras el monto total de la Factura.


Se procede luego a agregar “Totales”.


c.TotalCargos = 40.00;
c.TotalDescuentos = 10.00;
c.TotalImpuestos = 12.00;
c.ImporteTotal = 42.00;




Se colocan los valores totales del comprobante
TotalCargos (Total de todos los cargos aplicados a nivel de total de la factura)
El descuento total (TotalDescuento) que es la suma de los montos de descuentos ingresados en la factura
El Importe Total (Importe Total) que es la suma total de los productos con todos los impuestos y el Total impuesto General del comprobante.
El Impuesto Total (TotalImpuesto) que es la suma de los montos de impuestos ingresados en la factura



Después de haber terminado con la asignación de valores de los campos del Comprobante se usara el método Generar.


/* Instanciamos la clase Respuesta */

Respuesta r;
r = c.Generar();




Este método genera el comprobante y lo devuelve en un objeto tipo Respuesta.



El objeto Respuesta, contiene los siguientes atributos:
-	CodigoError
-	MensajeError
-	ArchivoPDF417
-	ArchivoXML
-	Hash
-	ResultadoFirma

Esto puede ser utilizado de la siguiente forma:


If (r.CodigoError = 0 ) 
     	  MsgBox (r.ArchivoPDF417) /*Ruta del PDF471 */
     	 	  MsgBox (r.ArchivoXML) /*Ruta del XML */
     	 	  MsgBox (r.Hash) /*Valor del Hash */
        	  MsgBox (r.ResultadoFirma) /*Valor de la Firma */

Else
             MsgBox (r.MensajeError)
        
End If



En ejemplo evaluamos : 
Si CodigoError es igual a cero, quiere decir que NO HAY ERROR por lo tanto el atributo MensajeError vendrá vacío, pero los otros atributos tendrán valores como se describe a continuación: 





-	Archivo PDF417: 
Devuelve una cadena de caracteres, que indica la ruta donde se guardó el archivo PDF417 como imagen PNG (La ruta siempre será la que tenga mayor permiso para escritura, por defecto será el directorio Documentos). 


Ejemplo : 


C:\Users\Admin\Documents\20543314529_01_F001-101.PNG


	Este atributo es el más importante, ya que nos entrega la ruta de la imagen en formato PNG que debemos agregar a la representación impresa del comprobante. Como se muestra en la siguiente imagen de ejemplo:




-	Archivo XML 
Devuelve una cadena de caracteres, que indica la ruta donde se guardó el archivo XML que tendrá de acuerdo a la especificación de la SUNAT.

	Ejemplo:

  
C:\Users\Admin\Documents\20543314529_01_F001-101.XML



-	Hash
Devuelve el valor de la cadena resumen calculado del archivo XML  en una cadena de caracteres. Según la especificación de la SUNAT este valor se puede imprimir en la representación impresa del comprobante en vez de utilizar la imagen PDF417.

Ejemplo:


oXaHY4FXt643ktMb2xEEmrFW5jA=


	Ejemplo de una representación impresa con Hash:



























-	Firma
Devuelve el valor de la firma digital calculada del archivo XML y utilizando el certificado digital asignado al emisor, en cadena de caracteres. 

Ejemplo:
1

LsNuE0mHnAtQsx5h5ZdWSOnvo3MCtcYfnc34BNsmBj3h+19At3ib5xeGcHt+ZT+Q4vZ/UGP9/fwFCMvtvpXu4zQMcYLIIqIkY4qTXGe/QBu5YG/1xZxCIQMc4cIhPV0unWt/dKwz5Yp4PgjgNr0+eVxQ7LNVSLFwj1aQ9YA3xtIEE/8U6K2UYvDI0HaKZelpnMjyoQn1l6u13+krt7226pwbjo4R/v/0x6wby5PVFrvsu88gEIXDoDrX6u1p2rpCAva3E0mzWWYSJvoE8AM1a/KkGt0LcMQ5ZrqHvKOTxYtR/VLurZsylOZxJkWVTX3Y+oqp4jcdwgPsm1zK8DihQA==




Para una mejor referencia se adjunta el diagrama de caso de Uso:







<script src="https://gist.github.com/factus-lib/8990e4ab7ddf741e087a.js"></script>
