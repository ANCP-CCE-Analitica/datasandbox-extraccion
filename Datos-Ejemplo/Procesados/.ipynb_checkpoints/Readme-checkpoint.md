<div style="  padding: 10px;text-align: center;" class='row'>
<div style="float:left;width: 5%;" class='column'><a href="https://datos.gov.co/"><img alt="Logo DataSandbox"  src="https://github.com/DataSandbox/Plantilla-Publicacion-Resultados/raw/main/App/logdat.JPG" style="width: 100px;"></a></div>
    <div style="float:left;width: 90%;" class='column'>
        <h1>EXTRACCIÓN DE INFORMACIÓN EN DOCUMENTOS DE PROCESOS DE CONTRATACIÓN PÚBLICA
        </h1> 
    </div>
 <div style="float:left;width: 5%;" class='column'><a href="https://www.colombiacompra.gov.co/" target="_blank"><img class="float-right" src="https://raw.githubusercontent.com/ANCP-CCE-Analitica/datasandbox-extraccion/main/logo_ancp_cce_web.png" style="width: 200px;"></a></div>
    </div>

# Datasets procesados

En *DFText_total_sample.parquet* se encuentra una muestra que integra los directorios de los contratos con los que se pueden trabajar en este repositorio, que se veran en el directorio **Datos-Ejemplo/Para-implementacion/Contratos/** con la base ubicada en **Datos-Ejemplo/Para-implementacion/muestra_SECOP_I.csv**. Esta base fue utiliza para automatizar la extracción de texto con <span style="color:blue">*Computer Vision*</span> y contiene una variable **Texto** que contiene el texto leido del contrato. 

La base *DFText_total_entities_sample.json* contiene información con las entidades obtenidas después de procesar con <span style="color:blue">*Text Analytics*</span>. Cada entidad se guarda como un diccionario para que sea fácil expresar la información como un DataFrame. 

