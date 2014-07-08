.. tags: 
.. title: Análisis de Tencent Weibo

**Análisis exploratorio de Tencent Weibo**

La BD

.. image:: http://wiki.getyatel.org/analysis/twdb/_attachment/ERv01.png


.. csv-table:: Base de datos
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

Atributo Category

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