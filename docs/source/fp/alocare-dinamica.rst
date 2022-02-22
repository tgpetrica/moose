ALOCARE DINAMICA
================

In scrierea ``int a[10]`` avem alocat static 10 casute de tip int pentru variabila ````a``. Intre paranteze ``[]`` trebuie neaparat sa apara o constanta. La alocarea statica trebuie sa cunoasteam, inca din momentul redactarii codului care este lungimea maxima a zonei de memorie pe care o vom folosi, in exemplul de mai sus, pentru vectorul ``a``.

In momentul rularii aplicatiei, de cele mai multe ori, din contextul executiei programului se poate determina lungimea zonei de memorie necesara executiei. De aceea, de cele mai multe ori se prefera ca pentru vectori, matrice, etc. sa se aloce dinamic memorie in momentul executiei aplicatiei. 

Avantaje:

- putem aloca exact atata memorie cat avem nevoie
- putem elibera oricand zonele de memorie de care nu mai avem nevoie
- dinamic, putem aloca memorie mult mai mult decat static.

Pentru a aloca dinamic in C se folosesc urmatoarele functii: ``malloc``, ``calloc``, ``realloc``, free Functiile de mai sus sunt in ``stdlib.h`` si ``malloc.h``

``malloc(int)`` - nr de octeti de memorie ce se doreste sa fie alocat. Functia returneaza un pointer catre ``void``. In cazul in care alocarea s-a facut cu succes, se returneaza adresa de memorie a zonei alocatie dinamic. In caz de insucces, se returneaza ``NULL``.

.. code-block:: c
    :linenos:

    int* x=(int*)malloc(sizeof(int));
    int* a=(int*)malloc(n*sizeof(int));
    if(a==NULL) exit(1);

``a`` retine adresa de inceput a vectorului; constanta ``NULL`` are valoarea ``0``

Un pointer care are valoarea ``NULL`` inseamna ca nu retine nicio adresa de memorie.

``calloc`` primeste 2 param : primul reprezinta nr de blocuri de memorie ce se doreste 

``calloc`` se potriveste pentru alocare de mamorie pt un vector

Spre deosebire de ``malloc``, functia ``calloc`` initilizeaza toti octetii de memorie zonei de memorie alocate dinamic cu valoarea ``0``. In consecinta un apel ``calloc`` este mai lent decat un apel ``malloc`` echivalent.

``realloc(void*, int)`` - functia ``realloc`` realoca memoria de la adresa primita in primul parametru la o alta adresa. Noua locatie de memorie va avea lungimea in octeti specificata de al doilea parametru. Daca alocarea este cu succes pentru noua locatie, informatia de la adresa din primul parametru este copiata la noua adresa.

.. code-block:: c
    :linenos:

    int n, *a;
    ...
    n=(int*)realloc(n*sizeof(int));
    ...
    a=2;
    a=(int*)realloc(a,n*sizeof*(int));

Daca lungimea noii zone de memorie este mai mica, atunci de la adresa initiala se copiaza exact atatia octeti cati am precizat in al doilea parametru.

``free(void*)`` - elibereaza zona de memorie alocata dinamic de la adresa primita ca parametru cu ``free`` putem dealoca doar o zona de memorie alocata cu succes al uneia dintre functiile ``malloc``, ``calloc`` sau ``realloc``.

Daca se incearca sa se aloca memorie de valoare negativa, fucntia returneaza valoarea ``NULL``. Daca se incearca a se aloca ``0`` octeti, in functie de compilator, functia va returna adresa ``NULL`` sau o adresa de memorie unde evident nu avem casute.

.. code-block:: c
    :linenos:

    int a[10];
    int n=10;
    int *b=(int*)malloc(n*sizeof(int));
    printf("%d %d",sizeof(a),sizeof(b));    //=> 40 4

Variabila a retine adresa de memorie a unei zone de lungime 40 de octeti in stiva de executie, iar b este un pointer catre int si orice pointer se reprezinta pe 4 octeti.

In momentul in care alocam dinamic memorie si o zona astfel alocata nu este eliberata spunem ca avem "memory leak".

Dezavantajele memory leak:

- zonele alocate dinamic si neeliberate pe parcursul executiei aplicatiei pot creste ca numar si ca dimensiune, existand riscul, ca executia aplicatiei sa nu se mai poata executa, ne mai existand memorie pentru a fi alocata dinamic.
- prin acumularea zonelor neeliberate, calculatorului i se va ingreuna functionalitatea
- la inchiderea unei aplicatii cu memory leak, OS va identifica si verifica zonele de memorie alocate dinamic neeliberate pe parcursul executiei, proces care este lent sau extrem de lent.
