COMPILATOARE
============

.. code-block:: c
    :linenos:

    // # include " stdio.h "
    // int x = 10 ;
    // float f = 2.5f ;
    //fara "f" trimite in double

Un compilator are 2 etape:

- are un analizor lexical
- un analizor sintactic

**Analizor lexical**

cunoaste fel de fel de secvente de caractere consecutive, le recunoaste ca fiind tokeni (sau unitati atomice) exemplu:

- intalneste ``#``, il recunoaste ca fiind token
- intalneste ``define`` - tot token
- gaseste, sa zicem , ``#include`` si dupa ghilimea , dupa care gaseste un text si dupa iar ghilimea (``#include "stdio.h"``) iar el va identifica tokenii din cuvinte el intelege semantica acestor tokeni, isi da seama ca e vorba despre o includere a acestui antet

**Analizor sintactic**

isi da seama ca e vorba de un string

trimiterea de la analizator sintactic la cel lexical se face cu ajutorul campurilor ``union``

analizorul lexical isi va da sema care sunt substantive si care sunt adjective; el le trimite analizorului sintactic, iar daca acesta primeste subst, verb, subst, adj isi da seama de functia sintactica a acestora; le traduce in engleza in ordinea in care trebuie

ex: ana are mere rosii => ana has red apples

Analizoare:

- lex (analizor lexical)
- yacc (yet another compiler compiler)
- bison(linux)