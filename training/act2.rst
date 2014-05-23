.. tags: 
.. title: Parte 2: testing y mercurial

Mercurial y TestCases
---------------------

La dificultad de este ejercicio es que vas a tener que buscar documentación
para ir saliendo adelante (incluso para entender terminos)

1. Crear un Fork personal de este repositorio Mercurial 
   (https://bitbucket.org/yatel/test_mercurial) 
2. Clonar tu repositorio privado.
3. Las instrucciones siguientes estan en el archivo README.txt que esta adentro
   del repositorio
   
Mas actividades
---------------

Nuevas tareas: Hacerlo en este orden

1. Instalar setuptools
2. Con setup tools instalado y configurado instala pip con el comando
   ``easy_install pip``
3. Instalar flake8 para comprobar el estilo de tu codigo. Para instalarlo vas
   a necesitar ``pip install flak8``
4. Syncronizqr tu repo con lo nuevo que subi y pasar tu codigo por flake 8 hasta que tenga el estilo correcto con el comando
   ``flake8 test.py`` y que no tire ni un error
5. Testear el nuevo comando copy.
6. De momento whyname.py tiene dos errores de funcionamiento:

    1. Si yo escribo ``python whyname.py -p politica -f archivo.txt`` va a 
       seter la politica con ``-p`` y va a ignorar al parametro ``-f``. Eso
       esta mal ya que deberian ser parametros excluyentes (o uno o el otro)
       para eso existe una opcion que se llama groups en argparse (fijate)
    2. El archivo *policy.txt* deberia estar en una carpeta de archivos de conf
       por ejemplo en linux seria ``/etc`` en windows ni idea... pero deberias
       probeer un mecanismo que lo ponga en el lugar correcto

7. Versionar todo

No dejarse estar