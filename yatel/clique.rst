.. tags: 
.. title: Clique

Siendo que tengo la tabla edges con los atributos 


.. csv-table:: Tabla edges
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

---------

Respuesta:

Según tu definición de la consulta sí, debería dar **3**, pero eso se 
considera solo **1** clique.

Debe ser pesado después buscar cuáles están repetidos. Se me ocurre una forma
para que se cree solo uno de entrada:

Si en la tabla edges los haplotipos están ordenados de mayor a menor, o si
se los devuelve ordenados cuando se consulta buscando cliques, se podría
hacer así:

La tabla ahora se vería como

.. csv-table:: Tabla edges_ord
    :header-rows: 1
    
    id,weight,hap_0, hap_1 
    1,23,1,2
    2,23,2,3
    3,23,1,3

Harían falta dos consultas:

1- La primera arma los "edges dobles" uniendo los edges donde 

    edge1.h2 = edge2.h1. 

Para la tabla del ejemplo solo se formaría uno.
Los edges dobles tienen un haplotipo inicial (le pongamos hi), uno oculto
y uno final (hf)
 
2- La segunda consulta cuza todos los edges contra todos los "edges dobles".
Se crea un clique en cada vez que hay coincidencia. La restricción es que:

    edge.h1 = edgedoble.hi AND edge.h2 = edgedoble.hf

Solo funciona si están ordenados los haplotipos dentro de cada arco.