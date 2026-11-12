#include <stdio.h>

int main(void) {
    int n;
    float tableau_notes[100], moyenne, somme = 0.0f, note_maximal = 0.0f, *p;

    printf("Ce programme permet de gerer les notes des etudiants\n");
    printf("\nSaisir le nombre de notes : ");
    if (scanf("%d", &n) != 1 || n <= 0 || n > 100) {
        printf("\nErreur : le nombre de notes doit etre compris entre 1 et 100.\n");
        return 1;
    }

    for (p = tableau_notes; p < tableau_notes + n; p++) {
        float note;

        do {
            printf("\nSaisir l'element %d : ", (int)(p - tableau_notes) + 1);
            if (scanf("%f", &note) != 1) {
                printf("\nErreur : veuillez saisir une note valide.\n");
                while (getchar() != '\n');
                note = -1.0f;
                continue;
            }

            if (note < 0.0f || note > 20.0f) {
                printf("\nErreur : la note doit etre comprise entre 0 et 20.");
            }
        } while (note < 0.0f || note > 20.0f);

        *p = note;
        somme += note;

        if (note > note_maximal) {
            note_maximal = note;
        }
    }

    moyenne = somme / n;
    printf("\nLa note maximale est : %.2f ", note_maximal);
    printf("\nLa moyenne des notes est : %.2f\n", moyenne);
    return 0;
}
