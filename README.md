# proj-3
les listes chaine
#include <stdio.h>
#include <stdlib.h>
typedef struct element {
    int val;
    struct element *suivant;
} element;
element* creerListe() {
    return NULL;
}
element* chargerListe(int* Tab, int taille, element* liste) {
    element* courant = liste;
    for (int i = 0; i < taille; i++) {
        element* nouveau = (element*)malloc(sizeof(element)); 
        nouveau->val = Tab[i];
        nouveau->suivant = NULL;
        if (courant == NULL) {
            liste = nouveau;
            courant = liste;
        } else {
            courant->suivant = nouveau;
            courant = courant->suivant;
        }
    }
    return liste;
}

void afficherListe(element* L) {
    element* courant = L;
    while (courant != NULL) {
        printf("%d -> ", courant->val);
        courant = courant->suivant;
    }
    printf("NULL\n");
}
element* supprimerEnFin(element* L) {
    if (L == NULL) {
        return NULL;  
    }

    if (L->suivant == NULL) {
        free(L); 
        return NULL;
    }

    element* courant = L;
    while (courant->suivant != NULL && courant->suivant->suivant != NULL) {
        courant = courant->suivant;
    }
    
    free(courant->suivant);  
    courant->suivant = NULL;  
    return L;
}

element* ajouterEnDebut(element* L, int valeur) {
    element* nouveau = (element*)malloc(sizeof(element));  
    nouveau->val = valeur;
    nouveau->suivant = L;  
    return nouveau; 
}
void viderListe(element* L) {
    element* courant = L;
    while (courant != NULL) {
        element* temp = courant;
        courant = courant->suivant;
        free(temp);  
    }
    printf("La liste est vide\n");
}

int main() {
    int Tab[10] = {1, 3, 5, 7, 8, 10, 9, 11, 13, 20};
    
    element* liste = creerListe();  
    element* L = chargerListe(Tab, 10, liste);  
    afficherListe(L);   
    element* L1 = supprimerEnFin(L);  
    afficherListe(L1);  
    element* L2 = ajouterEnDebut(L1, 40);  
    afficherListe(L2);  
    viderListe(L2);  
    
    return 0;
}
