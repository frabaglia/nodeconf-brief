# **NodeConf17**

## [V8 internals for JS developers](https://v8project.blogspot.com.ar/2017/09/elements-kinds-in-v8.html)

### Element kinds on V8

- SMI_ELEMENTS = [1,2,3]
- DOUBLE_ELEMENTS = [1,2,3,**3.5**]
- REGULAR_ELEMENTS = [1,2,3,3.5,**'x'**]
- HOLEY_ELEMENTS = [1,2,3,3.5,**'x'**]

### Holey vs Packed arrays

**HOLEY_ELEMENTS** es el tipo definido en V8 para etiquetar elementos de Arreglos que le quedan espacios vacios cuando agregas un indice desplazado.

``` javascript
const array = [1, 2, 3, 4.56, 'x'];
// elements kind: PACKED_ELEMENTS
array.length; // 5
array[9] = 1; // array[5] until array[8] are now holes
// elements kind: HOLEY_ELEMENTS
```

### Array types of elements

**[MORE SPECIFIC OPS]** Optimized and faster

- SMI
- DOUBLES
- REGULAR
- HOLEY

**[MORE GENERAL OPS]** Less optimized (more checks) and slower

## Tips

- Si un arreglo no es HOLEY_ARRAY, es PACKED_ARRAY. Un PACKED_ARRAY es mucho mas eficiente para consumir, porque se reducen la cantidad de operaciones por acceso.

- Un Array que se inicializa HOLEY, sera HOLEY para siempre aunque lo llenes de elementos o transformes en un arreglo que maneje elementos mas especificos.

- No usar For corriente, usar For Each / For Of para evitar iterar sobre elementos vacios. El problema no es solo arriesgarse a acceder a un elemento indefinido, sino que es más costoso.

- Los valores **NaN** e **Infinity** transforman un Array SMI_PACKED_ARRAY a un DOUBLE_PACKED_ARRAY y es más lento por ser menos especifico...

- Siempre usar arreglos que contengan elementos del tipo mas simple posible.

- Usar arreglos sobre arreglos-objetos. Ejemplo:

```javascript
const arrayLike = {}
arrayLike.push(1)
const array = []
array.push(1)
```

## [Dat](https://datproject.org/)

[Hyperdrive: Share filesystem over p2p.](https://github.com/mafintosh/hyperdrive)

[Hyperdiscovery: Discover the network](https://www.npmjs.com/package/hyperdiscovery)

## AOT

> [Swagger](https://swagger.io)

> [RAML](https://raml.org/)

## After years of Node production, we still block de Event Loop

> Monitorear el Event Loop y las metricas de tus servicios es la unica forma de mejorar tu performance.

### Tooling

[Blocked](https://www.npmjs.com/package/blocked)

[FlameGraphs](https://github.com/brendangregg/FlameGraph)

### Blocking operations

- require()
- JSON.parse()
- JSON.stringify()
- Garbage Collector

# AST la vista baby

- Entender como funciona AST te ayuda a entender la mayoria de las devtools conocidas (Babel, ESLint, etc).
- Como todos estos se manejan de esta forma, podes crear tus propios plugins escribiendo modificadores de AST.
- Lodash (para evitar exceptiones)

### Babel
Transformar JS y transformarlo a otro JS (no necesariamente habla de versiones de JS).

# Node Addons
> stdlib (Addons standard para Node) <
> El hecho de tener que crear un wrapper puede afectar la performance, por ende no siempre es la mejor opcion hacer algo nativo. Muchas veces la performance es mejor en su Orden, y se puede percibir en cantidades muy altas de operaciones. <

## Challanges on Addons:
- Windows.
- Bugs.
- Standards.
- Propietary.
- Portability.

## Util tools:
- BLAS = libreria para optimización de librerias nativas, una generica es OpenBlas (Sirve para cualquier SO)
- NAN (nan.h/cpp) = Api para usar V8 de forma transversal a las versines.
- NAPI (node_api.h/cpp):
  > Stability.

  > Compatibility.

  > VM Neutrality.


# Ordenando tus medias con JS

Porque armar tus propios prototipos de ordenamiento?
- Estabilidad: Cada VM de JS usa su version de sort, algunas VM uasn algoritmos inestables (V8 por ejemplo usa Quicksort).
- Performance: Para cantidades de elementos (>10.000.000) implementar tu propio sorting es más rapido que la versión nativa.


# The road to node (ML)

> ML empezo a usar Node + React como capa de UI. El %90 de las web apps de ML es SSR . <

- Be careful, don't transpile the server!
- ML acepto traspilar JSX en runtime del lado del server.
- React router en el server les cago todo.
- process.env no es un JS Object, hace una llamada a sistema. Estaría bueno cachear si vamos a usar process.env en cache. React 16 lo arregla internamente.
-

### Utils:
- node.green: ES feature status on every feature.

# Panel

- No transpilar el server.
- Callbacks > Promises > Async/Await [performance]
- Node 6 y 8 es mucho mas performante en promises que 4.
- Debugear callbacks es mucho mas facil que Promises.
- RoboticsJS es un ejemplo de como extender la comunidad y que un lenguaje llegue a todos lados puede aportar al creciemiento y la evolucion de un lenguaje.
- Use require over import

# Await/Async

We don't throw erro
