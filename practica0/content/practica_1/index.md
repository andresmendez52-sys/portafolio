+++
date = '2026-02-16T18:06:38-08:00'
draft = false
title = 'Practica_1: Elementos basicos de los lenguajes de programacion'
+++

## Introduccion
En esta practica se enfoco en el desarrollo de un programa que simule la utilizacion de colas de impresion en lenguaje C. El programa se realizara en tres sesiones donde primero realizamos el programa utilizando memoria estatica, posteriormente en la sesion 2 migramos el programa a memoria dinamica atravez de listas enlazadas y finalmente en la sesion tres agregamos una obsion al memnu para crear una simulacion de proseso de impresion y mejorar el codigo 

## Diseño

PrintJob_t es una estructura que representa un trabajo de impresión dentro del sistema. En ella se guardan todos los datos necesarios para identificar y procesar un documento que se enviará a la impresora.

Campos principales:

+ id: número único que identifica cada trabajo de impresión.

+ usuario: nombre de la persona que envió el documento a imprimir.

+ documento: nombre del archivo o documento que se va a imprimir.

+ paginas_totales: número total de páginas que tiene el documento.

+ paginas_restantes: número de páginas que todavía faltan por imprimirse. Este valor va disminuyendo conforme se procesa el trabajo.

+ copias: cantidad de copias que se desean imprimir.

+ prioridad: indica la importancia del trabajo (por ejemplo normal o alta).

+ estado: indica en qué situación se encuentra el trabajo, por ejemplo en cola, imprimiendo o completado.

La cola estatica se implementa un areglo de tamaño fijo por lo que los documento se agregan al final de la sola y se eliminas desde el frente, sus elementos principales son primer elemento, ultimo elemento y el tamaño de la cola

````
primer elemento -> [Trabajo1][Trabajo2][Trabajo3] <- ultimo elemento   
cantidad = 3
`````

 mientras que el memoria dinamica se utilizan listas enlasadas por lo que sus principales componen tes son lso punteros que conenctan a los nodos, un puntero al ultimo nodo(cola) y un puntero al primer nodo(cabeza).

````

 cabeza -> [Trabajo1] -> [Trabajo2] -> [Trabajo3] -> NULL

                                              ↑
                                             cola
````

## Implementacion
### Funciones utilizadas
 * void inicializarCola(ColaDinamica *cola);
   
   Esta funcion se encarga basicamente de crear la cola e inicializarla en cero (en caso de utilizar la memoria estatica) o apuntar a NULL (en caso de utilizar memoria dinamica), en otras palabras inicializa la cola vacia 

* int colaVacia(const ColaDinamica *cola);

    esta funcion verifica que la lista este vacia y regresa 1 si es que esta vacia o cero si es que no lo esta, esta funcion, al contrario de la funcion de inicializar, no modifica a la cola, simplemente verifica que este vacia

* void agregarTrabajo(ColaDinamica *cola,TrabajoImpresion trabajo);

    al llamar a esta funcion agrega un trabajo a la cola y aumenta la cantidad de datos que tienen guardada, esta funcion tambien verifica si la el arreglo esta llego, de lo contrario agega una nuev tarea al final, tarea que el ususario ingresa dando le los datos de el titulo, autor y nuemro de paguinas.
    en el caso de la memoria dinamica tambien ajusta los punteros de la cola siguiente y anterior los cuales controla los nodos que se encuentran antes y despues del nuevo nodo.

* void capturarDatos(ColaDinamica *cola, int siguiente_id);

    La función capturarDatos se encarga de pedir al usuario la información de un trabajo de impresión, como el nombre del usuario, el documento y el número de páginas. Primero valida que los datos no estén vacíos o incorrectos. Después asigna algunos valores al trabajo, como su ID, estado, prioridad y páginas restantes. Finalmente intenta agregar el trabajo a la cola de impresión y muestra un mensaje indicando si se agregó correctamente o si la cola está llena.

    En este caso se usa memoria estática, por otro lado, si se usara memoria dinámica, los trabajos se crean con malloc y se almacenan en  listas enlazadas y colas dinámicas, haciendo que la cola crezca o disminuya en tamaño según sea necesario.

* void verSiguienteTrabajo(const ColaDinamica *cola);

    La función verSiguienteTrabajo muestra la información del primer trabajo en la cola de impresión. Primero verifica si la cola está vacía; si lo está, muestra un mensaje y termina. Si hay trabajos, obtiene el que está al frente de la cola y muestra sus datos principales como ID, usuario, documento y número de páginas. Al usar memoria dinámica, los trabajos se almacenan en nodos enlazados que se crean y eliminan durante la ejecución del programa

* void procesarTrabajo(ColaDinamica *cola);

    se encarga de atender el primer trabajo de la cola de impresión. Primero revisa si la cola está vacía; si lo está, muestra un mensaje y termina. Si hay trabajos, toma el que está al frente, muestra su ID y el documento que se está procesando. Después mueve el frente de la cola al siguiente nodo y libera la memoria del trabajo que ya se procesó usando free. Esto se hace porque la cola utiliza memoria dinámica, donde los nodos se crean y eliminan durante la ejecución del programa.

    en caso de ser memoria estatica, es deci , que los trabajos se almacenen en un arreglo, simplemente los datos del arreglo de moveran y se disminuira el tamaño actual del arreglo reutilizando el espacio ya recervado 

* void listarCola(const ColaDinamica *cola);

    atravez de una estructura de repeticion for, se imprimen todos los trabajos que esten guardados la lista o el arreglo dependiendo el tipo de memoria que utilice, imprimirndo los datos de cada uno de los nodos o indices, el id, nombre de ussuario, nombre del documento y nuemro de paginas, ovbiamente tambien verificando que no este vacia la lista o  arreglo

* void destruirCola(ColaDinamica *cola);
  
    esta funcion solo se utiliza en la cesion dos para librerar la memori, esta funcion lo que hace es que con ayuda de una estructura de repeticion, se para nodo por nodo y se libera la memoria individualmente con el comando free() esto para librear el espacio de memoria que utilizava ya que en esa secion utilizamos memoria dinamica, la memoria dinamica requiere que liberemos la memoria manualmente con free() para no ener problemas

## Demostracion de conseptos

## simulacion

## Analisis comparativo


## Conclusiones

## Referencias

GeeksforGeeks. (2024). Queue data structure. GeeksforGeeks. https://www.geeksforgeeks.org/queue-data-structure/

GeeksforGeeks. (2024). Dynamic memory allocation in C using malloc, calloc, free and realloc. GeeksforGeeks. https://www.geeksforgeeks.org/dynamic-memory-allocation-in-c-using-malloc-calloc-free-and-realloc/

Tutorialspoint. (2024). Data structures – queues. TutorialsPoint. https://www.tutorialspoint.com/data_structures_algorithms/dsa_queue.htm

Programiz. (2024). C dynamic memory allocation. Programiz. https://www.programiz.com/c-programming/c-dynamic-memory-allocation