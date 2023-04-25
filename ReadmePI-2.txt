README

TELECOMUNICACIONES

Descripción del problema -contexto y rol a desarrollar-
Contexto
Las telecomunicaciones se refieren a la transmisión de información a través de medios electrónicos, como la telefonía, la televisión, la radio y, más recientemente, el internet. Estos medios de comunicación permiten la transmisión de información entre personas, organizaciones y dispositivos a largas distancias.

El internet, por su parte, es una red global de computadoras interconectadas que permite el intercambio de información en tiempo real. Desde su creación, ha tenido un impacto significativo en la vida de las personas, transformando la manera en que nos comunicamos, trabajamos, aprendemos y nos entretenemos.

La industria de las telecomunicaciones ha jugado un papel vital en nuestra sociedad, facilitando la información a escala internacional y permitiendo la comunicación continua incluso en medio de una pandemia mundial. La transferencia de datos y comunicación se realiza, en su mayoría, a través de internet, líneas telefónicas fijas, telefonía móvil y en casi cualquier lugar del mundo.

En comparación con la media mundial, Argentina está a la vanguardia en el desarrollo de las telecomunicaciones, teniendo para el 2020 un total de 62,12 millones de conexiones.

Rol a desarrollar
En este contexto, una empresa prestadora de servicios de telecomunicaciones le encarga a usted la realización de un análisis completo que permita reconocer el comportamiento de este sector a nivel nacional. Considere que la principal actividad de la empresa es brindar acceso a internet, pero también es importante considerar el comportamiento asociado al resto de los servicios de comunicación, con el fin de orientar a la empresa en brindar una buena calidad de sus servicios, identificar oportunidades de crecimiento y poder plantear soluciones personalizadas a sus posibles clientes.

Con el fin de monitorear la eficacia de los objetivos de la empresa, se le pide visualizar en un dashboard el siguiente KPI y establecer 3 KPIs adicionales producto de su análisis:

Aumentar en un 2% el acceso al servicio de internet para el próximo trimestre, cada 100 hogares, por provincia. (Datos)
Dataset extraidos de la página: https://datosabiertos.enacom.gob.ar/dashboards/20000/acceso-a-internet/

Análisis Exploratorio de los datos (Exploratory Data Analysis = EDA)

1	Penetración del Internet fijo por provincia acceso por cada 100 hogares
2	Penetración del Internet fijo Nacional acceso por cada 100 hogares
3	Por banda ancha y banda angosta Nacional
4	Por banda ancha y banda angosta por provincia
5	Acceso a internet por tipo de tecnología
6	Acceso a internet fijo por tipo de tecnología y provincia
7	Velocidad media de bajada a nivel nacional
8	Velocidad media internet fijo de bajada por provincia x cada 100 hogares
9	Total nacional acceso internet fijo por velocidad de bajada
10	Internet fijo velocidad de bajada por provincia
11	Internet fijo velocidad de bajada por provincia
12	Ingresos por la operación del internet fijo
13	Accesos internet fijo por velocidad de bajada y localidad
14	Accesos internet fijo por tecnología y localidad
15	listado de localidades con conexión a internet
16	Conectividad al servicio de internet

Se analizaran los diferentes campos que posee cada uno de los archivos con miras a integrar algunos.

# Se cargan cada uno de los archivos de Excel en un DataFrame
df1 = pd.read_excel('1.xlsx')
df2 = pd.read_excel('2.xlsx')
df3 = pd.read_excel('3.xlsx')
df4 = pd.read_excel('4.xlsx')
df5 = pd.read_excel('5.xlsx')
df6 = pd.read_excel('6.xlsx')
df7 = pd.read_excel('7.xlsx')
df8 = pd.read_excel('8.xlsx')
df9 = pd.read_excel('9.xlsx')
df10 = pd.read_excel('10.xlsx')
df11 = pd.read_excel('11.xlsx')
df12 = pd.read_excel('12.xlsx')
df13 = pd.read_excel('13.xlsx')
df14 = pd.read_excel('14.xlsx')
df15 = pd.read_excel('15.xlsx')
df16 = pd.read_excel('16.xlsx')

Con el fin de saber que columnas se tiene en cada uno de estos archivos se procede a # Obtener los títulos de las columnas del DataFrame
titulos_columnas1 = df1.columns
titulos_columnas2 = df2.columns
titulos_columnas3 = df3.columns
titulos_columnas4 = df4.columns
titulos_columnas5 = df5.columns
titulos_columnas6 = df6.columns
titulos_columnas7 = df7.columns
titulos_columnas8 = df8.columns
titulos_columnas9 = df9.columns
titulos_columnas10 = df10.columns
titulos_columnas11= df11.columns
titulos_columnas12 = df12.columns
titulos_columnas13 = df13.columns
titulos_columnas14 = df14.columns
titulos_columnas15 = df15.columns
titulos_columnas16 = df16.columns
print("1: ", titulos_columnas1)
print("2 :", titulos_columnas2)
print("3 :", titulos_columnas3)
print("4 :", titulos_columnas4)
print("5 :", titulos_columnas5)
print("6 :", titulos_columnas6)
print("7 :", titulos_columnas7)
print("8 :", titulos_columnas8)
print("9 :", titulos_columnas9)
print("10 :", titulos_columnas10)
print("11:", titulos_columnas11)
print("12:", titulos_columnas12)
print("13:", titulos_columnas13)
print("14:", titulos_columnas14)
print("15:", titulos_columnas15)
print("16:", titulos_columnas16)


Se observa que hay tres tipos de dataset asi:
1 Dataset Provincias: 1,4,6,8,10,11 que contienen las columnas Año, Trimestre y Provincia
Nacional: 2,3,5,7,9,12 donde se encuentran los datos a nivel nacional: Año y Trimestre y opcional Periodo.
Conectividad: 13,14,15,16 con las columnas Provincia, Partido y localidad

Procedo a mirar mas el detalle de los datos para ver si es posible unirlos adecuadamente según los tipos de datos que contengan.

Se inicia con el analisis de estos archivos en este orden con el fin de proceder a un merge posterior:  1,4,6,8,10,11

Se analiza cada tabla, los tipos y valores unicos para establecer que se puede transformar.
Se decide cambiar tipos, llenar valores vacios por cero o eliminar aquellos que no posean información relevante.

Se encuentran muchas columnas que contienen la velocidad en Mbps y se filtra por este concepto para contabilizar cuantas campos poseen este campo y sumar los contenidos de todas estas columnas en una sola.

Luego de pulir los datos se hace un merge que contienen las columnas Año, Trimestre y Provincia y el archivo resultante se guarda con el nombre:
datos_provincias.csv

Se hace el analisis de los archivos que contiene información a nivel nacional, para los cuales se tiene en común: Año y Trimestre y opcional Periodo. 
Se hace un merge y el archivo resultante es datos_nacional.csv

Finalmente, el tercer grupo de archivos sobre la conectividad: 13,14,15,16 con las columnas Provincia, Partido y localidad, posee el detalle de los servicios que se prestan por provincia.
Se hace el merge de estos y se genera el archivo: datos_conectividad.csv

ANALISIS PREVIO
Se estudian los datos y se encuentran 23 provincias de Argentina que poseen 8 servicios difernetes de telecomunicaciones ( incluyendo otros) detallado.
Tambien se encuentra la información a nivel nacional de Argentina con unos ingresos y acceso por cada 100 hogares.
Considerando que se requieren varios KPI, se procede a investigar sobre el país Argentina. 

País de suramerica con 46 millones de habitantes. Para entrar más en contexto procedo a consultar por otros paises que tengan aproximadamente la misma cantidad de población.
Se seleccionan Colombia, España y Ucrania. Se extrae información de paginas web con datos de estos paises, entre las bases de datos consultadas están:
INDEC Instituto Nacional de Estadística y Censos
Banco Mundial
Cepal
ENACOM Ente Nacional de Comunicaciones 
ITU Internacional de Telecomunicaciones 
FMI Fondo Monetario Internacional
Además, con información de Digital 2022: Global Overview Report" de We Are Social y Hootsuite, ARSAT  y la pagina del gobierno de Argentina.gov.ar/dashboards/20000/acceso-a-internet/
se extraen datos de interes para alimentar con información el reporte. 
Algunos no era lo esperado y se depuraron en el proceso. 

Estos archivos con un ETL básico, se suben a Power Bi para continuar haciendo transformaciones segun se requieran.

En Power Bi, se establecen varias hojas que permitan explicar el proceso de analisis que se siguio para la hipotesis, analisis, desarrollo y propuesta de los KPIs para el mejoramiento e incremento de penetración del internet en Argentina.
Se tomaron los datos proporcionados de provincias y nacionales de Argentina mas los comparativos de los otros paises para aprender de las experiencias de estos en su incremento de penetración de internet.
Se concluye que se manejarian estos KPIs:
1. Penetración del internet
2. ARGU ( Ingreso promedio por usuario)
3. Incremento de uso de internet para nuevos fines 
4. Apoyo a categorías de usuario con nuevo enfoque

Se realizó una presentación en power point para reforzar la presentación y ayudar en la explicación de algunos aspectos y manejar el orden de la presentación final.


