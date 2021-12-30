<div style="  padding: 10px;text-align: center;" class='row'>
<div style="float:left;width: 10%;" class='column'><a href="https://datos.gov.co/"><img alt="Logo DataSandbox"  src="https://github.com/DataSandbox/Plantilla-Publicacion-Resultados/raw/main/App/logdat.JPG" style="width: 100px;"></a></div>
    <div style="float:left;width: 80%;" class='column'>
        <h1>EXTRACCIÓN DE INFORMACIÓN EN DOCUMENTOS DE PROCESOS DE CONTRATACIÓN PÚBLICA
        </h1> 
    </div>
 <div style="float:left;width: 10%;" class='column'><a href="https://www.colombiacompra.gov.co/" target="_blank"><img class="float-right" src="https://raw.githubusercontent.com/ANCP-CCE-Analitica/datasandbox-extraccion/main/logo_ancp_cce_web.png" style="width: 200px;"></a></div>
    </div>


```python
import pandas as pd
pd.set_option("display.max_columns", None)
```

# Datos Muestra <a class="anchor" id="p1"></a>

Los datos de muestra usados en  la implementación del Modelo son obtenidos a través de la plataforma SECOP I Procesos de Contratación a la cual se puede acceder por medio del Portal de Datos Abiertos (<a href="https://www.datos.gov.co/Gastos-Gubernamentales/SECOP-I/xvdy-vvsk">https://www.datos.gov.co/Gastos-Gubernamentales/SECOP-I/xvdy-vvsk</a>). La base de datos completa contiene más de 10.8 millones de datos con 73 columnas.<br><br>
El proceso para extraer la muestra de los datos consistió en un análisis de las modalidades más relevantes para la contratación pública y las entidades que han presentado procesos de contratación pública. De esta manera, se observó la distribución de los datos prestando especial atención a la cantidad de contratos y procesos en los que participaron las diferentes entidades y cómo se ditribuyen estos por la modalidad de contratación, encontrando un grán número de entidades que han participado en múltiples procesos, al igual que entidades que han participado en pocos procesos o incluso 1. Similar a esto, se puede observar que la mayoría de los procesos se encuentran en 11 de las diferentes modalidades, los cuales tienen más de 10 mil procesos cada una.

Seguido a esto, para obtener una mayor variedad en el tipo de contrato, en su formato y en el archivo del contrato que contiene el proceso, se reducen los datos de tal forma que solo se guarde un contrato para cada entidad por cada modalidad de contratación. Es decir que una misma entidad puede tener varios contratos, pero solo uno de un mismo tipo de modalidad de contratación.

De esta forma, se toman los contratos que tienen más de 10,000 contratos en su modalidad antes de ser filtrados, con el fin de usar los tipos de contratos que son más relevantes y frecuentes, sin dividir en exceso los datos en grupos con muy pocos contratos.<br>
De estos grupos se genera la muestra aleatoria de 2000 contratos en los grupos que se puede y en los grupos que contengan menos de 2000 entradas, se toma el grupo completo.<br>
Por los tanto los contratos de los que se toma la muestra son los siguientes:<br>
<ul>
    <li>Contratación Directa (Ley 1150 de 2007)</li>
    <li>Régimen Especial</li>
    <li>Contratación Mínima Cuantía</li>
    <li>Selección Abreviada de Menor Cuantía (Ley 1150 de 2007)</li>
    <li>Subasta</li>
    <li>Licitación Pública</li>
    <li>Concurso de Méritos Abierto</li>
    <li>Contratación Directa Menor Cuantía</li>
    <li>Otras Formas de Contratación Directa</li>
    <li>Contratos y convenios con más de dos partes</li>
    <li>Licitación obra pública</li>
</ul>


```python
df = pd.read_csv("muestra_SECOP_I.csv")
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>UID</th>
      <th>Anno Cargue SECOP</th>
      <th>Anno Firma del Contrato</th>
      <th>Nivel Entidad</th>
      <th>Orden Entidad</th>
      <th>Nombre de la Entidad</th>
      <th>NIT de la Entidad</th>
      <th>Código de la Entidad</th>
      <th>ID Tipo de Proceso</th>
      <th>Tipo de Proceso</th>
      <th>Estado del Proceso</th>
      <th>Causal de Otras Formas de Contratacion Directa</th>
      <th>ID Regimen de Contratacion</th>
      <th>Regimen de Contratacion</th>
      <th>ID Objeto a Contratar</th>
      <th>Objeto a Contratar</th>
      <th>Detalle del Objeto a Contratar</th>
      <th>Tipo de Contrato</th>
      <th>Municipio Obtencion</th>
      <th>Municipio Entrega</th>
      <th>Municipios Ejecucion</th>
      <th>Fecha de Cargue en el SECOP</th>
      <th>Numero de Constancia</th>
      <th>Numero de Proceso</th>
      <th>Numero del Contrato</th>
      <th>Cuantia Proceso</th>
      <th>ID Grupo</th>
      <th>Nombre Grupo</th>
      <th>ID Familia</th>
      <th>Nombre Familia</th>
      <th>ID Clase</th>
      <th>Nombre Clase</th>
      <th>ID Ajudicacion</th>
      <th>Tipo Identifi del Contratista</th>
      <th>Identificacion del Contratista</th>
      <th>Nom Raz Social Contratista</th>
      <th>Dpto y Muni Contratista</th>
      <th>Tipo Doc Representante Legal</th>
      <th>Identific del Represen Legal</th>
      <th>Nombre del Represen Legal</th>
      <th>Fecha de Firma del Contrato</th>
      <th>Fecha Ini Ejec Contrato</th>
      <th>Plazo de Ejec del Contrato</th>
      <th>Rango de Ejec del Contrato</th>
      <th>Tiempo Adiciones en Dias</th>
      <th>Tiempo Adiciones en Meses</th>
      <th>Fecha Fin Ejec Contrato</th>
      <th>Compromiso Presupuestal</th>
      <th>Cuantia Contrato</th>
      <th>Valor Total de Adiciones</th>
      <th>Valor Contrato con Adiciones</th>
      <th>Objeto del Contrato a la Firma</th>
      <th>ID Origen de los Recursos</th>
      <th>Origen de los Recursos</th>
      <th>Codigo BPIN</th>
      <th>Proponentes Seleccionados</th>
      <th>Calificacion Definitiva</th>
      <th>ID Sub Unidad Ejecutora</th>
      <th>Nombre Sub Unidad Ejecutora</th>
      <th>Ruta Proceso en SECOP I</th>
      <th>Moneda</th>
      <th>EsPostConflicto</th>
      <th>Marcacion Adiciones</th>
      <th>Posicion Rubro</th>
      <th>Nombre Rubro</th>
      <th>Valor Rubro</th>
      <th>Sexo RepLegal Entidad</th>
      <th>Pilar Acuerdo Paz</th>
      <th>Punto Acuerdo Paz</th>
      <th>Municipio Entidad</th>
      <th>Departamento Entidad</th>
      <th>Ultima Actualizacion</th>
      <th>Fecha Liquidacion</th>
      <th>Codigo_contrato</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>16-12-49045964497785</td>
      <td>2016</td>
      <td>2016.0</td>
      <td>TERRITORIAL</td>
      <td>TERRITORIAL DEPARTAMENTAL CENTRALIZADO</td>
      <td>HUILA   INSTITUCIÓN EDUCATIVA NICOLAS GARCÍA B...</td>
      <td>891103249</td>
      <td>241799018</td>
      <td>12</td>
      <td>Contratación Directa (Ley 1150 de 2007)</td>
      <td>Liquidado</td>
      <td>Contratos para el Desarrollo de Actividades Ci...</td>
      <td>12</td>
      <td>Contratación Directa (Ley 1150 de 2007)</td>
      <td>81000000</td>
      <td>Servicios Basados en Ingeniería, Investigación...</td>
      <td>Contrato de arreglo congelación  e instalación...</td>
      <td>Prestación de Servicios</td>
      <td>Tello</td>
      <td>Tello</td>
      <td>Tello, Huila</td>
      <td>2016-03-21</td>
      <td>16-12-4904596</td>
      <td>005</td>
      <td>001</td>
      <td>2,850,000</td>
      <td>F</td>
      <td>[F] Servicios</td>
      <td>8116</td>
      <td>Entrega de servicios de tecnología de información</td>
      <td>811618</td>
      <td>Servicios de alquiler o arrendamiento de equip...</td>
      <td>4497785</td>
      <td>Cédula de Ciudadanía</td>
      <td>1075267858</td>
      <td>CM SOLUCIONES EFICACES  YO CRISTHIAN CAMILO ME...</td>
      <td>Huila</td>
      <td>Cédula de Ciudadanía</td>
      <td>1075267858</td>
      <td>CRISTHIAN CAMILO MEDINA PERDOMO</td>
      <td>2016-03-04</td>
      <td>2016-03-01</td>
      <td>10</td>
      <td>D</td>
      <td>0</td>
      <td>0</td>
      <td>2016-03-11 00:00:00</td>
      <td>Sn Definir</td>
      <td>2,850,000</td>
      <td>0</td>
      <td>2,850,000</td>
      <td>Contrato de arreglo congelación e instalación ...</td>
      <td>1</td>
      <td>Recursos propios</td>
      <td>0</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>0</td>
      <td>No Definido</td>
      <td>https://www.contratos.gov.co/consultas/detalle...</td>
      <td>No Definido</td>
      <td>No</td>
      <td>0</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>0</td>
      <td>N</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>Tello</td>
      <td>Huila</td>
      <td>2016-03-21</td>
      <td>2016-03-10</td>
      <td>'16-12-4904596'</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21-12-1179549010941635</td>
      <td>2021</td>
      <td>2021.0</td>
      <td>TERRITORIAL</td>
      <td>TERRITORIAL DEPARTAMENTAL DESCENTRALIZADO</td>
      <td>CAUCA  INSTITUTO MUNICIPAL DE DEPORTE Y RECREA...</td>
      <td>900589580</td>
      <td>21930017</td>
      <td>12</td>
      <td>Contratación Directa (Ley 1150 de 2007)</td>
      <td>Celebrado</td>
      <td>Prestación de Servicios Profesionales y de Apo...</td>
      <td>12</td>
      <td>Contratación Directa (Ley 1150 de 2007)</td>
      <td>80000000</td>
      <td>Servicios de Gestion, Servicios Profesionales ...</td>
      <td>PRESTAR SERVICIOS DE APOYO A LA GESTIÓN PARA R...</td>
      <td>Prestación de Servicios</td>
      <td>Guachené</td>
      <td>No Definido</td>
      <td>Guachené, Cauca</td>
      <td>2021-03-16</td>
      <td>21-12-11795490</td>
      <td>CPS N 19</td>
      <td>CPS N192021</td>
      <td>3,000,000</td>
      <td>F</td>
      <td>[F] Servicios</td>
      <td>8011</td>
      <td>Servicios de recursos humanos</td>
      <td>801116</td>
      <td>Servicios de personal temporal</td>
      <td>10941635</td>
      <td>Cédula de Ciudadanía</td>
      <td>4655229</td>
      <td>ZAMIR DIAZ GONZALEZ</td>
      <td>Cauca</td>
      <td>Cédula de Ciudadanía</td>
      <td>4655229</td>
      <td>ZAMIR DIAZ GONZALEZ</td>
      <td>2021-03-01</td>
      <td>2021-03-01</td>
      <td>90</td>
      <td>D</td>
      <td>0</td>
      <td>0</td>
      <td>2021-05-30 00:00:00</td>
      <td>Sn Definir</td>
      <td>3,300,000</td>
      <td>0</td>
      <td>3,300,000</td>
      <td>PRESTAR SERVICIOS DE APOYO A LA GESTIÓN PARA R...</td>
      <td>8</td>
      <td>Recursos Propios (Alcaldías, Gobernaciones y R...</td>
      <td>2020193000005</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>0</td>
      <td>No Definido</td>
      <td>https://www.contratos.gov.co/consultas/detalle...</td>
      <td>Peso Colombiano</td>
      <td>No</td>
      <td>0</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>0</td>
      <td>2</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>Guachené</td>
      <td>Cauca</td>
      <td>2021-03-16</td>
      <td>NaN</td>
      <td>'21-12-11795490'</td>
    </tr>
    <tr>
      <th>2</th>
      <td>13-12-20677961931485</td>
      <td>2013</td>
      <td>2013.0</td>
      <td>TERRITORIAL</td>
      <td>TERRITORIAL DISTRITAL MUNICIPAL NIVEL 6</td>
      <td>VALLE DEL CAUCA  ALCALDÍA MUNICIPIO DE EL CAIRO</td>
      <td>800100515- 2</td>
      <td>276246011</td>
      <td>12</td>
      <td>Contratación Directa (Ley 1150 de 2007)</td>
      <td>Liquidado</td>
      <td>Prestación de Servicios Profesionales y de Apo...</td>
      <td>12</td>
      <td>Contratación Directa (Ley 1150 de 2007)</td>
      <td>91000000</td>
      <td>Servicios Personales y Domésticos</td>
      <td>PRESTAR SERVICIOS PERSONALES DE APOYO A LA GES...</td>
      <td>Prestación de Servicios</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>El Cairo, Valle del Cauca</td>
      <td>2013-11-07</td>
      <td>13-12-2067796</td>
      <td>CDMEC089</td>
      <td>4000140892013</td>
      <td>3,872,000</td>
      <td>F</td>
      <td>[F] Servicios</td>
      <td>N/D</td>
      <td>No Definido</td>
      <td>N/D</td>
      <td>No Definido</td>
      <td>1931485</td>
      <td>Nit de Persona Natural</td>
      <td>61465104</td>
      <td>GREGORIO ANTONIO ROA ALARCONFULL MOTOS</td>
      <td>Valle del Cauca</td>
      <td>Cédula de Ciudadanía</td>
      <td>6146510</td>
      <td>GREGORIO ANTONIO ROA ALARCONFULL MOTOS</td>
      <td>2013-09-30</td>
      <td>2013-09-30</td>
      <td>20</td>
      <td>D</td>
      <td>0</td>
      <td>0</td>
      <td>2013-10-20 00:00:00</td>
      <td>Sn Definir</td>
      <td>3,872,000</td>
      <td>0</td>
      <td>3,872,000</td>
      <td>PRESTAR SERVICIOS PERSONALES DE APOYO A LA GES...</td>
      <td>0</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>0</td>
      <td>No Definido</td>
      <td>https://www.contratos.gov.co/consultas/detalle...</td>
      <td>No Definido</td>
      <td>No</td>
      <td>0</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>0</td>
      <td>N</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>El Cairo</td>
      <td>Valle del Cauca</td>
      <td>2013-11-07</td>
      <td>2013-10-20</td>
      <td>'13-12-2067796'</td>
    </tr>
    <tr>
      <th>3</th>
      <td>18-12-75074746822081</td>
      <td>2018</td>
      <td>2017.0</td>
      <td>TERRITORIAL</td>
      <td>TERRITORIAL DEPARTAMENTAL DESCENTRALIZADO</td>
      <td>ANTIOQUIA  INSTITUCIÓN EDUCATIVA HORACIO MUÑOZ...</td>
      <td>811019157</td>
      <td>205001153</td>
      <td>12</td>
      <td>Contratación Directa (Ley 1150 de 2007)</td>
      <td>Celebrado</td>
      <td>Prestación de Servicios Profesionales y de Apo...</td>
      <td>12</td>
      <td>Contratación Directa (Ley 1150 de 2007)</td>
      <td>72000000</td>
      <td>Servicios de Edificación, Construcción de Inst...</td>
      <td>MANTENIMIENTO LOCATIVO A TODO COSTO</td>
      <td>Prestación de Servicios</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>Medellín, Antioquia</td>
      <td>2018-01-10</td>
      <td>18-12-7507474</td>
      <td>122017</td>
      <td>122017</td>
      <td>1,800,000</td>
      <td>F</td>
      <td>[F] Servicios</td>
      <td>7210</td>
      <td>Servicios de mantenimiento y reparaciones de c...</td>
      <td>721033</td>
      <td>Servicios de mantenimiento y reparación de inf...</td>
      <td>6822081</td>
      <td>Nit de Persona Natural</td>
      <td>70116644</td>
      <td>LUIS HORACIO DE JESUS ARBOLEDA ALVAREZ</td>
      <td>Antioquia</td>
      <td>Nit de Persona Natural</td>
      <td>70116644</td>
      <td>LUIS HORACIO DE JESUS ARBOLEDA ALVAREZ</td>
      <td>2017-08-17</td>
      <td>2017-08-17</td>
      <td>14</td>
      <td>D</td>
      <td>0</td>
      <td>0</td>
      <td>2017-08-31 00:00:00</td>
      <td>Sn Definir</td>
      <td>1,800,000</td>
      <td>0</td>
      <td>1,800,000</td>
      <td>MANTENIMIENTO LOCATIVO A TODO COSTO</td>
      <td>0</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>0</td>
      <td>No Definido</td>
      <td>https://www.contratos.gov.co/consultas/detalle...</td>
      <td>Peso Colombiano</td>
      <td>No</td>
      <td>0</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>0</td>
      <td>N</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>Medellín</td>
      <td>Antioquia</td>
      <td>2018-01-10</td>
      <td>NaN</td>
      <td>'18-12-7507474'</td>
    </tr>
    <tr>
      <th>4</th>
      <td>09-12-175592245012</td>
      <td>2009</td>
      <td>2009.0</td>
      <td>NACIONAL</td>
      <td>NACIONAL DESCENTRALIZADO</td>
      <td>ONAC  ORGANISMO NACIONAL DE ACREDITACIÓN DECOL...</td>
      <td>900190680</td>
      <td>101092298</td>
      <td>12</td>
      <td>Contratación Directa (Ley 1150 de 2007)</td>
      <td>Celebrado</td>
      <td>No Definido</td>
      <td>12</td>
      <td>Contratación Directa (Ley 1150 de 2007)</td>
      <td>80000000</td>
      <td>Servicios de Gestion, Servicios Profesionales ...</td>
      <td>PRESTACION DE SERVICIOS DE EVALUACION DE ORGAN...</td>
      <td>Prestación de Servicios</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>Barranquilla, Atlántico</td>
      <td>2009-03-16</td>
      <td>09-12-175592</td>
      <td>030</td>
      <td>030</td>
      <td>24,000,000</td>
      <td>F</td>
      <td>[F] Servicios</td>
      <td>N/D</td>
      <td>No Definido</td>
      <td>N/D</td>
      <td>No Definido</td>
      <td>245012</td>
      <td>Cédula de Ciudadanía</td>
      <td>9131523</td>
      <td>ALVARO JOSE VILLALOBOS COMAS</td>
      <td>Atlántico</td>
      <td>Cédula de Ciudadanía</td>
      <td>9131523</td>
      <td>ALVARO JOSE VILLALOBOS COMAS</td>
      <td>2009-03-13</td>
      <td>2009-03-13</td>
      <td>6</td>
      <td>M</td>
      <td>0</td>
      <td>0</td>
      <td>2009-09-13 00:00:00</td>
      <td>Sn Definir</td>
      <td>24,000,000</td>
      <td>0</td>
      <td>24,000,000</td>
      <td>PRESTACION DE SERVICIOS DE EVALUACION A ORGANI...</td>
      <td>0</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>0</td>
      <td>No Definido</td>
      <td>https://www.contratos.gov.co/consultas/detalle...</td>
      <td>No Definido</td>
      <td>No</td>
      <td>0</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>0</td>
      <td>N</td>
      <td>No Definido</td>
      <td>No Definido</td>
      <td>Bogotá D.C.</td>
      <td>Bogotá D.C.</td>
      <td>2009-03-16</td>
      <td>NaN</td>
      <td>'09-12-175592'</td>
    </tr>
  </tbody>
</table>
</div>



De esta base de 22,021 procesos se extraen, de los documentos registrados en el proceso, los contratos finales. Obteniendo una muestra de 14,693 contratos.


```python
contratos = pd.read_csv("contratos_sql.csv", header=None)
contratos
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
      <th>13</th>
      <th>14</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15697384</td>
      <td>C_PROCESO_15-12-4086257_263272711_15697384.pdf</td>
      <td>ORIGINAL FIRMADO</td>
      <td>.pdf</td>
      <td>181543</td>
      <td>ORIGINAL FIRMADO</td>
      <td>1</td>
      <td>2015-07-30</td>
      <td>2015-07-30</td>
      <td>263272711</td>
      <td>15-12-4086257</td>
      <td>3796402</td>
      <td>-1</td>
      <td>13</td>
      <td>cloud/cloud2/2015/C/263272711/15-12-4086257/C_...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>11207872</td>
      <td>C_PROCESO_14-12-2797719_266001447_11207872.pdf</td>
      <td>NaN</td>
      <td>.pdf</td>
      <td>3040758</td>
      <td>NaN</td>
      <td>1</td>
      <td>2014-07-29</td>
      <td>2014-07-29</td>
      <td>266001447</td>
      <td>14-12-2797719</td>
      <td>2618949</td>
      <td>-1</td>
      <td>13</td>
      <td>cloud/cloud2/2014/C/266001447/14-12-2797719/C_...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6894729</td>
      <td>C_PROCESO_13-12-1590068_268167014_6894729.pdf</td>
      <td>CONTRATO</td>
      <td>.pdf</td>
      <td>206749</td>
      <td>CONTRATO</td>
      <td>1</td>
      <td>2013-04-10</td>
      <td>2013-04-10</td>
      <td>268167014</td>
      <td>13-12-1590068</td>
      <td>1491123</td>
      <td>-1</td>
      <td>13</td>
      <td>historico/I/2013/C/268167014/13-12-1590068/C_P...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4141775</td>
      <td>C_PROCESO_12-12-817955_113001004_4141775.pdf</td>
      <td>CONTRATO</td>
      <td>.pdf</td>
      <td>3248128</td>
      <td>CONTRATO</td>
      <td>1</td>
      <td>2012-02-29</td>
      <td>2012-02-29</td>
      <td>113001004</td>
      <td>12-12-817955</td>
      <td>790040</td>
      <td>-1</td>
      <td>13</td>
      <td>historico/E/product/10.1.2/OracleAS_1/infra/Ap...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5735281</td>
      <td>C_PROCESO_12-12-1267476_122043000_5735281.pdf</td>
      <td>CONTRATO 019-2012</td>
      <td>.pdf</td>
      <td>167937</td>
      <td>CONTRATO 019-2012</td>
      <td>1</td>
      <td>2012-11-16</td>
      <td>2012-11-16</td>
      <td>122043000</td>
      <td>12-12-1267476</td>
      <td>1185521</td>
      <td>-1</td>
      <td>13</td>
      <td>historico/G/2012/C/122043000/12-12-1267476/C_P...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>14688</th>
      <td>94503061</td>
      <td>C_PROCESO_21-22-29683_205440026_94503061.pdf</td>
      <td>CONVENIO CS-001-2021</td>
      <td>.pdf</td>
      <td>282310</td>
      <td>CONVENIO CS-001-2021</td>
      <td>1</td>
      <td>2021-10-01</td>
      <td>2021-10-01</td>
      <td>205440026</td>
      <td>21-22-29683</td>
      <td>11459941</td>
      <td>-1</td>
      <td>13</td>
      <td>2020/2020Q2/2021/C/205440026/21-22-29683/C_PRO...</td>
    </tr>
    <tr>
      <th>14689</th>
      <td>94525304</td>
      <td>C_PROCESO_21-22-29708_28834870_94525304.pdf</td>
      <td>CONTRATO</td>
      <td>.pdf</td>
      <td>199281</td>
      <td>CONTRATO</td>
      <td>3</td>
      <td>2021-10-01</td>
      <td>2021-10-04</td>
      <td>28834870</td>
      <td>21-22-29708</td>
      <td>11461374</td>
      <td>-1</td>
      <td>13</td>
      <td>2020/2020Q2/2021/C/28834870/21-22-29708/C_PROC...</td>
    </tr>
    <tr>
      <th>14690</th>
      <td>94678251</td>
      <td>C_PROCESO_21-22-29793_268679053_94678251.pdf</td>
      <td>CONVENIO 009-2021</td>
      <td>.pdf</td>
      <td>890423</td>
      <td>CONVENIO 009-2021</td>
      <td>1</td>
      <td>2021-10-05</td>
      <td>2021-10-05</td>
      <td>268679053</td>
      <td>21-22-29793</td>
      <td>11471525</td>
      <td>-1</td>
      <td>13</td>
      <td>2020/2020Q2/2021/C/268679053/21-22-29793/C_PRO...</td>
    </tr>
    <tr>
      <th>14691</th>
      <td>94781612</td>
      <td>C_PROCESO_21-22-29876_205000012_94781612.pdf</td>
      <td>CONTRATO</td>
      <td>.pdf</td>
      <td>4506535</td>
      <td>CONTRATO</td>
      <td>1</td>
      <td>2021-10-07</td>
      <td>2021-10-07</td>
      <td>205000012</td>
      <td>21-22-29876</td>
      <td>11479201</td>
      <td>-1</td>
      <td>13</td>
      <td>2020/2020Q2/2021/C/205000012/21-22-29876/C_PRO...</td>
    </tr>
    <tr>
      <th>14692</th>
      <td>94814435</td>
      <td>C_PROCESO_21-22-29917_215861011_94814435.pdf</td>
      <td>CONVENIO</td>
      <td>.pdf</td>
      <td>4850611</td>
      <td>CONVENIO</td>
      <td>1</td>
      <td>2021-10-08</td>
      <td>2021-10-08</td>
      <td>215861011</td>
      <td>21-22-29917</td>
      <td>11481286</td>
      <td>-1</td>
      <td>13</td>
      <td>2020/2020Q2/2021/C/215861011/21-22-29917/C_PRO...</td>
    </tr>
  </tbody>
</table>
<p>14693 rows × 15 columns</p>
</div>



En el cuaderno [Muestra SECOP-I.ipynb] se muestra en detalle la implementación de estas ideas en la selección de datos.
