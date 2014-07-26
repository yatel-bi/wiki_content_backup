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
    FROM `user_profile`
    WHERE year_birth
    IN (
    '1889', '1890', '1891', '1892', '1893', '1894', '1895', '1896', '1897', '1898', '1899', '1900', '1901', '1902', '1903', '1904', '1905', '1906', '1907', '1908', '1909', '1910', '1911', '1912', '1913', '1914', '1915', '1916', '1917', '1918', '1919', '1920', '1921', '1922', '1923', '1924', '1925', '1926', '1927', '1928', '1929', '1930', '1931', '1932', '1933', '1934', '1935', '1936', '1937', '1938', '1939', '1940', '1941', '1942', '1943', '1944', '1945', '1946', '1947', '1948', '1949', '1950', '1951', '1952', '1953', '1954', '1955', '1956', '1957', '1958', '1959', '1960', '1961', '1962', '1963', '1964', '1965', '1966', '1967', '1968', '1969', '1970', '1971', '1972', '1973', '1974', '1975', '1976', '1977', '1978', '1979', '1980', '1981', '1982', '1983', '1984', '1985', '1986', '1987', '1988', '1989', '1990', '1991', '1992', '1993', '1994', '1995', '1996', '1997', '1998', '1999', '2000', '2001', '2002', '2003', '2004', '2005', '2006', '2007', '2008', '2009', '2010', '2011', '2012', '2013'
    )
    AND gender IN ('1','2')