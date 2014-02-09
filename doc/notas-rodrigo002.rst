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