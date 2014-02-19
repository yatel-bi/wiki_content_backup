.. tags: tuto, typeconv, ejemplos
.. title: Notas sobre modulos para el desarrollo


``yatel.typeconv``
++++++++++++++++++

La idea de este módulo es convertir todos los tipos de datos
soportados por yatel a unos tipos mas simples (con informacion de su
tipo original) para que puedan ser persistidos en un json.

donde se usa?

- Para persisitir las redes de manera agnostica a la base de datos
  (ya sabemos que los sql son diferentes en diferentes motores)
  y generar el formato YJF (Yatel JSON Format)
- Para trasmitir queries y resultados en QBJ (Query By JSON)

Por ejemplo si imaginamos un tipo de dato que no puede persistirse en yatel
onda la fecha actual typeconv funcionaría asi

.. code-block:: python

    In [3]: from yatel import typeconv
    In [4]: import datetime
    In [5]: now = datetime.datetime.now()
    In [6]: typeconv.simplifier(now)
    Out[6]: {'type': 'datetime', 'value': '2014-02-09T13:56:50.870024'}

Como se ve la fecha se guarda con ``simplifier`` en un formato unicode pero guarda una
llave que se llama *type* que indica que eso no es un texto sino un datetime.

Para datos mas simples por cuestiones de uniformidad hace lo mismo
por ejemplo si usamos algo que si puede persistirse en json como un int, str o unicode

.. code-block:: python

    In [7]: typeconv.simplifier(1)
    Out[7]: {'type': 'int', 'value': 1}

    In [8]: typeconv.simplifier("fooo")
    Out[8]: {'type': 'unicode', 'value': u'fooo'}

    In [9]: typeconv.simplifier(u"fooo")
    Out[9]: {'type': 'unicode', 'value': u'fooo'}

    In [10]: typeconv.simplifier(True)
    Out[10]: {'type': 'bool', 'value': True}


Cosas a notar, por cuestiones de uniformidad, tanto string como unicode se persiste como
unicode, y bueno int y boolean como int.

Tambien funciona con tipos mas complejos como listas, tuplas, diccionarios, sets y frozensets

.. code-block:: python

    In [12]: typeconv.simplifier([1,2,3])
    Out[12]:
    {'type': 'list',
        'value': [{'type': 'int', 'value': 1},
        {'type': 'int', 'value': 2},
        {'type': 'int', 'value': 3}]}

    In [13]: typeconv.simplifier({"k": "v"})
    Out[13]: {'type': 'dict', 'value': {'k': {'type': 'unicode', 'value': u'v'}}}

Tambien soporta los tipos de datos de yatel y muchos mas (la lista completa se puede ver
con ``typeconv.NAMES_TO_TYPES``

Obviamente se puede leer ese formato desde el mismo modulo. Por ejemplo si pasamos un in como
una cadena de caracteres:

.. code-block:: python

    In [22]: typeconv.parse({"type": "int", "value": "1"})
    Out[22]: 1


Teniendo una red de yatel en memoria podemos sacar un objeto *Descriptor* *Haplotype*, *Fact* o *Edge*,
y transformarlo con type conv. Por ejemplo con un Fact

.. code-block:: python

    In [8]: fact = list(nw.haplotypes())[0] # sloooow
    In [9]: typeconv.simplifier(fact)
    Out[9]:
      {'type': 'Haplotype',
       'value': {u'color': {'type': 'unicode', 'value': u'y'},
        u'description': {'type': 'unicode',
         'value': u'Dolordolor rebum at gubergren diam'},
        'hap_id': {'type': 'int', 'value': 0},
        u'number': {'type': 'int', 'value': 62},
        u'special': {'type': 'bool', 'value': False}}}


Tambien funciona con objetos numpy basicos y ndarray
