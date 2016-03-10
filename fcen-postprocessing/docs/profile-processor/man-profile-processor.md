### profile-processor

`profile-processor [src=<ruta>] [wrk=<ruta>] [log=<ruta>] [out=<ruta>] [name=nombre] [dir=directorio] [profile=<perfiles>] [include|exclude=<archivos>] [imgimprove=<archivos>] [ext=<extensiones>] [no-ocr] [no-overwrite-ocr] [clear]`

**`src=<ruta>`**  
Origen: ruta al directorio que contiene los archivos para procesar. Por defecto toma el directorio donde se esté ejecutando el script. La ruta puede ser absoluta o relativa. Ej: `src=/opt/archives/tesis1`.

**`wrk=<ruta>`**  
Procesamiento: ruta al directorio de trabajo donde se generarán los archivos intermedios del proceso. Estos archivos quedan guardados en carpetas ocultas (por ej: `.processing`) creadas en este directorio. Su valor igual a `src` en caso de no especificarse.

**`log=<ruta>`**   
Registro: ruta al directorio donde quedarán guardados los registros del proceso. Valor por defecto igual a `wrk`. Se generan nuevos logs cada vez que se ejecuta el script. No se crea un directorio contenedor.

**`out=<ruta>`**   
Salida: ruta al directorio de destino del pdf final. Por defecto igual a `wrk`. 

**`name=<nombre>`**   
Nombre del archivo de salida (pdf), sin la extension. Por defecto "Tesis".

**`dir=<directorio>`**   
Un directorio que se añadirá al final de la rutas especificadas para origen y procesamiento. Por ejemplo: si se especifica `src=/opt/tesis` y `wrk=/home/user`, al incluir la opción `dir=Tesis_Milstein` se agregará el directorio en la ruta origen `/opt/tesis/Tesis_Milstein` y se creará (si no existiera) el directorio `/home/user/Tesis_Milstein` para su procesamiento. En caso de no haberse especificado nada para `out` o `log`, tomarán este ultimo valor.

**`profile=<lista de perfiles>`**   
Perfiles: los perfiles asignados al proceso, separados por comas y sin espacios. Sin especificar se aplica perfil por defecto `default`. Lista de perfiles al final de este documento. El perfil `default` corresponde a `a2`.
Ej: `profile=a2,b1,d1`.

**`include|exclude=<lista de archivos>`**   
incluir o excluir una lista de archivos separados por comas. En ambos casos se puede colocar el nombre completo (sin la extensión y sin espacios) o los últimos caracteres (por ejemplo `001,002,003,` etc ). En el caso de `include`, solo cargará los archivos especificados, en el caso de `exclude`, cargará todos los archivos con la extensión permitida menos los indicados. Si no se especifica `include`/`exclude` el script cargará todos los archivos con la extensión permitida.   
Ej: `include=001,002,005,012,132,345,346`.

**`ext=<lista de extensiones>`**   
Lista de extensiones de los archivos de imagen a procesar, separadas por comas. Por defecto ext=tif,TIF (Sensitivo a mayúsculas/minúsculas).   
Ej: `ext=jpg,JPG,jpeg,JPEG`.

**`imgimprove=<lista de archivos>`**   
Lista de los archivos que contienen fotografías o gráficas que deben ser procesadas como imágenes en color o valores de grises. El script excluye estos archivos en un primer procesamiento siguiendo el perfil especificado en 'profile', y en una segunda instancia los procesa independientemente agregando o modificando el perfil seleccionado con ciertas características óptimas para detectar y procesar imágenes (en desmedro de otras que optimizan el OCR).   
Ej: `imgimprove=001,002,005,012,132,345,346`.

**`no-ocr`**   
Si se incluye este parámetro no se realizará la operación de reconocimiento de caracteres (OCR).

**`no-overwrite-ocr`**  
Si se incluye este parámetro no se realizará la operación de reconocimiento de caracteres (OCR) si existiese un archivo previo de ocr (hocr con extensión `.html`) ya generado anteriormente.

**`clear`**  
Elimina todos los archivos generados por el sript: el pdf final, las carpetas ocultas con archivos intermedios (`.processing`, `.preprocessing`, etc), y los archivos de log. No elimina ningún archivo de origen.

### Referencia de perfiles

Tipo de página:
* **a1**: Sin bordes de pagina visibles.
* **a2**: Con borde de página.
* **a3**: Con borde de página y parte de la página opuesta visible.

Fondo:
* **b1**: Variaciones difusas (sombreados, bandas, oxidación del papel).
* **b2**: Variaciones o manchas contrastadas ("manchas de café").

Texto:
* **c1**: Muy fino.
* **c2**: Muy grueso.

Perforaciones:
* **d1**: perforaciones de anillados o marcas sobre los márgenes.

Contraste:
* **f1**: muy bajo contraste entre la figura (tipografía) y fondo.

Color:
* **g1**: Fondo oscuro (plano, sin variación).
* **g2**: Fondo/figura invertido (texto blanco).

