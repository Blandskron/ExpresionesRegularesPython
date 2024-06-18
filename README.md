# Guía para Expresiones Regulares en Python

Las expresiones regulares (regex) son patrones utilizados para buscar y manipular texto de manera eficiente. Este documento proporciona una guía básica para entender y crear expresiones regulares en Python.

## ¿Qué es una expresión regular?

Una expresión regular es un patrón de búsqueda que define un conjunto de cadenas de texto válidas. Permite buscar, reemplazar y manipular texto de manera precisa y eficiente.

## Creando una expresión regular

Para crear una expresión regular en Python, utilizamos el módulo `re`. A continuación, se explica cada elemento que puedes encontrar en una expresión regular:

### Elementos comunes de una expresión regular:

1. **Literales**: Los caracteres literales coinciden exactamente con ellos mismos. Por ejemplo, `abc` coincidirá con la cadena `"abc"`.

2. **Secuencias de escape**: Caracteres especiales precedidos por una barra invertida `\`. Por ejemplo, `\d` coincide con cualquier dígito (equivalente a `[0-9]`).

3. **Clases de caracteres**: Especifican un conjunto de caracteres que se pueden usar en un punto específico en una cadena. Por ejemplo, `[abc]` coincide con `'a'`, `'b'` o `'c'`.

4. **Metacaracteres**: Caracteres con un significado especial en expresiones regulares. Algunos metacaracteres comunes incluyen:
   - `.`: Coincide con cualquier carácter excepto nueva línea.
   - `^`: Coincide con el inicio de una línea.
   - `$`: Coincide con el final de una línea.
   - `*`, `+`, `?`: Cuantificadores que especifican la cantidad de ocurrencias de un patrón.

5. **Grupos y Capturas**: Permite agrupar patrones juntos y capturar los resultados. Por ejemplo, `(abc)` agrupa y captura `"abc"` como una sola entidad.

6. **Cuantificadores**: Especifican la cantidad de veces que un elemento puede aparecer en un patrón. Por ejemplo:
   - `*`: Cero o más veces.
   - `+`: Una o más veces.
   - `?`: Cero o una vez.

### Ejemplos de expresiones regulares en Python:

#### Ejemplo 1: Validación de Correo Electrónico

```python
import re

def validar_correo(correo):
    patron = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return re.match(patron, correo) is not None

correo = "usuario@dominio.com"
print(validar_correo(correo))  # True
```

- `^`: Coincide con el inicio de la cadena.
- `[a-zA-Z0-9._%+-]+`: Coincide con uno o más caracteres alfanuméricos, puntos, guiones bajos, porcentajes o signos más y menos.
- `@`: Coincide con el carácter literal `@`.
- `[a-zA-Z0-9.-]+`: Coincide con uno o más caracteres alfanuméricos, puntos o guiones.
- `\.`: Coincide con el carácter literal punto (`.`).
- `[a-zA-Z]{2,}`: Coincide con dos o más letras del alfabeto (dominio de nivel superior).

#### Ejemplo 2: Extracción de URLs

```python
import re

def extraer_urls(texto):
    patron = r'https?://\S+'
    return re.findall(patron, texto)

texto = "Visita mi sitio en http://www.ejemplo.com y también https://otroejemplo.com"
urls = extraer_urls(texto)
print(urls)  # ['http://www.ejemplo.com', 'https://otroejemplo.com']
```

- `https?`: Coincide con `http` o `https`.
- `://`: Coincide con los caracteres literales `://`.
- `\S+`: Coincide con uno o más caracteres que no sean espacios en blanco.

## Consideraciones adicionales

- **Modificadores**: Puedes agregar modificadores al final de una expresión regular para cambiar su comportamiento, como `re.IGNORECASE` para hacer la búsqueda insensible a mayúsculas y minúsculas.

- **Funciones útiles**: En Python, funciones como `re.match()`, `re.search()`, `re.findall()` y `re.sub()` son comunes para trabajar con expresiones regulares.

- **Práctica**: Es recomendable probar y ajustar tus expresiones regulares utilizando herramientas como RegExr (https://regexr.com/) antes de implementarlas en tu código.


1. **Validación de correo electrónico simple**:
   ```python
   import re

   def validar_correo(correo):
       patron = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
       return re.match(patron, correo) is not None

   correo1 = "usuario@dominio.com"
   correo2 = "usuario@dominio"

   print(validar_correo(correo1))  # True
   print(validar_correo(correo2))  # False
   ```

2. **Validación de URL**:
   ```python
   import re

   def validar_url(url):
       patron = r'^(https?|ftp):\/\/[^\s/$.?#].[^\s]*$'
       return re.match(patron, url) is not None

   url1 = "http://www.ejemplo.com"
   url2 = "ftp://ftp.ejemplo.com"
   url3 = "https://invalid url"

   print(validar_url(url1))  # True
   print(validar_url(url2))  # True
   print(validar_url(url3))  # False
   ```

3. **Validación de número de teléfono (formato internacional)**:
   ```python
   import re

   def validar_telefono(telefono):
       patron = r'^\+(?:[0-9] ?){6,14}[0-9]$'
       return re.match(patron, telefono) is not None

   telefono1 = "+1234567890"
   telefono2 = "+1 234 567 8901"
   telefono3 = "+12345"  # Invalid

   print(validar_telefono(telefono1))  # True
   print(validar_telefono(telefono2))  # True
   print(validar_telefono(telefono3))  # False
   ```

4. **Detección de direcciones IPv4**:
   ```python
   import re

   def encontrar_ipv4(texto):
       patron = r'\b\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}\b'
       return re.findall(patron, texto)

   texto = "La dirección IP de mi servidor es 192.168.1.1 y la de mi router es 10.0.0.1"
   ips = encontrar_ipv4(texto)
   print(ips)  # ['192.168.1.1', '10.0.0.1']
   ```

5. **Detección de código postal (formato estadounidense)**:
   ```python
   import re

   def encontrar_codigo_postal(texto):
       patron = r'\b\d{5}(?:-\d{4})?\b'
       return re.findall(patron, texto)

   texto = "Mi código postal es 12345-6789"
   codigos_postales = encontrar_codigo_postal(texto)
   print(codigos_postales)  # ['12345-6789']
   ```

6. **Extracción de etiquetas HTML**:
   ```python
   import re

   def extraer_etiquetas_html(texto):
       patron = r'<([a-zA-Z][a-zA-Z0-9]*)\b[^>]*>(.*?)<\/\1>'
       return re.findall(patron, texto)

   texto_html = "<p>Este es un <b>texto</b> de ejemplo.</p>"
   etiquetas = extraer_etiquetas_html(texto_html)
   print(etiquetas)  # [('p', 'Este es un <b>texto</b> de ejemplo.')]
   ```

7. **Detección de números decimales**:
   ```python
   import re

   def encontrar_numeros_decimales(texto):
       patron = r'\b\d+\.\d+\b'
       return re.findall(patron, texto)

   texto = "El valor aproximado es 3.14 y el otro número es 123.456."
   numeros_decimales = encontrar_numeros_decimales(texto)
   print(numeros_decimales)  # ['3.14', '123.456']
   ```

8. **Detección de palabras específicas**:
   ```python
   import re

   def encontrar_palabras(texto, palabras):
       patron = r'\b(?:' + '|'.join(palabras) + r')\b'
       return re.findall(patron, texto, flags=re.IGNORECASE)

   texto = "Este texto contiene algunas palabras clave como Python, Java y C++."
   palabras_clave = encontrar_palabras(texto, ["Python", "Java", "C++"])
   print(palabras_clave)  # ['Python', 'Java', 'C++']
   ```

9. **Validación de formato de fecha (YYYY-MM-DD)**:
   ```python
   import re

   def validar_fecha(fecha):
       patron = r'\b\d{4}-(0[1-9]|1[0-2])-(0[1-9]|[12]\d|3[01])\b'
       return re.match(patron, fecha) is not None

   fecha1 = "2024-06-18"
   fecha2 = "24-06-18"
   fecha3 = "2024/06/18"  # Invalid

   print(validar_fecha(fecha1))  # True
   print(validar_fecha(fecha2))  # False
   print(validar_fecha(fecha3))  # False
   ```

10. **Eliminación de caracteres especiales**:
    ```python
    import re

    def eliminar_caracteres_especiales(texto):
        return re.sub(r'[^a-zA-Z0-9\s]', '', texto)

    texto = "Este texto tiene @caracteres !especiales."
    texto_limpio = eliminar_caracteres_especiales(texto)
    print(texto_limpio)  # 'Este texto tiene caracteres especiales'
    ```

Estas funciones muestran cómo puedes utilizar expresiones regulares en Python para realizar diversas operaciones como validación, extracción o limpieza de texto según patrones específicos.
