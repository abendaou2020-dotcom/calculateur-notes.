#include <stdio.h>

int main() {
    int choix;
    float coef, cc, exam, moyenne;
    float total_points = 0;
    float total_coeffs = 0;
    int nombre_modules = 0;

    do {
        printf("\n=========================================\n");
        printf("   CALCULATEUR DE NOTES - EMSI (Simple)\n");
        printf("=========================================\n");
        printf("1. Ajouter un module et calculer sa moyenne\n");
        printf("2. Afficher la moyenne generale du semestre\n");
        printf("3. Quitter\n");
        printf("Votre choix : ");
        
        scanf("%d", &choix);

        // --- FONCTION CONDITIONNELLE PRINCIPALE (switch) ---
        switch (choix) {
            case 1:
                printf("\n--- Ajout d'un module ---\n");
                
                printf("Entrez le coefficient du module : ");
                scanf("%f", &coef);
                
                printf("Entrez la note de CC (sur 20) : ");
                scanf("%f", &cc);
                
                printf("Entrez la note d'Examen (sur 20) : ");
                scanf("%f", &exam);

                // Validation conditionnelle basique des notes
                if (cc < 0 || cc > 20 || exam < 0 || exam > 20 || coef <= 0) {
                    printf("[ERREUR] Les notes doivent etre entre 0 et 20, et le coef > 0.\n");
                } else {
                    // Calcul de la moyenne du module : 40% CC + 60% Examen
                    moyenne = (cc * 0.4f) + (exam * 0.6f);
                    printf("--> Moyenne de ce module : %.2f / 20\n", moyenne);

                    // Cumul pour la moyenne générale
                    total_points += moyenne * coef;
                    total_coeffs += coef;
                    nombre_modules++;
                }
                break;

            case 2:
                // --- FONCTION CONDITIONNELLE (if / else) ---
                if (nombre_modules == 0) {
                    printf("\nAucun module enregistre pour le moment.\n");
                } else {
                    float moyenne_generale = total_points / total_coeffs;
                    
                    printf("\n=========================================\n");
                    printf("Nombre de modules valides : %d\n", nombre_modules);
                    printf("Moyenne Generale : %.2f / 20\n", moyenne_generale);
                    
                    // Condition de validation du semestre
                    if (moyenne_generale >= 10.0f) {
                        printf("Statut : SEMESTRE VALIDE \n");
                    } else {
                        printf("Statut : RATTRATAGE / NON VALIDE \n");
                    }
                    printf("=========================================\n");
                }
                break;

            case 3:
                printf("\nAu revoir et bon courage pour vos etudes a l'EMSI !\n");
                break;

            default:
                printf("\n[ERREUR] Choix invalide. Veuillez choisir entre 1, 2 et 3.\n");
        }

    } while (choix != 3); // La boucle continue tant qu'on ne choisit pas de quitter

    return 0;
}
