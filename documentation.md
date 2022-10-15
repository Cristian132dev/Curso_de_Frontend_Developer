# *Documentacion*

Este es mi libreta de apuntes de todo lo que vi en el ***Curso de Frontend Developer*** de ***Platzi***

Repasamos las bases de *HTML* y *CSS*:

- [*Documentacion*](#documentacion)
  - [Colapso de margenes](#colapso-de-margenes)
  - [Especificidad](#especificidad)
  - [Flexbox](#flexbox)
  - [Grid](#grid)
  - [Modela Caja](#modela-caja)
  - [Posicionamiento](#posicionamiento)
  - [Pseudoclases y Pseudoelementos](#pseudoclases-y-pseudoelementos)
  - [Selectores](#selectores)
    - [Selector de Descendientes](#selector-de-descendientes)
    - [Selector Directo](#selector-directo)
    - [Elemento Adyacente](#elemento-adyacente)
    - [Selector de hermanos](#selector-de-hermanos)
  - [Unidades de Medida](#unidades-de-medida)
  - [Z-index](#z-index)
  - [Responsive Design](#responsive-design)
  - [Conclusion](#conclusion)

## Colapso de margenes

El colapso de margenes se da cuando 2 elementos de tipo bloque coinciden en su *margin bottom* con *margin top*, lo que ocurre es que en lugar de respetar el espacio entre estos, simplemente se solapan.

Esto solo ocurre con elementos tipo bloque sin modificaciones de display, porque si se usa ``display:grid`` o `display: flex` esto se soluciona y no se interponen los margenes

## Especificidad

La especificidad es el metodo que usa el propio **CSS** para evitar errores y acomodar correctamente los estilos, para ello se creo una lista con valores, donde cada uno de estos sumara a un puntaje, puntaje que si es mayor es mas especifico:

| Valor | Elemento/Propiedad                   |
| ----- | ------------------------------------ |
| 10000 | `!important`                         |
| 1000  | Estilo en linea                      |
| 100   | #ID                                  |
| 10    | Clases y Pseudoclases `(:)`          |
| 1     | Elementos y Pseudoelementos ``(::)`` |
| 0     | Selector Universal ``*``             |

De este modo, cada propiedad *CSS* tiene su propia especificidad, por ejemplo:

```css
   section > a:hover{
      color: #458168;
      text-decoration: none;
   }
```

| Propiedad  | valor |
| ---------- | ----- |
| `section`  | 01    |
| `a`        | 01    |
| `:hover`   | 10    |
| Suma Total | 12    |

12 seria la especificidad del codigo css que vimos anteriormente

Si de casualidad dos especificidades coinciden, ganara la ultima "codeada" porque *CSS* funciona por cascada

## Flexbox

Flexbox es una manera de maquetar nuestra pagina, con esta podemos organizar distintos elementos y agruparlos a lo largo de la pagina. Para usarlos necesitamos un padre contenedor y los hijos. El padre tendra la propiedad `display: flexbox` y con solo eso ya los hijos se podran acomodar a nuestro acomodo

Flexbox es bastante utilizado en [Responsive Design](#responsive-design) junto los *media queries* para que nuestra pagina sea perfecta, tanto en web como en otros dispositivos, desde celulares hasta televisores

## Grid

Usar grid le dara a nuestro documento una propiedad nueva basada en grillas o espacios, como si fuesen cajones. desde ella podemos ajustar el tamaño de cada uno de estos cajones y sus posiciones.

Igual que con [flexbox](#flexbox) podemos combinarlo con los *media queries* para darle un [diseño adaptable](#responsive-design) a cualquier dispositivo

## Modela Caja

El box model son las medidas que tiene cualquier elemento el DOM, estas son cuatro:

1. **Content:** El contenido explicito del elemento, ya sea un texto o una imagen
2. **Padding:** El grueso del content, este rodea el content dandole volumen
3. **Border:** Rodea el padding y le da grosor al elemento
4. **Margin:** el espacio que hay entre el elemento hasta otro, este espacio es transparente

Estos cuatro modelos son modificables de muchas maneras pudiendo darle infinidad de estilos. Es recomendable añadir al selector universal `*` la propiedad `box-sizing: border-box` para que todos nuestros elementos empiezen a contar del borde hacia adentro, sin ese los valores se tomaran desde el padding hacia adentro sin contar el tamaño del borde.

## Posicionamiento

La propiedad de posicionamiento define donde estara ubicado nuestro elemento en el documento, al momento de usar esta propiedad podemos mover nuestro elemento con ``top``, ``left``, ``right`` y ``bottom``

Los posicionamientos existentes son:

1. **Static:** Es la propiedad por defecto y en esta las propiedades ``top``, ``left``, ``right`` y ``bottom`` no son utilizables
2. **Absolute:** El elemento se vera limitado por la propiedad ``position: relative;`` por lo tanto el tamaño de su padre sera el unico lugar donde podra moverse
3. **Relative:** No demuestra diferencia aparente pero permite ser posicionado donde queramos,   ademas si los hijos tienen un ``position: absolute;`` estos seran limitados por el tamaño del elemento ``relative`` mas cercano
4. **Sticky:** El posicionamiento ``sticky`` quedara fijo en el punto que le indiquemos, siempre y cuando el scroll lo arrastre con el, por ello, el elemento se movera junto al scroll
5. **Fixed:** Fija nuestro elemento donde le indiquemos en la pantalla, por lo tanto si tenemos un scroll este no perdera su sitio y se quedara fijo donde lo dejamos

## Pseudoclases y Pseudoelementos

Las *Pseudoclases* y los *Pseudoelementos* son modificadores presentes en *CSS* que permiten modificar un elemento o un conjunto de ellos.

Para identificar un *Pseduoelemento* o una *Pseudoclase* lo hacemos de esta forma:

Si despues del selector va solo un dos puntos ``selector:hover{}`` este es una *pseudoclase* y si por el contrario lleva doble dos puntos ``selector::first-letter {}`` es un Pseudoelemento

## Selectores

Los selectores es algo complejo de entender, sin embargo algo basico para seleccionar los elementos a modificar. Un concejo es que los *selectores* en ocasiones se leen mejor de izquierda a derecha.

Estos son los selectores, hay mas pero en este curso solo vimos estos de aca:

### Selector de Descendientes

Selecciona todos los elementos hijos, nietos, visnietos, etc...

```css
div .rojito{
   background-color: darkgrey;
   border: 1px solid black;
}
```

```html
<div>
   <article>
      <p class="rojito">A mi si me agarra 😁</p>
   </article>
   <span class="rojito">A mi tambien me agarra 😃</span>
</div>

<span class="rojito">A mi no me agarra 😭 </span>
```

### Selector Directo

**SOLO** selecciona los elementos hijos, **NO** los nietos. por ejemplo:

```css
div > .directo {
   background-color: darkgrey;
   border: 1px solid black;
}
```

```html
<div>
   <span class="directo">A mi si me agarra 😄</span>

   <section>
      <article class="directo">A mi no me agarra 😥</article>
</section>
</div>

<span class="directo">A mi menos 😭</span>
```

### Elemento Adyacente

Selecciona sus hermanos, es decir, al elemento que este justo por debajo, pero **SOLO** los que estan a su lado, si otro elemento se interpone no sera modificado:

```css
p + p{
   background-color: darkgrey;
   border: 1px solid black;
}
```

```html
<p>a mi nadie me selecciono 😭</p>
<p>Seleccionare el elemento de abajo 🤑</p>
<p>El elemento de arriba me selecciono 😀</p>
<div>
   <p>a mi nadie me selecciono 😭</p>
</div>
<p>a mi nadie me selecciono 😭</p>
```

### Selector de hermanos

Este a diferencia del anterior si selecciona todos los hermanos sin importar su posicion, en el ejemplo selecciona todos los elementos `p` que sean hermanos de `div`:

```css
div ~ p{
   background-color: darkgrey;
   border: 1px solid black;
}
```

```html
<p>soy hermano del div</p>
<section>
   <article>
      <h2>estoy dentro de un article</h2>
      <p>estamos en el primer hijo</p>
   </article>
   <article>
      <h2>estoy dentro de un article</h2>
      <p>estamos en el segundo hijo</p>
   </article>
</section>

<p>soy hermano del div</p>
<div>
   <p>soy hermano de los articles</p>
</div>
```

## Unidades de Medida

Las unidades de medida es algo fundamental en css, pero no tiene ningun tipo de complejidad:

- **px:** El pixel es la unidad de medida mas usada y esta es absoluta, por lo tanto no cambiara de tamaño por consecuencia de otro parametro o elemento
- **REM:** El REM es una unidad de medida que es variable, y su tamaño lo determina el `font-size` de la raiz del documento: el `html`, esta puede ser modificada para que podamos usar nuestra propias medidas
- **EM:** Usa el mismo concepto que el `REM` a diferencia que en lugar de apuntar a la raiz, esta apunta a su contenedor, si no tiene apuntara a su padre, sino a su abuelo, y haci hasta llegar a la raiz
- **vh:** El viewport hight o vh para los amigos es el tamaño visible que tenga nuestro documento a lo alto
- **vw:** El viewport width o vw funciona igual que el vh solo que este es a lo ancho
- **%:** el porcentaje usara de referencia el tamaño del documento visible y depende del valor que le demos este tomara el porcentaje correspondiente
- **min-hight & min-width:** El elemento como minimo tendra cierto tamaño y si el documento se achica este no se achiquitara mas alla de su valor, dejando un tamaño estatico minimo
- **max-hight & max-width:** El elemento tendra como maximo el tamaño que le demos, si el documento crece mas este dejara de expandirse quedandoce fijo en el valor que impusimos

## Z-index

El z-index es la forma en el que el navegador renderiza nuestra pagina, este lo hace por capas y estas capas respetan un estilo en cascada similar a *CSS* pero en *HTML* donde el ultimo elemento de nuestro html, sera la capa superior de la pagina. Esto lo podemos alterar desde *CSS* para que cada capa quede como queremos:

solo debemos agregar la propiedad `z-index:` con el valor que deseemos, un numero positivo sera la capa estara por encima y un numero negativo significa una capa por debajo.

Solo hay una excepcion, los elementos hijos **JAMAS** estaran por encima de los padres, no importa la cifra `z-index` que le agreguemos, simplemente no se puede, esta es una regla de *CSS*

## Responsive Design

El Responsive Design es la manera en la que nosotros como desarrolladores somos capaces de ofrecer nuestras plataformas para que sean consumibles desde cualquier dispositivo, mas especificamente, desde cualquier tipo de pantalla. Para lograr esto se usan distintos metodos:

- **Media queries:** son condicionales que si se convierten a `true` nos ejecutara el codigo *CSS* que tengan por dentro
- **Unidades de Medida**
- **Flexbox**
- **Grid**

Entre otros, lo que nos facilita mucho nuestro trabajo.

## Conclusion

Como nos podemos dar cuenta, algo tan basico puede llegar a ser muy extenso, este camino apenas inicia y ya estamos conociendo como se crean las paginas que vemos dia a dia.

Ahora sigue ***EL Curso Practico de Frontend***
