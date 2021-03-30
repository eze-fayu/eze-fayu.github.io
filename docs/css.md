# GUIA DE CSS



### FORMULARIOS  
  
etiqueta **form**  
    for en un *label* relaciona  
etiqueta **input**  (text, email, etc)  
    conviene agrupar todo en un div, cada etiqueta + su input o los botones para darles formato a todos juntos. se usan pseudoclases para personalizar mas sobre todo los botones.  
    **text**= ingreso de texto
    **num**= para ingreo de num. tiene las flechitas para subir y bajar. en celulares abre el teclado numerico.  
    **password**= aculta lo escrito  
    **email**= hace las validaciones para que sea un correo electronico  
    **date**=pone un calendario para seleccionar una fecha  
    **color**= selector de color
    **textarea**=area para escribir. conviene manejarlo x css y no html

*placeholder* se usa para poner texto de muestra, que dato se requiere
*readonly* solo lectura
*disabled* activa o desactiva    
*autofocus* se posiciona solo ahi
*maxlen* longitud maxima de caracteres  
    **datalist** (de text)= input type=text list=paises
    datalist id=paises
    `<option data-value=casa>Casa></option>` para cada opcion  
    **dropdownlist** (de select) tiene la opcion multiple para seleccionar varios
    `<select><option value=0>Opcion</option>`
    `<optgroup>` y aca van option para crear un grupo  
    **checkbox** type=checkbox
    `<input type="checkbox" id=front-end></input>`
    `<label for=front-end>LALALAL</label>`
    *chequed* para que aparezca tildado x defecto, *disable*  
    **radiobutton** solo selecciona uno
    `<input type="radio" name="sdfsdf" id="oro"></inout>`
    `<label for="oro">sjk</label>`
    El grupo por el cual selecciona uno u otro se rige por name      
    
### TRANSFORMACIONES

**transform** _rotate_(20°) gira
              _scale_(1.6) agranda
              :hover (la pseaudoclase) para ponerle efectos cuando se pone el mouse. Se pone transition: transform y el tiempo (.5s)
              _skew_ deforma la imagen tambien en grados
              _translate_(10px, 20px) puede ir una sola

** 3D**
    **perspective** en pixeles
        *rotatex*(en grados)
        *rotatey*(en grados)

#### TRANSICIONES

se pone **transition** en el elemento a     cambiar y despues en la seudoclase elemento:hover

#### VARIABLES

```
:root{
    --color-fondo: orange
}

despues se usa en donde se quiere var(--color-fondo)
```

#### BUENAS PRACTICAS

- no usar nombres raros. si descriptivos a los que se vincula
- mantener orden de importancia de los elementos. 
    1. :root
    2. *
    3. html
    4. body
    5. h.......
    6. nav
    7. main  
y asi

- no repetir codigo. paran es0o estan los generadores (:root)
- comentar y mucho para saber que se hace

#### BEM
- utilizar clases para agrupar y a los hijos llamarlos con ese nombre + __ (dos guiones bajos) y lo que representa.