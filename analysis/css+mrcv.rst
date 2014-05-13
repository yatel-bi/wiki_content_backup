.. tags: 
.. title: CSS + MRCV

Bla bla

12/05/2014
++++++++++

**Exploración y filtrado de la base de datos**

- La base de datos contiene 3902 registros.

- Se deben seleccionar solo los registros con latitud > -30° y con longitud entre -64° y - 62°.




01/05/2014
++++++++++

**Fuentes de datos:**

    - Planilla de ingreso de muestras.xlsx (PI)
    - base de datos 18-07-2011.xls (E1)

**Estructura de PI:**

- 5 hojas ("Hoja1", "2011", "2012", "2013", "2014")
- Todas las hojas tienen estructuras similares (no idénticas)
- Los campos comunes son:
        - "Nº"
        - "Provincia"
        - "Localidad"
        - "Fecha"
        - "Síntomas-comentarios"
        - "CSS"
        - "MRCV"
- Problemas detectados:
        - Hay muchos valores nulos (hay que definir tratamiento para cada caso (tipo de atributo))
        - Representación no uniforme de la información (por ejemplo, en campo "MRCV" hay valores como ["4/32", "(+)", "(-)(+)", NULL]
        - Hay casos como: nro. 21325 en P1.Hoja1, que riene información sobre MRCV en el campo "Síntomas-comentarios" pero NULL en el campo "MRCV"
        - La hoja "2012" tiene celdas combinadas en cada fila

**Estructura de E1:**

- 3 hojas ("Insectos +CSS", "Base D. maidis", "CSS")
- Las hojas contienen datos distintos, pero probablemente con el mismo origen
- Los campos comunes son (no siempre con los mismos nombres):
        - "Latit."
        - "Long."
        - "Pcia."
        - "Localidad"
        - "Fecha"
        - "Cultivo"
        - "Labranza"
        - "Planta Nº"
- Campos de hoja "Insectos +CSS":
        - "Latit."
        - "Long."
        - "Pcia.
        - "Localidad"
        - "Fecha"
        - "Año"
        - "Mes"
        - "Día"
        - "Presencia CSS"
        - "Inc CCS"
        - "Observación"
        - "Cultivo"
        - "Estado/ sp."
        - "Labranza"
        - "Planta Nº"
        - "D. maidis"
        -    ...más campos de insectos (49)...
        - "MRCV"
        - "inc MRCV"
        - "MDMV"
        - "SCMV"
        - "MRFV"
        - "MCMV"
        - "Fitoplas"
        - "Otros"
- Campos de hoja "Base D. maidis":
        - "Lat."
        - "Long."
        - "Pcia."
        - "Localidad"
        - "Fecha"
        - "Cultivo"
        - "Labranza"
        - "Planta Nº"
        - "D. maidis"
- Campos de hoja "CSS":
        - "Latitud"
        - "Longitud"
        - "Provincia"
        - "Localidad"
        - "Fecha"
        - "Cultivo"
        - "Estado/ sp."
        - "Labranza"
        - "Planta N°"
        - "CSS"
        - "IncCCS"
        - "observaciones"
        - "MRCV"
        - "incMRCV"
        - "MDMV"
        - "SCMV"
        - "MRFV"
        - "MCMV"
        - "Fitoplas"
- Problemas detectados:
        - Muchos valores nulos (salvo en los campos geográficos)
        - Fechas incompletas
        - Números de planta como rangos y enumeraciones (por ejemplo: "133/147", "22;29/31;35/36;39/40;48;53;58")
        - **Representación no uniforme de la información**, por ejemplo:
        
            - En E1.CSS.incCSS hay valores como ["11,76%", "30 hojas", "3 plantas", NULL, "0%"]
            - En E1.CSS.incMRCV hay valores como ["Si", "No", "2,50%", "0%", NULL, "Sospechoso", "Dudoso")
            - En E1.CSS.CSS hay valores como ["Si", "No", "D", NULL]
            - En E1.CSS.MRCV hay valores como ["5???", "4", "13 de 30", "0 de 5", NULL]. **No es el mismo criterio que para CSS.**
            - En E1.CSS hay casos como: 
               - CSS = "Si"
               - incCSS = NULL
               - observaciones = "achaparrada, muchas mazorcas 1 de 19". **¿Con esta observación no debería haber otros valores para CSS o incCSS, como 1/19 o algo así?**


