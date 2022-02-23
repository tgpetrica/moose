UNIUNI SI TIPUL ENUM
====================

UNIUNI
------

Foloseste cuvantul rezervat ``union``. Deosebirea esentiala dintre o uniune si o structura este ca in cazul uniunii folosim acelasi spatiu de memorie.

O uniune se defineste folosind cuvantul rezervat union asemănător cu o structură, diferenţa esenţială dintre o uniune şi o structură este că membrii uniunii folosesc în comun aceeaşi zonă de memorie.

.. code-block:: c
    :linenos:

    union test { char c;  int i;  float f; 79 };

Pentru a reţine o variabilă de tip union sunt necesari 4 octeţi de memorie. În exemplul de mai sus câmpurile c, i şi f ale uniunii se referă toate la aceeaşi zonă din memorie: c se referă la primul octet (din cei patru), i se referă la primii doi octeţi, iar f se referă la toţi cei 4 octeţi.

.. code-block:: c
    :linenos:

    #include "stdio.h"
    #include "conio.h"

    union test \\foloseste aceeasi zona de \\memorie
    {
        char c;
        int i;
        float f;
        double d;
        char st[9];
    };

    struct test2 \\foloseste zona de \\memorie diferita 
    {
        char c;
        int i;
        float f;
        double d;    
        char st[9];
    };

    void main()
    {
        printf("%d %d"\n, sizeof(struct test2), sizeof(union test)); //40 16
        //(x-1)*8 < 40 <= x*8 = 32
        union test u; 
        u.c='A';
        printf("%c %d %f", u.c, u.d, u.f);
        _getch(); 
    }

TIPUL ENUM
----------

.. code-block:: c
    :linenos:

    enum culoare
    {
       CL_BLACK,  //0
       CL_RED,  //1
       CL_GREEN, //2
       CL_BLUE,  //3
       CL_WHITE  //4
    };

    enum tipdrum
    {
        TD_PAMANT,  //0
        TD_PAVAT,  //1
        TD_COMUNAL = 5,
        TD_LOCAL,  //6
        TD_JUDETEAN,  //7
        TD_NATIONAL,  //8
        TD_EUROPEAN = 10,
        TD_AUTOSTRADA =20
     };
    
    enum tipdrum v;
    v=TD_NATIONAL;
    v=(enum tipdrum)7; 

- in interiorul unui enum se enumera constante dar care trebuie sa fie toate intregi
- de regula constantele in C si C++ se dau cu litere mari
- daca definesc un grup de constante, atunci e bine sa aiba toate acelasi prefix
- prefixul se da de forma 2,3 sau 4 constante urmate de _ si apoi denumirea constantei
- pt ca putem sa avem mai multe tipuri de constante pentru diverse situatii

ex: CL - culoare

- intr-un set de constante se prefera sa avem valori diferite pentru fiecare constanta.
- putem avea si valori similare si nu este necesar ca aceste valori sa fie in ordine crescatoare
- le dam denumiri care incep cu acelasi prefix
- in C++, daca avem mai multe tipuri de constante, la un moment dat putem avea de ex tip drum si altul drum, iar utilizatorul vrea sa foloseasca o constanta tip drum, iar pentru asta foloseste o variabila din tip drum, se produce o eroare.