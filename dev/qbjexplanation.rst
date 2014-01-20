.. tags: qbj, ejemplo, impleentacion, sql
.. title: Explicación de Qbj

La idea es tener un grupo de funciones de bajo nivel que sirvan para
desarrollar un lenguaje de alto nivel de manera mas sencilla.
Por ejemplo:

En sql algo tan simple como

.. code-block:: sql

	select a.name from A a where a.id = 1 union select b.name from B b where b.id = 2

Es una cadena de llamadas a algun protocolo de mas bajo nivel 
mucho menos explicito pero mucho mas generico y flexible que SQL . 
Podriamos razonar esa sentencia 
SQL (invento un cacho) con QBJ a algo parecido a esto: 

.. code-block:: javascript


	{
      "id": null,
      "function": {
          "name": "union",
          "type": "literal",
          "args": [
              {
                  "type": "literal",
                  "function": {
                      "name": "select",
                      "type": "literal",
                      "kwargs": {
                          "where": {
                                  "type": "literal",
                                  "function": {
                                      "name": "equals",
                                      "type": "literal",
                                      "kwargs": {
                                          "from": {"type": "table", "value": "A"},
                                          "attr": {"type": "colum", "value": "id"},
                                          "val": {"type": "literal", "value": 1},
                                      }
                                  }
                          },
                      }
                  }
              },
              {
                  "type": "literal",
                  "function": {
                      "name": "select",
                      "type": "literal",
                      "kwargs": {
                          "where": {
                                  "type": "literal",
                                  "function": {
                                      "name": "equals",
                                      "type": "literal",
                                      "kwargs": {
                                          "from": {"type": "table", "value": "B"},
                                          "attr": {"type": "colum", "value": "id"},
                                          "val": {"type": "literal", "value": 2},
                                      }
                                  }
                          },
                      }
                  }
              },
          
          ]
      }
	}
    
Como notarán en el ejemplo hay un monton de funciones de más bajo nivel
que se llaman desde SQL para realizar su función. En definitiva QBJ va 
a ser nuestro motor de soporte para nuestra verdadera herramienta de
consulta (que aun no tiene nombre).