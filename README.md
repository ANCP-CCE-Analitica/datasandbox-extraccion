<div style="  padding: 10px;text-align: center;" class='row'>
<div style="float:left;width: 10%;" class='column'><a href="https://datos.gov.co/"><img alt="Logo DataSandbox"  src="https://github.com/DataSandbox/Plantilla-Publicacion-Resultados/raw/main/App/logdat.JPG" style="width: 100px;"></a></div>
    <div style="float:left;width: 80%;" class='column'>
        <h1>EXTRACCIÓN DE INFORMACIÓN EN DOCUMENTOS DE PROCESOS DE CONTRATACIÓN PÚBLICA
        </h1> 
    </div>
 <div style="float:left;width: 10%;" class='column'><a href="https://www.colombiacompra.gov.co/" target="_blank"><img class="float-right" src="https://www.colombiacompra.gov.co/sites/cce_public/files/files_2020/logo_ancp_cce_web.png" style="width: 200px;"></a></div>
    </div>


# Problemática 

La Agencia Nacional de Contratación Pública - Colombia Compra Eficiente (ANCP-CCE), como ente rector, tiene como objetivo desarrollar e impulsar políticas públicas y herramientas, orientadas a la organización y articulación de los partícipes en los procesos de compra y contratación pública con el fin de lograr una mayor eficiencia, transparencia y optimización de los recursos del Estado. En este sentido, la subdirección de Estudios de Mercado y Abastecimiento Estratégico (EMAE) ha detectado problemas relacionados a la calidad de la información de los contratos que han sido cargados por las entidades en la plataforma SECOP I, encontrando diferencias respecto a los documentos contractuales que soportan los procesos de contratación. Por ejemplo, se ha encontrado altos valores de contratación; al revisar esta información en los documentos del contrato se observa que las personas colocaron en los formularios de la plataforma cifras adicionales ocasionando estas diferencias.

Estas inconsistencias afectan los resultados que se generan en los insumos estratégicos y estudios de mercado sobre la contratación pública que la subdirección desarrolla, causando sesgos en la información que pueden afectar la toma de decisiones por parte de los diferentes actores de la compra pública.

Para corregir estos problemas de calidad, en la actualidad se realiza una depuración manual para algunos contratos de la plataforma SECOP I; en este proceso se revisa una muestra de contratos, se determina cuales de ellos tienen alguna incosistencia en su información y se notifica mediante Oficio a la entidad correspondiente, con el fin de que ellas realicen los respectivos ajustes. Sin embargo, al tener más de 10 millones de registros es necesario desarrollar una solución más eficiente que permita detectar de una manera más oportuna y agil estas incosistencias, disminuyendo los tiempos de notificación y ajuste de la información por parte de las entidades.


# Objetivos

**Desarrollar una herramienta de extracción y estructuración de la información contenida en los documentos que soportan los procesos de contratación pública que se suscriben en la plataforma SECOP I.**

- [x] Automatizar la extracción de texto de los documentos soporte de los procesos de contratación pública cargados en el SECOP I.
- [x] Aplicar tareas de reconocimiento de las variables correspondientes a datos específicos usando modelos de lenguaje previamente entrenados (BERT, Cognitive Services, entre otros) y estructurarlos con el fin de contrastarlos con la información previamente digitada por los usuarios del SECOP.
- [ ] Automatizar la búsqueda de datos erroneos en la plataforma y reportar posibles banderas rojas.
- [ ] Definir métricas que evalúen el desempeño de la herramienta frente a la calidad de los datos contenidos en los documentos y frente a la consistencia de los datos ingresados por el usuario.
- [x] Diseñar un tablero de control que contenga métricas de desempeño de la herramienta de  extracción y estructuración de información.
- [x] Diseñar un tablero de control que contenga métricas de desempeño del uso de la plataforma SECOP I por parte de los usuarios que registran la información.

# Fuentes de información

Las fuentes de información utilizadas en el desarrollo de este proyecto son:

Contratos suscritos por las entidades en la plataforma SECOP I. Esta plataforma en la actualidad cuenta con más de 10.8 millones de contratos cargados por las entidades del sector público. Esta información se puede consultar desde el portal de Datos Abiertos (www.datos.gov.co), siendo esta la fuente a partir de la cual se construyeron las bases de datos que se usaron en el desarrollo del proyecto.

# Equipo de Trabajo 

**Líder del proyecto:** Wilson Sanchez.

**Científico de Datos:** Isaac Zainea.

**Ingeniero de Datos:** Diego Rodríguez.

**Analista de Datos:** David Restrepo.

**Estadístico:** Juan Manuel Fernández.

**Administrador de Bases de Datos:** Diego Rodríguez.

**Apoyo Gestión de Proyectos:** Vivian La Farina.

# Contenido del repositorio

En esta parte se especifica la estructura de carpetas del repositorio y una descripción breve de cada una a manera de índice.

1. App                   carpeta para el Código del proyecto
2. Datos de Ejemplo      Carpeta donde se alojan ejemplos de los datos, tanto lo iniciales (fuentes de Datos), como los finales o los obtenidos (procesados)
3. Documentación         Carpeta que contiene toda la documentación del Proyecto.





