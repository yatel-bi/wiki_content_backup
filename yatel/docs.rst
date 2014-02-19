.. tags:
.. title: Draft sobre lo que se va a documentar de yatel

En esta pagina el proposito es completarla para ver
que documentacion vamos a ir generando en Yatel,
detallar cual documentacion es necesaria y prioritaria,
sobre todo para este primer semestre.


Que documentar?
+++++++++++++++

* Codigo en Python. **si**
* Tutoriales de instalacion? **si**
* Como forkear el proyecto? Tutorial de hg, rapido?
  **NO ya esta en http://getyatel.com.ar/contribute.html**
* Como usar Yatel (manual de usuario)? **si**


Prioridades de documentacion
++++++++++++++++++++++++++++

* Que seria lo primero que debemos documentar? **Codigo fuente**
* Como podemos establecer un orden de prioridad que se
  adapte a los avances escalables de Yatel?
  **Primero doc, despues manual, despues se traduce**


Documentadores
++++++++++++++

* Quienes documentan en Yatel?
  **Rodrigo, JBC & ROQUE segun la ultima minuta**
* Cada cuanto tiempo hay que hacer reviews de las docs?
  **Se cambia la documentacion a medida que se toca el codigo**


Extras
++++++

* Video tutoriales onda los resources? **SI**

.. tags: numpydoc, YatelDocFormat
.. title:


Formato de documentación de Yatel
+++++++++++++++++++++++++++++++++

A continuacion se detalla el formato de documentación
del código de Python empleado en Yatel, el mismo
es aquel que emplea NumPy

.. code-block:: python

    def foo(var1, var2, long_var_name='hi')
        """This function does something.

        Parameters
        ----------
        var1 : array_like
            This is a type.
        var2 : int
            This is another var.
        Long_variable_name : {'hi', 'ho'}, optional
            Choices in brackets, default first when optional.

        Returns
        -------
        describe : type
            Explanation
        """

Para más información dirigirse
`aquí <http://codeandchaos.wordpress.com/2012/08/09/sphinx-and-numpydoc/>`_
y `aca <https://github.com/numpy/numpy/blob/master/doc/example.py>`_ .

Y aca abajo dejo un link de `numpydoc guide <https://github.com/numpy/numpy/blob/master/doc/HOWTO_DOCUMENT.rst.txt>`_
