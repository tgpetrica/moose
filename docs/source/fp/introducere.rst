INTRODUCERE IN LIMBAJUL C
=========================

Un fisier sursa are extensia ``.c``. Intr-un fisier C pot aparea:

- includeri
- macrocomenzi
- definitii tipuri de date
- definitii de constante globale
- definitii de variabile globale
- antete / definitii de functii

La intalnirea ``#`` compilatorul intelege ca urmeaza informatii cu privire la compilare. Dupa ``#`` poate aparea cuvantului include urmat de numele unui fisier dat intre ``<>`` sau ``""``. La compilare, fisierul respectiv este cautat pe drive si ceea ce gaseste in acel fisier va fi folosit la compilarea fisierului curent. 

``<>`` - cautat in folderul de fisiere antet ale compilatorului (mediului de programare). Acest folder pe disk are denumirea de include. Aici se gasesc, de regula, fisierele antet standard ale limbajului C.

exemple: ``stdio.h``, ``conio.h``, ``stdi.h``, ``string.h``

``""`` - cautat atat in folderul include cat si in caile curente de cautare. De regula, includerea presupune un fisier antet (cu extensia ``.h`` - header); putem include si alte fisiere cu extensia ``.c``.

Intr-un fisier antet pot aparea aceleasi elemente enumerate anterior, insa, intr-un fisier antet nu se scriu definitii de functii, ci numai antete de functii.

pentru parametri putem da / omite denumiri;

antetul unei functii se incheie cu ;

.. code-block:: c
    :linenos:

    int test();
    int max (int, int);
    int min (int a, int b);

Rolul fisierelor antet:

- la compilarea unui proiect, fiecare fisier din acel proiect este compilat separat; in momentul in care se intalneste un apel de functie intr-un fisier ``.c`` si acea functie nu este implementat in acel fisier se cauta antetul functiei apelate intr-unul dintre fisierele ``.h``.
- daca apelul se potriveste cu antetul gasit, se trece mai departe cu compilarea acelui fisier.
- in C, semnatura unei functii este data de numele acele functii; prin semnatura functiei intelegem caracteristicile dupa care o functie este cautata la compilare.
- din cauza ca in C, semnatura unei functii este data de numele ei, nu putem avea mai multe functii in acelasi proiect cu acelasi nume si cu parametri diferiti, asa cum este acceptat in C++, unde semnatura este data de nume, nr de parametri si tipurile de date ale parametrilor.
- dupa ce toate fisierele programului au fost compilate cu succes se trece la etapa de link-edit-are, unde se fac legaturile dintre codurile obiect, rezultate in urma compilarii fisierelor sursa. in exemplul nostru, apelul ``max(1,2)`` se va transmite unei functii implementate cu numele ``max`` si cu 2 parametri ``int``. dintr-un alt fisier sursa compilat sau dintr-un fisier care deja exista compilat.
- fisierele C compilate sunt fisiere cu extensia ``.obj``, ``.lib`` sau fisiere externe: ``file.obj`` se obtine in urma compilarii unui fisier C; ``file.lib`` sunt biblioteci statice care contin o multitudie de functii compilate; fisierele ``file.obj`` si ``file.lib`` sunt conectate de catre link-editor pentru a finaliza crearea fisierului executabil ``.exe``.
- exista posibilitatea ca unele functii sa fie implementate in biblioteci externe, apelurile acestor functii nefiind include in fisierul executabil, apelurile acestor functii identificandu-se atunci cand programul se lanseaza in executie; fisierele externe in care se afla astfel de functii poarta numele de biblioteci dinamice; sub Win OS, acestea au extensia ``.dll``.

Declaratii variabile globale
----------------------------

Intr-un fisier sursa C cu extensia ``.h`` / ``.c`` putem declara variabile in exteriorul functiilor, devenind astfel variabile globale cunoscute in intreg proiectul. O variabila globala este cunoscuta din locul declararii in jos. Nu este recomandat a se folosi variabile globale.



.. code-block:: c
    :linenos:

    tipdate var;
    tipdate var = val;

In momentul intalnirii unei declaratii de var globala, respectiva var intra in stiva de executie si la iesirea blocului din care este declarata, var paraseste stiva de executie. De asemenea, putem avea si constate globale (nerecomandat). La compilare, orice referire la const in program este inlocuita cu valoarea constantei; o constanta se defineste:

.. code-block:: c
    :linenos:

    const tipdate numeCst = val;

