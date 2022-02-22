.. code-block:: c
   :linenos:

    #include <stdio.h>
    #include <conio.h>
    #include <stdlib.h>
    #include <process.h>
    #include <alloc.h>

    void EroareAloc ()
    {
        printf("Eroare! Memorie insuficienta.");
        exit(1);
    }

    float** MatrAlloc (int m, int n)
    {
        int i;
        float **a;
        if ((a = float**)calloc(m,sizeof(float)) == NULL)
            EroareAloc();
        for (i = 0; i < m; i++)
            if ((a[i] = (float*)calloc(n,sizeof(float))) == NULL)
                EroareAloc();
        return a;
    }

    void main(void)
    {
        char numef[100];
        int i, j, k, m, n, n2, p;
        float **a, **b, **c, f;
        FILE *fis;
        printf("Dati numele fisierului text cu prima matrice: ");
        gets(numef);
        fis = fopen(numef,"rt");
        if (fis == NULL)
        {
            printf("Eroare! Nu am putu deschide %s pt citire.\n", numef);
            getch();
            exit(0);
        }
        fscanf(fis, "%d%d", &m, &n);
        a = MatrAlloc (m, n);
        for (i = 0; i < m; i++)
        {
            for (j=0; j < n; j++)
            {
                fscanf (fis, "%f", &f);
                a[i][j] = f;
                printf ("%10.2lf", a[i][j]);
            }
            puts("");
        }
        fclose (fis);
        printf ("dati numele fisierului text cu a doua matrice: ");
        gets(numef);
        fis = fopen (numef, "rt");
        if (fis == NULL)
        {
            printf("Eroare! Nu am putu deschide %s pt citire.\n", numef);
            getch();
            exit(0);
        }
        fscanf(fis, "%d%d", &n2, &p);
        if(n != n2)
        {
            fclose(fis);
            printf("\nEroare! Matricile nu se pot inmulti: \n");
            printf(" A(%d,%d) x B(%d.%d) \n", m, n, n2, p);
            getch();
            exit(0);
        }
        b = MatrAlloc (n, p);
        for (i = 0; i < n; i++)
        {
            for (j = 0; j < p; j++)
            {
                fscanf (fis, "%f", &s);
                b[i][j] = f;
                printf ("%10.2lf", b[i][j]);
            }
            puts("");
        }
        fclose (fis);
        printf ("Dati numele fisierului in care sa se puna rezultatul: ");
        gets(numef);
        if (fis == NULL)
        {
            printf("Eroare! Nu am putut deschide %s pt scriere. \n", numef);
            getch();
            exit(0);
        }
        fis = fopen (numef, "wt");
        c = MatrAlloc (m, p);
        for (i = 0; i< m; i++)
            for (j = 0; j < p; j++)
            {
                c[i][j] = 0;
                for (k = 0; k < n; k++)
                    c[i][j] += a[i][k] * b[k][j];
            }
        for (i = 0; i< m; i++)
        {
            for (j = 0; j < p; j++)
            {
                printf("%10.2f", c[i][j]);
                fprintf(fis, "%10.2f", c[i][j]);
            }
            printf("\r\n");
            fprintf(fis, "\r\n");
        }
        for (i = 0; i < m; i++)
            free(a[i]);
        for (i = 0; i < n; i++)
            free(a[i]);
        for (i = 0; i < m; i++)
            free(a[i]);
        free(a);
        free(b);
        free(c);
        fclose (fis);
        getch();
    }