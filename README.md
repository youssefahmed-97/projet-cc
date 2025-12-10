#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <stdbool.h>

bool test_seq(int *i, int *j, int t[], int h[], int n)
{
    *i = 0;
    *j = 0;
    for (int e = 0; e < n; e++)
    {
        for (int k = 0; k < n; k++)
        {
            if ((t[e] == h[k]) && (e == k))
                (*i)++;
            else if ((t[e] == h[k]) && (e != k))
                (*j)++;
        }
    }

    return (*i == n);
}




void tache2(double *s, int t[], int n)
{
    int i = 0;
    int j = 0;
    int m = 0;
    int h[20];
    printf("saisir la sequence : ");
    for (int x = 0; x < n; x++)
        scanf("%d", &h[x]);
    while (test_seq(&i, &j, t, h, n) == 0)
    {
        printf("nombre mal place %d\n", j);
        printf("nombre bien place %d\n", i);
        m++;
        (*s)++;

        printf("saisir la sequence : ");
        for (int x = 0; x < n; x++)
            scanf("%d", &h[x]);
    }

    if (m < 5)
        *s = 100;
    else if (m < 10)
        *s = 80;
    else
        *s = 50;
}




void tache3(double *s, char t[], int n)
{
    int i = 0;
    char c;
    printf("saisir une direction valide (N,E,W,S) : ");
    while ((i < n) && (scanf(" %c", &c)))
    {
        if (c != t[i])
            break;

        i++;
        if (i < n)
            printf("saisir une direction valide (N,E,W,S) : ");
    }

    if (i == n)
    {
        *s = 30;
        for (int j = 0; j < n; j++)
            printf("%c ", t[j]);
    }
    else
    {
        printf("c'est faux\n");
        for (int j = 0; j < n; j++)
            printf("%c ", t[j]);
    }
}





void tache1(double *s, int t[], int cible)
{
    int i = 0;
    int f;
    int j;
    char e;
    char ch[100] = "";
    while (i < 5)
    {
        printf("donner une operation mathematique : ");
        scanf(" %c", &e);

        printf("donner un nombre valide : ");
        scanf("%d", &f);

        printf("donner une nombre valide : ");
        scanf("%d", &j);

        switch (e)
        {
            case '+':
                printf("tu ne peut pas utiliser (%d,%d) mais vous pouvez utiliser (%d)\n", f, j, f + j);
                sprintf(ch, "%d + %d = %d", f, j, f + j);
                break;

            case '-':
                printf("tu ne peut pas utiliser (%d,%d) mais vous pouvez utiliser (%d)\n", f, j, f - j);
                sprintf(ch, "%d - %d = %d", f, j, f - j);
                break;

            case '*':
                printf("tu ne peut pas utiliser (%d,%d) mais vous pouvez utiliser (%d)\n", f, j, f * j);
                sprintf(ch, "%d * %d = %d", f, j, f * j);
                break;

            case '/':
                if (j != 0)
                {
                    printf("tu ne peut pas utiliser (%d,%d) mais vous pouvez utiliser (%d)\n", f, j, f / j);
                    sprintf(ch, "%d / %d = %d", f, j, f / j);
                }
                break;
        }

        printf("%s", ch);
        i++;
    }

    if (i <= 5)
        *s = 50;
}
void tache4(double *s,int a[],int l,int n,int h[] )
{
    char operation[50];
    int e = 0;
    int c = 0;
    int i , j;
    int t;
    int d = 0;
    while (e + c < l)
    {
        printf("donner operation que voulez vous effectuez echange ou comparaion ");
        scanf("%s", operation);

        if ((operation[0] == '<') || (operation[0] == '>'))
        {
            e++;
        }
        else if (strcmp(operation, "echange") == 0)
        {
            printf("donner indice ");
            scanf("%d", &i);
            printf("donner indice ");
            scanf("%d", &j);
            c++;

            t = a[i];
            a[i] = a[j];
            a[j] = t;
        }

        d = 0;
        for (int r = 0; r < n; r++)
        {
            if (h[r] == a[r])
                d++;
        }

        if (d == n)
        {
            *s = 30;
            return;
        }
    }
}






int main()
{
    char tab[10] = {'N','E','W','E','S','S','S','E','S','S'};
    int cible;
    int t[6];
    int i;
    double s = 0;
    int l[6] = {7, 2, 3, 6, 4, 5};

    printf("entrer le numero de competition que voulez vous entrer : ");
    scanf("%d", &i);

    srand(time(NULL));

    switch (i)
    {
        case 1:
            for (int j = 0; j < 6; j++)
                t[j] = rand() % 100;

            cible = rand() % 100;
            tache1(&s, t, cible);
            printf("votre score est (%f)", s);
            FILE *f1 = fopen("score1.txt", "w");
            fprintf(f1, "%f", s);
            fclose(f1);
            break;

        case 2:
            tache2(&s, l, 6);
            printf("votre score est (%f)", s);
            FILE *f2 = fopen("score2.txt", "w");
            fprintf(f2, "%f", s);
            fclose(f2);
            break;

        case 3:
            tache3(&s, tab, 10);
            printf("votre score est (%f)", s);
            FILE *f3 = fopen("score3.txt", "w");
            fprintf(f3, "%f", s);
            fclose(f3);
            break;

        case 4:
        {
            int a[6] = {7,2,3,6,4,5};
            int h[6] = {2,3,4,5,6,7};
            tache4(&s, a, 10, 6, h);
            printf("votre score est (%f)", s);
            FILE *f4 = fopen("score4.txt","w");
            fprintf(f4,"%f", s);
            fclose(f4);
            break;
        }
    }

    return 0;
}

