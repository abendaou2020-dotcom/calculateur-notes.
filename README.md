/*
 * gestion_notes.c
 *
 * Saisie des notes d'etudiants (entre 0 et 20), puis affichage
 * de la note maximale et de la moyenne.
 *
 * Compilation : gcc -Wall -Wextra -std=c11 -o gestion_notes gestion_notes.c
 * Execution   : ./gestion_notes
 */

#include <stdio.h>
#include <stdlib.h>

#define NB_NOTES_MAX 100
#define NOTE_MIN     0.0f
#define NOTE_MAX     20.0f

/* Vide le tampon d'entree jusqu'a la fin de la ligne (ou la fin de l'entree). */
static void vider_tampon(void)
{
    int c;

    while ((c = getchar()) != '\n' && c != EOF) {
        /* rien a faire */
    }
}

int main(void)
{
    float notes[NB_NOTES_MAX];
    float somme = 0.0f;
    float note_maximale = NOTE_MIN;
    int n;

    printf("Ce programme permet de gerer les notes des etudiants\n\n");

    printf("Saisir le nombre de notes : ");
    if (scanf("%d", &n) != 1 || n < 1 || n > NB_NOTES_MAX) {
        fprintf(stderr, "Erreur : le nombre de notes doit etre compris entre 1 et %d.\n",
                NB_NOTES_MAX);
        return EXIT_FAILURE;
    }

    for (float *p = notes; p < notes + n; p++) {
        float note;
        int valide = 0;

        while (!valide) {
            int lu;

            printf("Saisir la note %d : ", (int)(p - notes) + 1);
            lu = scanf("%f", &note);

            if (lu == EOF) {
                fprintf(stderr, "\nErreur : fin de l'entree inattendue.\n");
                return EXIT_FAILURE;
            }

            if (lu != 1) {
                printf("Erreur : veuillez saisir une note valide.\n");
                vider_tampon();
                continue;
            }

            /* Ecrit ainsi, le test rejette aussi la valeur "nan". */
            if (!(note >= NOTE_MIN && note <= NOTE_MAX)) {
                printf("Erreur : la note doit etre comprise entre %.0f et %.0f.\n",
                       NOTE_MIN, NOTE_MAX);
                continue;
            }

            valide = 1;
        }

        *p = note;
        somme += note;

        if (note > note_maximale) {
            note_maximale = note;
        }
    }

    printf("\nLa note maximale est : %.2f\n", note_maximale);
    printf("La moyenne des notes est : %.2f\n", somme / n);

    return EXIT_SUCCESS;
}
