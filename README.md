## Table des Matières
* [Octal, Binary, Hexadecimals & More](#octal-binary-hexadeciaml-&-more)
* [Variables](#variables)
	* [Reading input from user](#reading-input-from-user)
* [Data Types](#data-types)
* [Organisation des dossiers](#organisation-des-dossiers-du-projet)
* [Structure du projet](#structure-du-projet)
* [Notes](#notes)
	
# Octal Binary Hexadeciaml & more
# Variables
Structure en C :
```c
1. Declaration
<type> <nom> ;

2. Assignation
nom = 10;
```

## Reading input from user

En C il faut utiliser la fonction Scanf
```c
1. Declaration
int grade 1;
int grade 2;


// %D = format specifier for integer
// &grade1 = pointer vers grade 1;
scanf(%d, &grade1);
scanf(%d, &grade2);

printf("Average = %d", (grade1+grade2/2); )

```

### Organiser à l'intérieur des methodes 
```c
// Définition de la fonction
int addition(int a, int b) {
    int somme;      // 1. Déclaration des variables
    somme = a + b;  // 2. Assignation des variables
    return somme;   // 3. Retour de la valeur
}
```

# Data types
| Data Type                 | Size (bytes) | Range                                      | Format Specifier |
|---------------------------|-------------|--------------------------------------------|------------------|
| short int                 | 2           | -32,768 to 32,767                         | %hd              |
| unsigned short int        | 2           | 0 to 65,535                               | %hu              |
| unsigned int              | 4           | 0 to 4,294,967,295                        | %u               |
| int                       | 4           | -2,147,483,648 to 2,147,483,647           | %d               |
| long int                  | 4           | -2,147,483,648 to 2,147,483,647           | %ld              |
| unsigned long int         | 4           | 0 to 4,294,967,295                        | %lu              |
| long long int             | 8           | -(2^63) to (2^63)-1                       | %lld             |
| unsigned long long int    | 8           | 0 to 18,446,744,073,709,551,615           | %llu             |
| signed char               | 1           | -128 to 127                               | %c               |
| unsigned char             | 1           | 0 to 255                                  | %c               |
| float                     | 4           | 1.2E-38 to 3.4E+38                        | %f               |
| double                    | 8           | 1.7E-308 to 1.7E+308                      | %lf              |
| long double               | 16          | 3.4E-4932 to 1.1E+4932                    | %Lf              |


## 1. short int
- Taille : 2 octets (16 bits)
- Plage de valeurs : -32,768 à 32,767
- Format Specifier : %hd
- Description :
        Un entier signé stocké sur 16 bits.
        Utilisé lorsque la plage de valeurs est limitée et que l'on souhaite économiser de la mémoire.
        Les valeurs négatives sont représentées en complément à deux.

## 2. unsigned short int
- Taille : 2 octets (16 bits)
- Plage de valeurs : 0 à 65,535
- Format Specifier : %hu
- Description :
        Version non signée de short int, ce qui signifie qu'il ne peut stocker que des valeurs positives.
        Permet d’étendre la plage de valeurs maximales disponibles en sacrifiant la possibilité de stocker des nombres négatifs.

## 3. unsigned int
- Taille : 4 octets (32 bits)
- Plage de valeurs : 0 à 4,294,967,295
- Format Specifier : %u
- Description :
        Entier non signé, stocké sur 32 bits.
        Permet de doubler la plage de valeurs positives disponibles par rapport à int.
        Utilisé lorsqu’on sait que la valeur ne sera jamais négative (exemple : tailles, nombres d’éléments, etc.).

## 4. int
- Taille : 4 octets (32 bits)
- Plage de valeurs : -2,147,483,648 à 2,147,483,647
- Format Specifier : %d
- Description :
    L’un des types de données les plus utilisés en C pour stocker des nombres entiers.
    Représenté en complément à deux pour gérer les valeurs négatives.
    La taille peut varier selon l’implémentation, mais en général, elle est de 4 octets.

### Pourquoi utiliser unsigned int et/ou int

### Signed vs Unsigned : Comment sont répartis les valeurs ?
Quand tu as un type signed (avec signe), une partie des bits est utilisée pour représenter le signe (+ ou -), alors que dans un unsigned (sans signe), tous les bits servent à stocker des valeurs positives.

| Type                        | Taille (bits) | Plage des valeurs                      |
|-----------------------------|--------------|----------------------------------------|
| `signed int` (4 octets)     | 32 bits      | -2 147 483 648 à 2 147 483 647        |
| `unsigned int` (4 octets)   | 32 bits      | 0 à 4 294 967 295                     |


📌 Observation : Un unsigned int permet d’aller deux fois plus loin en positif qu’un signed int, mais il ne permet pas d’avoir de nombres négatifs.

### Pourquoi ? Explication en binaire !

Prenons un exemple avec 4 bits pour simplifier :
1) Signed int (2 bits pour les valeurs + 1 bit pour le signe)

Avec 4 bits, on peut coder 16 valeurs (2⁴ = 16), mais en signed, on partage les valeurs entre positif et négatif :

| Binaire | Décimal (Signed)  |
|---------|------------------|
| 0000    | 0                |
| 0001    | 1                |
| 0010    | 2                |
| 0011    | 3                |
| 0100    | 4                |
| 0101    | 5                |
| 0110    | 6                |
| 0111    | 7                |
| 1000    | -8 (bit de signe activé) |
| 1001    | -7               |
| 1010    | -6               |
| 1011    | -5               |
| 1100    | -4               |
| 1101    | -3               |
| 1110    | -2               |
| 1111    | -1               |


Plage de valeurs possibles : -8 à +7

### 2) Unsigned int (tous les bits pour les valeurs)

En unsigned, on n'a pas de signe, donc tous les 16 nombres possibles sont positifs :

| Binaire | Décimal (Unsigned) |
|---------|--------------------|
| 0000    | 0                  |
| 0001    | 1                  |
| 0010    | 2                  |
| 0011    | 3                  |
| 0100    | 4                  |
| 0101    | 5                  |
| 0110    | 6                  |
| 0111    | 7                  |
| 1000    | 8                  |
| 1001    | 9                  |
| 1010    | 10                 |
| 1011    | 11                 |
| 1100    | 12                 |
| 1101    | 13                 |
| 1110    | 14                 |
| 1111    | 15                 |


## 5. long int
- Taille : 4 octets (32 bits) (souvent 8 octets sur certains systèmes 64 bits)
- Plage de valeurs : -2,147,483,648 à 2,147,483,647 (ou plus sur certains systèmes)
- Format Specifier : %ld
Description :
        Similaire à int, mais peut parfois offrir une plage de valeurs plus grande selon l’architecture du système.
        En général, sur les systèmes 64 bits, long int peut être stocké sur 8 octets, offrant une plage plus large.

## 6. unsigned long int

    Taille : 4 octets (32 bits) (ou 8 octets sur systèmes 64 bits)
    Plage de valeurs : 0 à 4,294,967,295 (ou plus sur certains systèmes)
    Format Specifier : %lu
    Description :
        Version non signée de long int, qui permet d’avoir une plus grande plage de valeurs positives.
        Utilisé dans les situations où seules des valeurs positives sont nécessaires, comme pour des indices ou des tailles.


## 7. long long int
- Taille : 8 octets (64 bits)
- Plage de valeurs : -(2^63) à (2^63)-1
- Format Specifier : %lld
Description :
        Utilisé pour stocker des nombres entiers encore plus grands que long int.
        Très utile pour des calculs nécessitant une très grande précision avec des nombres entiers.


## 8. unsigned long long int
- Taille : 8 octets (64 bits)
- Plage de valeurs : 0 à 18,446,744,073,709,551,615
- Format Specifier : %llu
- Description :
        Version non signée de long long int.
        Permet de représenter des nombres très grands sans négatif, ce qui est utile pour des calculs scientifiques ou des indices de très grandes bases de données.

## 9. signed char
- Taille : 1 octet (8 bits)
- Plage de valeurs : -128 à 127
- Format Specifier : %c (mais aussi %hhd pour afficher la valeur numérique)
- Description :
        Stocke un caractère ASCII (8 bits).
        Peut également être utilisé pour stocker de petits nombres entiers.

## 10. unsigned char
- Taille : 1 octet (8 bits)
- Plage de valeurs : 0 à 255
- Format Specifier : %c (ou %hhu pour la valeur numérique)
    Description :
        Similaire à signed char, mais ne peut pas stocker de valeurs négatives.
        Souvent utilisé pour représenter des couleurs en format RGB (chaque canal variant de 0 à 255).

## 11. float
- Taille : 4 octets (32 bits)
- Plage de valeurs : 1.2E-38 à 3.4E+38
- Format Specifier : %f
- Description :
        Type de donnée en virgule flottante utilisé pour stocker des nombres décimaux.
        Moins précis que double, mais prend moins de mémoire.
        Suivant la norme IEEE 754, il utilise :
            1 bit pour le signe,
            8 bits pour l’exposant,
            23 bits pour la mantisse.

## 12. double
- Taille : 8 octets (64 bits)
- Plage de valeurs : 1.7E-308 à 1.7E+308
- Format Specifier : %lf
- Description :
        Plus précis que float car il utilise plus de bits pour stocker les valeurs.
        Suit également la norme IEEE 754, avec :
            1 bit pour le signe,
            11 bits pour l’exposant,
            52 bits pour la mantisse.
        Utilisé dans des calculs nécessitant une plus grande précision.

## 13. long double
- Taille : 16 octets (128 bits) (selon l’architecture)
- Plage de valeurs : 3.4E-4932 à 1.1E+4932
- Format Specifier : %Lf
- Description :
        Encore plus précis que double.
        Sur certaines architectures, il occupe 16 octets et peut représenter des valeurs beaucoup plus grandes ou plus précises.
        Très utilisé dans les calculs scientifiques et en ingénierie pour minimiser les erreurs d’arrondi.


# Organisation des dossiers du projet

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


# Structure du projet

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

## Contenu des fichiers src
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

## Notes

### Lancement du script pour créer un projet C de base 

```
chmod +x create_project.sh
./create_project
```
