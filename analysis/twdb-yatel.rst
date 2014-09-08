.. tags: 
.. title: Análisis de Tencent Weibo con Yatel

General
+++++++

En este documento se detallan las tareas a realizar para cargar una BD Yatel con
los datos de Tencent Weibo. Inicialmente se describen los objetivos de
cada etapa. Lo escrito para cada tarea se debería completar con lo ejecutado
en Yatel (por línea de comandos y código) para que, terminado, se pueda usar
como tutorial.

Para entender un poco más de Tencent Weibo ver:

https://www.kddcup2012.org/c/kddcup2012-track1

http://wiki.getyatel.org/analysis/twdb/

Tareas
++++++

**1) Base de datos**

Bajar alguno de los archivos que tienen la DB completa en 
https://www.kddcup2012.org/c/kddcup2012-track1/data

**2) Haplotipos**

Del archivo User_profile.csv usar los campos *year_birth* y *gender* 
para cargar la tabla haplotypes de Yatel. El campo *hap_id* se debe formar 
concatenando *gender* + '_' + *year_birth*. Además, tambien incluir en la 
tabla los campos *gender* y *year_birth* como atributos separados. Solo se 
deben tener en cuenta los registros de User_profile.csv que tengan 
*year_birth* bien formados (enteros de cuatro dígitos) entre '1889' y '2013'. 
Para *gender* los valor válidos son '1' y '2'. 

Para aclarar, la lógica en SQL sería:

.. code-block:: sql

    INSERT INTO haplotypes(hap_id, year_birth, gender)
    SELECT DISTINCT concat(gender, '_', year_birth), year_birth, gender
    FROM user_profile
    WHERE year_birth
    IN (
    '1889', '1890', '1891', '1892', '1893', '1894', '1895', '1896', '1897', '1898', '1899', '1900', '1901', '1902', '1903', '1904', '1905', '1906', '1907', '1908', '1909', '1910', '1911', '1912', '1913', '1914', '1915', '1916', '1917', '1918', '1919', '1920', '1921', '1922', '1923', '1924', '1925', '1926', '1927', '1928', '1929', '1930', '1931', '1932', '1933', '1934', '1935', '1936', '1937', '1938', '1939', '1940', '1941', '1942', '1943', '1944', '1945', '1946', '1947', '1948', '1949', '1950', '1951', '1952', '1953', '1954', '1955', '1956', '1957', '1958', '1959', '1960', '1961', '1962', '1963', '1964', '1965', '1966', '1967', '1968', '1969', '1970', '1971', '1972', '1973', '1974', '1975', '1976', '1977', '1978', '1979', '1980', '1981', '1982', '1983', '1984', '1985', '1986', '1987', '1988', '1989', '1990', '1991', '1992', '1993', '1994', '1995', '1996', '1997', '1998', '1999', '2000', '2001', '2002', '2003', '2004', '2005', '2006', '2007', '2008', '2009', '2010', '2011', '2012', '2013'
    )
    AND gender IN ('1','2')

En Yatel:

.. code-block:: bash

    $ xxxxx
    

**3) Arcos**

Cargar la tabla edges de Yatel con las distancias entre los haplotipos. 
Para calcular las distancias (*weight*), se deben comparar todos los pares 
posibles de haplotipos y sumar:

    * La diferencia en años multiplicada por .125
    * La diferencia en géneros

En SQL sería así:

.. code-block:: sql

    INSERT INTO weight(hap_id_A, hap_id_B, weight)
    SELECT 
    A.hap_id,
    B.hap_id, 
    ABS(CAST(A.year_birth AS DECIMAL(4,0)) - CAST(B.year_birth AS DECIMAL(4,0))) * .125 
    + ABS(CAST(A.gender AS DECIMAL(1,0)) - CAST(B.gender AS DECIMAL(1,0))) AS weight
    FROM haplotypes A, haplotypes B

En Yatel:

.. code-block:: bash

    $ xxxxx

**4) Hechos**

Cargar la tabla *facts* de Yatel con el contenido del archivo *user_action.csv* y agregar los 
campos *hap_id* (tiene que estar siempre en *facts*) y *dest_hap_id*. Estos nuevos campos
son los *hap_id* que corresponden a los *user_id* de las dos primeras columnas.

La tabla debe quedar así:

.. image:: http://wiki.getyatel.org/analysis/twdb-yatel/_attachment/facts.png

Se deben tener en cuenta los criterios de hap_id válidos del punto 2. Si un fact determinado no
tiene un hap_id válido, no se debe importar.

En Yatel:

.. code-block:: bash

    $ xxxxx

**5) Exploración por ambientes**

Dividir los hechos cargados por ambiente. Crear un ambiente para cada combinación
existente de *n_action*, *n_retweet* y *n_comment*. Hay aprox. 33000 ambientes.
Identificar los haplotipos que existen en cada ambiente. En el ambiente *n_action* = 0, *n_retweet* = 0 y *n_comment* = 0 hay 184 haplotipos

En SQL sería así:

.. code-block:: sql

	SELECT n_action, n_retweet, n_comment, count(DISTINCT hap_id) AS cantHap, count(*) AS cantFact
	FROM user_action
	GROUP BY n_action, n_retweet, n_comment

Algunos ejemplos (los valores pueden tener errores):

.. csv-table:: Ambientes
    :header: n_action, n_retweet, n_comment, cantHap, cantFact

    
    0, 0, 0, 185, 14249
    0, 0, 1, 247, 989179
    0, 0, 2, 247, 195186
    0, 0, 3, 240, 66460
    0, 0, 4, 226, 34025
    0, 0, 5, 220, 18742
    0, 0, 6, 205, 12226
    0, 0, 7, 181, 8071
    0, 0, 8, 176, 5777
    0, 0, 9, 168, 4255
    0, 0, 10, 155, 3308
    0, 0, 11, 151, 2578
    0, 0, 12, 131, 1927

En Yatel:

.. code-block:: bash

    $ xxxxx

**6) Distancia por ambientes**


En Yatel:

.. code-block:: bash

    $ xxxxx

**7) Distancia esperada**

En Yatel:

.. code-block:: bash

    $ xxxxx

