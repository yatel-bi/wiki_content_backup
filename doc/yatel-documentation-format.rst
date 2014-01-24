.. tags: 
.. title: Formato de documentación de Yatel

Formato de documentación de Yatel:
++++++++++++++++++++++++++++++++++

Todo el codigo realizado en python respetará el estándar de documentacón
y sintaxis de documentación que emplea NumPy.

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