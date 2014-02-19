.. tags:
.. title: Instalacion Yatel y Sphinx con NumpyDoc


Para instalar Yatel en linux es necesario ejecutar
el siguiente comando en la carpeta de Yatel:

.. code-block:: bash

    $ sudo python setup.py develop

Con eso instalamos Yatel, ahora vamos a instalar Sphinx:

.. code-block:: bash

    $ sudo pip install sphinx
    $ sudo pip install numpydoc

Luego en la carpeta de yatel vamos a  /doc y ejecutamos:

.. code-block:: bash

    $ make clean html

Lo cual nos genera la documentacion en html de yatel.
Nos dirigimos al directorio de build y vamos a index.html
para abrir la documentacion.


Como crear una red de prueba
++++++++++++++++++++++++++++

Desde consola se puede crear una red con  el comando ``fake-network``

::

    $ yatel --database sqlite:///fake_db.db --mode w --fake-network 25 50 ham

Luego desde Python se puede leer la db de la siguiente forma.

.. code-block:: python

    In [1]: from yatel import db
    In [2]: nw = db.YatelNetwork(**db.parse_uri("sqlite:///fake_db.db"))
