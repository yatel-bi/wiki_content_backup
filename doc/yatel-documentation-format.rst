.. tags: numpydoc YatelDocFormat
.. title: Formato de documentación de Yatel

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