# 1. Organisation des dossiers du projet

- `/bin` : Dossier pour les exécutables compilés
  - `main` : Programme principal
  - `test_fahrenheit` : Fichier exécutable pour tester la conversion
- `/src` : Code source
  - `main.c` : Programme principal
  - `fahrenheit.c` : Implémentation de la fonction de conversion Fahrenheit -> Celsius
  - `fahrenheit.h` : Déclaration des prototypes de fonction pour la conversion
- `/tests` : Fichiers de tests
  - `test_fahrenheit.c` : Fichier pour tester la fonction de conversion
- `/docs` : Documentation
  - `explication_architecture_fichier.c` : Explications détaillées sur l'architecture du projet


# 2. Structure du projet

```c
/mon_projet  
│  
├── /bin                     # Dossier des exécutables  
│   ├── main                 # Programme principal  
│   └── test_fahrenheit      # Fichier exécutable pour tester la conversion  
│  
├── /src                     # Dossier des sources  
│   ├── main.c               # Programme principal  
│   ├── fahrenheit.c         # Implémentation de la fonction de conversion Fahrenheit -> Celsius  
│   └── fahrenheit.h         # Déclaration des prototypes de fonction pour la conversion  
│  
├── /tests                   # Dossier des tests  
│   └── test_fahrenheit.c    # Fichier pour tester la fonction de conversion  
│  
├── /docs                    # Documentation et explications  
│   └── explication_architecture_fichier.c  # Explications détaillées sur l'architecture du projet  
│  
└── Makefile                 # Fichier pour automatiser la compilation
```

## Contenu des fichiers `/src`
En C, chaque fonctionnalité du programme est généralement divisée en deux fichiers : un fichier .c et un fichier .h. 

- Le fichier .c contient le code qui réalise l’action (la logique de la fonction).
- Le fichier .h contient la déclaration des fonctions, c'est-à-dire leur nom, type de retour et paramètres, mais sans le code. Il permet aux autres fichiers de savoir quelles fonctions existent et comment les utiliser sans avoir besoin de connaître leur fonctionnement détaillé. Cela aide à organiser le programme et à éviter des erreurs.

### Le fichier fahrenheit.h
Le fichier fahrenheit.h est un fichier d'en-tête (header file) qui contient des déclarations nécessaires pour l'utilisation de la fonction de conversion de Fahrenheit en Celsius dans d'autres fichiers source, comme fahrenheit.c et main.c.
Contenu de fahrenheit.h :
```c
#ifndef FAHRENHEIT_H
#define FAHRENHEIT_H

int fahrenheitToCelsius(int fahr); // Déclaration de la fonction

#endif
```
### Introduction aux concepts de base
Avant de commencer, quelques notions sont importantes pour comprendre les lignes de code que tu mentionnes.
- Préprocesseur : C’est un programme qui s'exécute avant la compilation proprement dite. Il traite les directives spéciales que l’on met dans le code, comme #include, #define, ou #ifndef. Le préprocesseur manipule le code source avant qu'il ne soit compilé.
- Macro : Une macro est une sorte de "recherche et remplacement" que fait le préprocesseur. Par exemple, une macro peut être utilisée pour remplacer un nom de constante ou une partie de code par un autre, avant même que le programme ne soit compilé. Cela permet de simplifier le code et d'éviter les répétitions.

    Préprocesseur : C’est un programme qui s'exécute avant la compilation proprement dite. Il traite les directives spéciales que l’on met dans le code, comme #include, #define, ou #ifndef. Le préprocesseur manipule le code source avant qu'il ne soit compilé.

    Macro : Une macro est une sorte de "recherche et remplacement" que fait le préprocesseur. Par exemple, une macro peut être utilisée pour remplacer un nom de constante ou une partie de code par un autre, avant même que le programme ne soit compilé. Cela permet de simplifier le code et d'éviter les répétitions.

Les directives de préprocesseur (#ifndef, #define, #endif) :
```c
#ifndef FAHRENHEIT_H
#define FAHRENHEIT_H
#endif
```
    
#### 1. ifndef 
signifie "If Not Defined" en anglais, ou "Si non défini" en français.
- Cela veut dire : "Si la macro FAHRENHEIT_H n’est pas encore définie".
- Si FAHRENHEIT_H n'est pas encore défini, alors le code entre #ifndef et #endif va être exécuté.

Cela sert à dire au préprocesseur qu'il doit vérifier si la macro FAHRENHEIT_H existe déjà. Si elle n'existe pas, il va inclure le code qu'il y a après. Si la macro existe déjà (c’est-à-dire si le fichier a déjà été inclus), alors le préprocesseur ignorera ce bloc de code.

#### 2. define FAHRENHEIT_H (Définir FAHRENHEIT_H)
-define est une directive de préprocesseur qui permet de définir une macro. Cela signifie que tu donnes un nom (dans ce cas, FAHRENHEIT_H) et tu le "définis" pour qu'il existe dans ton programme.
-Une fois qu'une macro est définie, son nom peut être utilisé pour vérifier dans d'autres parties du programme, afin de savoir si une certaine section de code a déjà été incluse ou non.

Dans ton exemple, #define FAHRENHEIT_H sert à dire "Maintenant, la macro FAHRENHEIT_H existe". Cela indique au préprocesseur qu'il a déjà inclus ce fichier d'en-tête et qu'il ne doit pas le réinclure si cela se reproduit.

#### 3. endif (Fin de la condition)

- endif est une directive de préprocesseur qui marque la fin d'une section conditionnelle commencée avec #if, #ifndef ou #ifdef.
- Dans ce cas, cela marque la fin de la section conditionnelle où le préprocesseur a vérifié si la macro FAHRENHEIT_H était déjà définie.

Donc, #endif signifie simplement "fin de la condition". Cela indique que le bloc conditionnel est terminé et que le préprocesseur peut continuer avec le reste du code.


### Le fichier fahrenheit.c
```c
#include "fahrenheit.h"

int fahrenheitToCelsius(int fahr) {
    return 5 * (fahr - 32) / 9;
}
```
#### 1. #include "fahrenheit.h"

Cette ligne permet d'inclure le fichier d'en-tête fahrenheit.h dans le fichier source fahrenheit.c. Cela permet au fichier fahrenheit.c d'avoir accès aux déclarations des fonctions ou variables définies dans fahrenheit.h.

L'inclusion de ce fichier est essentielle pour lier correctement le code de la fonction que nous allons définir ici, fahrenheitToCelsius(), avec son prototype qui a été déclaré dans fahrenheit.h.

#### 2. Définition de la fonction fahrenheitToCelsius
```c
int fahrenheitToCelsius(int fahr) {
    return 5 * (fahr - 32) / 9;
}
```

- int fahrenheitToCelsius(int fahr) : Cette ligne définit la fonction fahrenheitToCelsius qui prend un paramètre d'entrée fahr (température en degrés Fahrenheit) et retourne la température convertie en degrés Celsius (de type int).
- Calcul de la conversion Fahrenheit → Celsius.
- Retour de la valeur : La valeur calculée est retournée en tant qu'entier (int). Cela signifie que la partie décimale est perdue lors de la conversion.

#### 3. Rôle du fichier fahrenheit.c

Le fichier fahrenheit.c contient la définition des fonctions déclarées dans le fichier d'en-tête fahrenheit.h. En d'autres termes, ce fichier contient l'implémentation réelle de la fonction fahrenheitToCelsius.

#### Pourquoi ce fichier est important ?

- Séparation des responsabilités : En séparant la déclaration des fonctions (dans le fichier .h) et leur implémentation (dans le fichier .c), on permet à d'autres fichiers de se concentrer sur l'utilisation des fonctions sans avoir à connaître les détails de leur fonctionnement interne.
- Réutilisation du code : Cela permet également de réutiliser facilement la fonction fahrenheitToCelsius dans d'autres parties du programme, simplement en incluant fahrenheit.h là où il est nécessaire. D'autres fichiers pourront appeler cette fonction sans avoir besoin de réécrire la logique de conversion.


### Le fichier main.c
```c
#include <stdio.h>
#include "fahrenheit.h"

int main(void) {
    int fahr = 100;
    printf("%d Fahrenheit = %d Celsius\n", fahr, fahrenheitToCelsius(fahr));
    return 0;
}
```

#### 1. #include <stdio.h>

Cette ligne inclut la bibliothèque standard stdio.h (standard input/output) qui permet d'utiliser des fonctions d'entrée et de sortie, telles que printf, pour afficher des informations à l'écran ou lire des entrées de l'utilisateur.
- printf est une fonction de cette bibliothèque qui permet d'afficher des textes formatés à l'écran.

#### 2. #include "fahrenheit.h"
Cette ligne inclut le fichier d'en-tête fahrenheit.h dans le fichier main.c.

- Comme expliqué précédemment, cela permet de déclarer les fonctions et les variables qui seront utilisées dans ce fichier. Ici, le fichier fahrenheit.h déclare la fonction fahrenheitToCelsius, ce qui permet à main.c de l'utiliser sans avoir besoin de connaître son implémentation (qui se trouve dans fahrenheit.c).

#### 3. int main(void)
```c
int main(void) {}
```
Cette ligne définit la fonction principale main, qui est le point d'entrée de tout programme en C. Le programme commence ici et s'exécute à partir de cette fonction.

- int : Cela signifie que la fonction main retourne une valeur entière à la fin de son exécution, généralement pour indiquer si le programme s'est terminé correctement ou s'il y a eu une erreur.
- Ici, nous retournons 0, ce qui signifie que le programme s'est terminé sans erreurs.
- void : Cela signifie que la fonction main ne prend aucun argument.

#### 4. Déclaration et initialisation de la variable fahr
```c
int fahr = 100;
```
- int fahr = 100; : Cette ligne déclare une variable fahr de type int (entier) et lui assigne la valeur 100. Cette variable représente une température en degrés Fahrenheit que nous voulons convertir en degrés Celsius.

#### 5. Appel de la fonction fahrenheitToCelsius et affichage du résultat
```c
printf("%d Fahrenheit = %d Celsius\n", fahr, fahrenheitToCelsius(fahr));
```
- printf : La fonction printf est utilisée pour afficher du texte formaté à l'écran.
- "%d" : C'est un specifier de format qui indique que l'on souhaite afficher un nombre entier. Dans ce cas, nous affichons fahr et la valeur retournée par la fonction fahrenheitToCelsius.
- fahrenheitToCelsius(fahr) : Cela appelle la fonction fahrenheitToCelsius que nous avons définie dans fahrenheit.c. Cette fonction prend en entrée la température en Fahrenheit (ici 100) et retourne la température convertie en Celsius. Le résultat est affiché dans le message.

#### 6. Retourner 0 et fin du programme
```c
return 0;
```
- Cela signifie que le programme s'est terminé avec succès. 0 est généralement retourné pour indiquer qu'aucune erreur n'est survenue durant l'exécution du programme.


## Contenu des fichiers `/Makefile`
Un Makefile est un fichier qui automatise la compilation et l’exécution de ton projet en C. Il permet d'éviter d'écrire manuellement des commandes gcc à chaque fois.

```c
# Nom du compilateur
CC = gcc  # On utilise GCC comme compilateur

# Dossiers
SRC_DIR = src    # Dossier contenant les fichiers sources (.c)
TEST_DIR = tests # Dossier contenant les fichiers de tests
BIN_DIR = bin    # Dossier où seront placés les exécutables

# Fichiers sources
SRC_FILES = $(SRC_DIR)/fahrenheit.c $(SRC_DIR)/main.c # Liste des fichiers sources du programme
TEST_FILES = $(TEST_DIR)/test_fahrenheit.c            # Fichier source pour les tests
OBJ_FILES = $(SRC_DIR)/fahrenheit.o $(SRC_DIR)/main.o # Liste des fichiers objets (compilés)

# Options de compilation
CFLAGS = -Wall -Wextra -pedantic -std=c11  # Active les warnings et force le standard C11

# Cible par défaut : compilation du programme et des tests
all: bin/main bin/test_fahrenheit  # Lorsque "make" est exécuté sans argument, il compile ces cibles

# Compilation du programme principal
bin/main: $(SRC_FILES)
	$(CC) $(CFLAGS) $(SRC_FILES) -o bin/main  # Compile tous les fichiers sources et génère l'exécutable "bin/main"

# Compilation des tests
bin/test_fahrenheit: $(TEST_FILES) $(SRC_DIR)/fahrenheit.c
	$(CC) $(CFLAGS) $(TEST_FILES) $(SRC_DIR)/fahrenheit.c -o bin/test_fahrenheit  
	# Compile le fichier de test avec la logique du programme pour produire "bin/test_fahrenheit"

# Exécuter les tests
test: bin/test_fahrenheit
	./bin/test_fahrenheit  # Exécute les tests en lançant l'exécutable généré

# Nettoyage des fichiers compilés
clean:
	rm -rf bin/* *.o *.dSYM  # Supprime tous les fichiers compilés pour repartir de zéro

```

## Contenu des fichiers `/tests`


```c
#include <stdio.h>               // Inclusion de la bibliothèque standard pour les entrées/sorties (printf).
#include <assert.h>              // Inclusion de la bibliothèque pour les assertions (assert).
#include "../src/fahrenheit.h"   // Inclusion de l'en-tête du fichier "fahrenheit.h" qui contient les déclarations de fonctions (par exemple fahrenheitToCelsius).

// Fonction de test pour vérifier la conversion Fahrenheit -> Celsius
void test_fahrenheitToCelsius(void) {
    printf("Début des tests Fahrenheit -> Celsius...\n");  // Affiche un message indiquant que les tests commencent.

    // Tableau des valeurs de test en Fahrenheit
    int test_values[] = {32, 212, 98, 0, 300}; 

    // Tableau des résultats attendus pour chaque valeur en Celsius (en fonction de la conversion correcte)
    int expected_results[] = {0, 100, 36, -17, 148}; 

    // Détermination du nombre de tests (taille du tableau de test)
    int num_tests = sizeof(test_values) / sizeof(test_values[0]);

    // Boucle à travers les valeurs de test
    for (int i = 0; i < num_tests; i++) {
        // Appel de la fonction fahrenheitToCelsius pour chaque valeur
        int result = fahrenheitToCelsius(test_values[i]);

        // Affichage des résultats du test : la valeur testée, le résultat obtenu et le résultat attendu
        printf("Test %d: fahrenheitToCelsius(%d) = %d (attendu: %d)\n", 
               i + 1, test_values[i], result, expected_results[i]);

        // Vérification que le résultat de la fonction est correct en utilisant assert
        assert(result == expected_results[i]);
    }
    
    // Si tous les tests passent sans erreur, message de succès
    printf("Tous les tests sont passés avec succès !\n");
}

// Fonction principale pour exécuter les tests
int main(void) {
    test_fahrenheitToCelsius();  // Appel de la fonction de test
    return 0;  // Fin du programme avec un statut de réussite
}

```
