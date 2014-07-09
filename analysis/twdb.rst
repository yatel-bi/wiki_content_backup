.. tags: 
.. title: Análisis de Tencent Weibo

General
+++++++

Para entender el domino de los datos, leer esto:

https://www.kddcup2012.org/c/kddcup2012-track1

La BD
+++++

* Fuente: KDD Cup 2012 Track 1
* Datos: https://www.kddcup2012.org/c/kddcup2012-track1/data

**Estructura**

.. image:: http://wiki.getyatel.org/analysis/twdb/_attachment/ERv01.png

- Las tablas con relleno gris no existen en la BD original, las creé para normalizarla y hacer más simples algunas consultas.
- Los atributos en azul pertenecen pertenecen a la misma clase, son palabras claves obtenidas con NLP y, en el caso de las tablas user_key_word* tienen un valor "peso".

**Tamaño de BD**

.. csv-table:: Base de datos - Tamaño y cant. de registros
    :header: Tabla,Filas,Tamaño

    item,6.095,1.2 MB
    item_keyword,202.802,3.9 MB
    rec_log_train,73.068.927,8.9 GB
    user_action,10.578.864,569.0 MB
    user_key_word,2.301.577,250.8 MB
    user_key_word_norm,15.657.691,694.0 MB
    user_profile,2.314.012,121.6 MB
    user_profile_tags,6.317.662,227.8 MB
    user_sns,50.492.960,2.0 GB


Atributo "user_profile.year_birth"
++++++++++++++++++++++++++++++++++

- Hay 41.144 registros con valores indiscutiblemente erroneos
- Los 2.279.751 restantes se distribuyen de la siguiente forma:

.. csv-table:: Distribución de year_birth
    :header: year_birth,cant

    1889,3
    1890,103
    1891,13.240
    1892,7.070
    1893,1.319
    1894,756
    1895,739
    1896,824
    1897,628
    1898,997
    1899,1.625
    1900,5.858
    1901,1.069
    1902,2.359
    1903,714
    1904,476
    1905,540
    1906,537
    1907,979
    1908,2.519
    1909,3.830
    1910,5.457
    1911,2.862
    1912,709
    1913,279
    1914,214
    1915,185
    1916,207
    1917,205
    1918,351
    1919,680
    1920,732
    1921,588
    1922,749
    1923,249
    1924,160
    1925,177
    1926,178
    1927,214
    1928,309
    1929,256
    1930,354
    1931,145
    1932,119
    1933,203
    1934,98
    1935,91
    1936,106
    1937,177
    1938,168
    1939,154
    1940,235
    1941,165
    1942,171
    1943,178
    1944,250
    1945,224
    1946,232
    1947,238
    1948,328
    1949,1.064
    1950,692
    1951,485
    1952,568
    1953,648
    1954,772
    1955,1.019
    1956,1.095
    1957,1.220
    1958,1.559
    1959,1.308
    1960,2.090
    1961,1.735
    1962,2.940
    1963,4.056
    1964,4.006
    1965,4.135
    1966,4.613
    1967,4.254
    1968,7.317
    1969,6.977
    1970,11.448
    1971,9.521
    1972,11.253
    1973,11.576
    1974,12.580
    1975,14.666
    1976,15.737
    1977,16.449
    1978,21.518
    1979,23.377
    1980,32.713
    1981,34.154
    1982,47.385
    1983,49.816
    1984,56.705
    1985,73.953
    1986,100.926
    1987,126.721
    1988,144.956
    1989,154.530
    1990,199.837
    1991,139.166
    1992,121.750
    1993,90.500
    1994,76.673
    1995,75.709
    1996,77.062
    1997,80.119
    1998,78.103
    1999,53.351
    2000,35.405
    2001,9.499
    2002,4.074
    2003,2.602
    2004,2.490
    2005,2.925
    2006,4.139
    2007,7.938
    2008,17.211
    2009,26.981
    2010,55.708
    2011,30.442
    2012,947
    2013,1

.. image:: http://wiki.getyatel.org/analysis/twdb/_attachment/year_birth.png

Atributo "user_profile.gender"
++++++++++++++++++++++++++++++

- La distribución entre sexos es uniforme y hay pocos valores erroneos u omitidos.

.. csv-table:: Distribución de "user_profile.gender"
    :header: gender,cant,descripción

    0,24.580,Desconocido
    1,1.159.797,Masculino
    2,1.136.390,Femenino
    3,128,Error
    
.. image:: http://wiki.getyatel.org/analysis/twdb/_attachment/gender.png



Atributo "user_profile.n_tweets"
++++++++++++++++++++++++++++++++

El atributo "n_tweets" tiene como falor mínimo 0 con 181.968 ocurrencias y como máximo 65.506 tweets (el doble
que el valor menor más cercano) con 1 ocurrencia.

Gráfico completo:

.. image:: http://wiki.getyatel.org/analysis/twdb/_attachment/user_profile-n_tweets_v01.png

Gráfico para valores entre 1 y 499:

.. image:: http://wiki.getyatel.org/analysis/twdb/_attachment/user_profile-n_tweets_v02.png


Atributo "user_profile.tag_id"
++++++++++++++++++++++++++++++

Hay 130305 tag_ids diferentes en user_profile_tags.

El tag_id más frecuente es "0", con 181.968 ocurrencias. La cantidad de ocurrencias de las demás tag_ids
cae rápido. La mayoría tiene 1 ocurrencia.

En este gráfico se ve la cantidad de ocurrencias de cada tag_id ordenadas por cantidad. Sólo se grafican las que tienen hasta 500 ocurrencias.

.. image:: http://wiki.getyatel.org/analysis/twdb/_attachment/user_profile_tags-tag_id_v01.png

En el gráfico que sigue se puede ver la cantidad de tag_ids que tienen n cantidad de ocurrencias. Por ejemplo, hay 83.670 tag_ids que sólo aparecieron una vez.

.. code-block:: sql

    SELECT ocurrencias, COUNT( * ) AS cant
    FROM (
    		SELECT tag_id, COUNT( * ) AS ocurrencias
    		FROM  `user_profile_tags` 
    		GROUP BY tag_id
    )A
    GROUP BY ocurrencias
    ORDER BY ocurrencias

.. image:: http://wiki.getyatel.org/analysis/twdb/_attachment/user_profile_tags-tag_id_v02.png

Atributo "item.category"
++++++++++++++++++++++++

Este campo tiene la forma A.B.C.D, donde A, B, C y D son números enteros
que representan una categoría o subcategoría de un ítem. Todos los ítems
pertenecen a una categoría formada por los cuatro niveles. Las categorías
se pueden representar como un árbol donde término A es el de mayor jerarquía
(está más cerca de la raíz). Los valores de las categorías no están uniformemente
distribuídos. En la siguiente tabla se muestran como ejemplo la cantidad
de existencias para cada valor del primer nivel.

.. code-block:: sql

    SELECT SUBSTRING_INDEX(category,'.',1) AS cat, COUNT(*) AS cant
	FROM item
	GROUP BY cat
	ORDER BY cat

.. csv-table:: Distribución 1er nivel de "item.category"
    :header: cat, cant

    1,4405
    2,1
    4,900
    6,22
    7,1
    8,766

En la siguiente imagen se puede ver la distribución completa del atributo
"category". En el círculo interno está se representa a A y en el externo a C.
Este tipo de gráficos se llama "sunburst" y es muy útil para visualizar datos
jerárquicos o estructuras de árbol.

.. image:: http://wiki.getyatel.org/analysis/twdb/_attachment/Analisis_categorias_v02.png