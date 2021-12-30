<div style="  padding: 10px;text-align: center;" class='row'>
<div style="float:left;width: 10%;" class='column'><a href="https://datos.gov.co/"><img alt="Logo DataSandbox"  src="https://github.com/DataSandbox/Plantilla-Publicacion-Resultados/raw/main/App/logdat.JPG" style="width: 100px;"></a></div>
    <div style="float:left;width: 80%;" class='column'>
        <h1>EXTRACCIÓN DE INFORMACIÓN EN DOCUMENTOS DE PROCESOS DE CONTRATACIÓN PÚBLICA
        </h1> 
    </div>
 <div style="float:left;width: 10%;" class='column'><a href="https://www.colombiacompra.gov.co/" target="_blank"><img class="float-right" src="https://raw.githubusercontent.com/ANCP-CCE-Analitica/datasandbox-extraccion/main/logo_ancp_cce_web.png" style="width: 200px;"></a></div>
    </div>

# ---------

En este ejercicio se pretende leer los contratos asociados a algunos procesos de contratación pública alojados en la plataforma del SECOP I y guardados como imagen en archivos PDF. En los siguientes directorios se encontrará:

- Para implmentacion

    - Una muestra de contratos, en el proyecto que se llevo a cabo con DataSandbox se uso una cuenta de almacenamiento que contenía más de 10000 documentos de este estilo, dejamos una muestra con 50 contratos de procesos revisados en este ejercicio.
    - *Muestra SECOP_I.csv* La muestra de los procesos que se trabajaron en el proyecto, en la documentación se explica en detalle como se obtuvieron estas muestras y que criterios nos llevaron a trabajar con estos proceso.
    - *contratos_procesados.csv* Un filtro de la base anterior que contiene los datos descargados y que se alojaron en el *Data Lake* proporcionado por DataSandBox.
    - *Mapeo_Variables_SECOPI.xlsx* Una base de datos que relaciona los diferentes nombres de la variables según diferentes fuentes, muy útil para unificar el ejercicio usando la API Socrata de datos abiertos con una descarga directa. Más información de su uso en la documentación.
   
- Procesados

    - *DFText_total_sample.parquet* es una base que integra los directorios de los contratos con los que se pueden trabajar en este repositorio. También contiene la variable *Text* que contiene el texto extraido de cada documento.
    - *DFText_total_entities_sample.json* contiene información con las entidades obtenidas después de procesar con <span style="color:blue">*Text Analytics*</span>. Cada entidad se guarda como un diccionario para que sea fácil expresar la información como un DataFrame. 
