.. tags: 
.. title: Clique

Siendo que tengo la tabla haplotipos con los atributos 


.. csv-table:: Tabla haplotypos
    :header-rows: 1
    
    id,weight,hap_0, hap_1 
    1,23,1,2
    2,23,2,3
    3,23,3,1


Como veras esta tabla indica que hay un arco no dirigido que conecta el nodo 1
con el nodo 2, otro el nodo 2 con el nodo 3, y por ultimo el 3 con el 1.

tengo la intención de encontrar  cliques con el cual el resultado de la 
consulta SQL debería dar **3**

En otras palabras la query debería realizar la consulta.

::


    Dame todos los id de haplotipos que tengan un arco enlazándolo con otro
    segundo id de de haplotipo que tenga un arco enlazando a tercer id de
    haplotipo que tenga un arco enlazando al primer id de haplotipo