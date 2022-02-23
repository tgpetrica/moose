MACROCOMENZI
============

abbr. MCA

MCA poate fi considerata o generalizare a conceptului de constanta, in sensul ca referirea la o macrocomanda este inlocuita la compilare cu corpul macrocomenzii; MCA se expandeaza la compilare intr-o secventa de cod descrisa in corpul MCA. MCA reprezinta un suport foarte puternic pt programarea generica in C.

Build:

- precompilare
- compilare
- link editare

Inainte de a se trece la compilare pot exista cateva prelucrari initiale ale codului sursa. Aceste prelucrari sunt specificate de catre programator folosind ``#``.

- ``#include`` : intregi fisiere sunt introduse in locul in care apare includerea (fisiere antet);
- ``#define`` : macrocomenzi;
- precompilare conditionata: ``#ifdef``, ``#if``, etc.

O MCA se specifica cu ``#define``, denumirea macrocomenzii si eventual specificatia expandarii macrocomenzii.

.. code-block:: c
    :linenos:

    #define  ROAD

Dupa denumirea MCA poate sa apara un text care arata modul in care o MCA se expandeaza in cod C.

.. code-block:: c
    :linenos:

    #define PI 3.14159

De fiecare data cand in codul sursa apare cuvantul ``PI``, in etapa de precompilare fiecare aparitie va fi inlocuita cu valoarea din definitie, adica ``3.14159``.

ex.
.. code-block:: c
    :linenos:
    int x = PI;
    //--->precompilare
    int x = 3.14159;

O MCA poate avea parametri; expandarea MCA facandu-se in functie de acesti parametri.

ex

.. code-block:: c
    :linenos:

    #define suma(x,y) x+y
    int n = suma(1,2); //in etapa de precompilare ---> int n = 1+2;
    int expresie = suma(1+2)*2 //in etapa de precompilare ---> int expresie = (1+2)*2; ---> int expresie = 5;

ex

.. code-block:: c
    :linenos:

    #define suma(x,y) (x+y)
    int p = suma(1,2)*2 //---> int p = (1+2)*2; ---> int p = 6;

ex.

.. code-block:: c
    :linenos: 

    #define prod(x,y) ((x)*(y))
    int x = prod(1+2,3+4); //---> int x = (1+2)*(3+4); ---> int x = 3*7; ---> int x = 21;

ex.

.. code-block:: c
    :linenos:

    #define max(x,y) (x>y)?(x):(y)
    int m = max(max(1+2,3+4),5+6);

ex.

.. code-block:: c
    :linenos:

    #define inter(x,y) x=x+y,y=x-y,x=x-y
    int a = 1, b = 2;
    inter(a,b); //---> a=a+b,b=a-b,a=a-b;

Operatorul ``,``
----------------

In limbajul C, virgula ``,`` este operator binar

.. code-block:: c
    :linenos:

    a,b //are valoarea returnata de catre operatorul virgula egala cu valoarea lui b
    int x = 1,2; //x = 2
    int y = ++x,x*2,x+5; // ++x este 3, x*2 este 6, x+5 este 8, deci y = 8
    y = ++x,(x*=2),x+5.9; // double > int     ++x este 4, (x*=2) este 8, x+5.9 este 13.9

Operatorul ``=``
----------------

In limbajul C, egal ``=`` este operatoru binar in care in stanga este o variabila, iar in dreapta o expresie.


.. code-block:: c
    :linenos:

    a=b //valoarea lui b este convertita si atribuita variabilei a (conversie la tipul variabilei a)
    //valoarea returnata de = este cea atribuita lui a
    int x = 1;
    int y = x = 2;
    float u = 1.7f;
    int n = u = 5.9f; //u=5.9 si n=5
    // 1.5 constanta de tip double pe 8 octeti
    // 1.5f constanta de tip float pe 4 octeti

O MCA se poate scrie numar pe o singura linie

ex.

.. code-block:: c
    :linenos:

    #define inter2(x,y,z) z=x;\
                          x=y;\
                          y=z;
    //punand backslash \ compilatorul intelege ca linia curenta continua dedesubt

    int a = 1, b = 2, inte;
    inter2(a,b,inte) 
    //nu este necesar a se pune ; dupa o macrocomanda
    //---> inte = a ; a = b ; b = inte ;
ex.

.. code-block:: c
    :linenos:

    #define inter3(x,y){\
                        int inte = x;\
                        x = z;\
                        y = inte;\
                        }
    inter3(a,b)
    //---> {int inte = a ; a = b ; b = inte ;}

Operatorul ``##``
-----------------

poate fi folosit in cadrul unei MCA

prin ``a##b`` intelegem ca textul a este lipit de textulb, deci ``ab``.

ex

.. code-block:: c
    :linenos:

    #define alip(a,b) a##b
    int intersch = 7;
    alip(inter,sch)++; //---> intersch++; ---> intersch = 8;
    int x = alip(12,3); //---> x = 123
    int y = alip(x+,2); //---> y = x + 2; ---> y = 125;
    int f = 4;
    float u = alip(1+2,0.1f); //---> 1 + 20.1f

ex

.. code-block:: c
    :linenos:

    #define max2(x,y,z) if(x<y)\
                        z=x;\
                        else\
                        z=y;
    int a = 1, b = 2, c;
    max2(a,b,c);

Macrocomenzi standard
---------------------

``__FILE__``: se expandeaza intr-un script continand numele fisierului curent la care s-a ajuns cu compilarea.
ex. fisierul: ``test.c``

.. code-block:: c
    :linenos:

    #include "stdio.h"
    void main(){
        printf(__FILE__); // printf(".../test.c");
    }

``__LINE__`` : se expandeaza intr-un nr intreg reprezentand indicele liniei pe care apare macrocomanda __LINE__
ex.

.. code-block:: c
    :linenos:

    #include "stdio.h"
    void main(){
        printf("%s:%d\n",__FILE__,__LINE__); // printf(".../test.c:4");
    }

``__TIME__`` : se exandeaza intr-un string ce contine ora la care s-a trecut prin precompilare

``__DATE__`` : se exandeaza intr-un string ce contine data la care s-a trecut prin precompilare

.. code-block:: c
    :linenos:

    printf("Eroare: impartire prin 0. Fisier: %s, linia: %d, data si ora compilarii %s %s\n", __FILE__, __LINE__, __DATE__, __TIME__);
    //pe baza acestor informatii putem gasi versiunea exacta a erorii

MCA ``__FILE__``, ``__LINE__``, ``__TIME__``, ``__DATE__`` sunt folosite la depanare. Aceste mesaje se conecteaza de obicei intr-un fisier LOG (log file). Un fisier LOG colecteaza mesaje de-a lungul executiei aplicatiei: valori, atentionari, erori, informatii, etc.

``__STDC__`` :se expandeaza in 1 sau 0 dupa cum compilatorul respecta sau nu standardul ISO

``__STDC_VERSION__	se expandeaza intr-un nr intreg de tip long si acesta reprezinta versiunea standard de compilare (pt ce versiune de C a fost implentat) in formatul YYYYMM

``__cplusplus``: se expandeaza in 1 daca si numai daca avem de-a face cu un compilator de C++

``__OBJC__``: "C++ de la Apple"

``__ASSEMBLER__``:verifica daca prepocesarea se face in limbaj assembler

``_WIN64``:	este sau nu compilator pentru Windows x64

``_WIN32``:	este sau nu compilator pentru Windows x32

``__APPLE__``: rezulta cod executabil pentru Apple

``__linux``:	verific daca sunt sub mediul Linux

``__unix``:	verific daca sunt sub mediul Unix

