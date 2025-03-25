## Table des Matières
* [Octal, Binary, Hexadecimals & More](#octal-binary-hexadeciaml-&-more)
* [Variables](#variables)
	* [Reading input from user](#reading-input-from-user)
 	* [Casting](#casting)
* [Structure de données](#structure-de-donnees)
	* [Tableaux](#tableaux)
  	* [struct](#struct)
  	* [Listes Chaînées](#liste-chainees)
  	* [Piles & files](#piles-et-files)
  	* [Arbres & graphes](#arbres-et-graphes)
  	* [Tables de hashage](#tables-de-hashage)
  	* [Set](#set)
  	* [Tas](#tas)
* [Data Types](#data-types)
* [Organisation des dossiers](#organisation-des-dossiers-du-projet)
* [Structure du projet](#structure-du-projet)
* [Script](#script)
	
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


## Casting

Le casting (ou "conversion de type") en C est le processus de conversion d'une variable d'un type de donnée à un autre. Le casting est utile lorsque vous voulez forcer une valeur à être traitée comme un autre type, ce qui peut être nécessaire pour éviter des erreurs de type ou pour optimiser des calculs.

Il existe deux types de casting en C :
- Casting implicite (ou automatique) : Cela se fait automatiquement, selon les règles de promotion des types en C.
- Casting explicite : C'est lorsque le programmeur indique explicitement la conversion d'un type à un autre.

### 1. Casting implicite (automatique)

Le casting implicite se produit lorsque le compilateur convertit automatiquement une valeur d'un type à un autre type plus large ou plus adapté, comme dans les calculs entre des entiers et des nombres à virgule flottante.
Exemple de casting implicite :

```c
int main() {
    int x = 5;
    double y = 2.5;
    double result;

    // Implicit cast: int to double
    result = x + y;

    printf("Resultat: %.2f\n", result);  // 7.50
    return 0;
}
```

Ici, x est un entier, et y est un double. Le compilateur va automatiquement convertir x (int) en double avant de faire l'addition, car le type double peut contenir à la fois des entiers et des décimales.

### 2. Casting explicite (ou "cast")

Le casting explicite est utilisé lorsqu'on veut forcer une conversion de type qui ne serait pas réalisée automatiquement par le compilateur. Cela se fait à l'aide d'une opération de cast.
Syntaxe du casting explicite :
```c
(type) expression
```
- type : le type vers lequel vous voulez convertir l'expression.
- expression : la valeur ou la variable à convertir.

#### Exemple de casting explicite 
```c
int main() {
    double pi = 3.14159;
    int integer_pi;

    // Cast explicite : double to int
    integer_pi = (int) pi;

    printf("Valeur de pi (en int): %d\n", integer_pi);  // 3
    return 0;
}

```

Dans cet exemple, la valeur de pi (qui est un double) est convertie explicitement en int en utilisant (int) avant d'assigner la valeur à integer_pi. Cela supprime la partie décimale de pi.

### 3. Problèmes fréquents avec le casting

#### a. Troncature (Perte de données)

Lorsqu'on convertit un type plus grand (par exemple, un double ou long) en un type plus petit (int, char), il peut y avoir une perte de données. Par exemple, si un nombre avec des décimales est converti en un entier, la partie après la virgule sera perdue.
Exemple de troncature :
```C
#include <stdio.h>

int main() {
    double value = 123.456;
    int truncated_value;

    truncated_value = (int) value;  // Troncature, perte de la partie décimale

    printf("Valeur après troncature: %d\n", truncated_value);  // 123
    return 0;
}
```

#### b. Dépassement de capacité (Overflow)

Si vous convertissez un type plus grand vers un type plus petit et que la valeur dépasse la capacité du type de destination, cela peut entraîner un dépassement de capacité.
Exemple de dépassement :

```c
#include <stdio.h>

int main() {
    long large_number = 1000000;
    short small_number;

    // Cast explicite (long vers short) peut entraîner un dépassement
    small_number = (short) large_number;

    printf("Valeur après conversion: %d\n", small_number);  // Dépassement, peut afficher un nombre incorrect
    return 0;
}
```

Le type short a une plage de valeurs plus petite que long. Si large_number est trop grand pour tenir dans un short, il y aura un dépassement.

### 4. Types de cast courants en C
#### a. Cast entre entiers
Convertir un entier vers un autre entier ou vers un type à virgule flottante :

```c
int a = 5;
float b = (float) a;  // Conversion de int vers float
```

#### b. Cast entre entiers et flottants
Convertir un float ou un double en un int :
```c
float f = 10.75;
int i = (int) f;  // Conversion de float vers int (perte des décimales)
```

#### c. Cast entre types plus grands et plus petits
Lorsque vous travaillez avec des types de différentes tailles, vous pouvez être amené à les convertir, ce qui peut entraîner une perte de données.
```c
long l = 1234567890L;
int i = (int) l;  // Conversion de long vers int, peut entraîner un dépassement (OverFlow)
```

Le casting en C est un outil puissant mais doit être utilisé avec soin. Il est essentiel de comprendre les types de données et leurs plages de valeurs afin d'éviter des erreurs comme la perte de données ou le dépassement de capacité.
- Utilisez le casting implicite lorsque cela est possible, pour des conversions naturelles entre types compatibles.
- Utilisez le casting explicite avec précaution, surtout lorsqu'il s'agit de conversions entre types de tailles différentes ou lorsqu'une troncature ou une perte de données peut se produire.

# Data types

## Tableaux

Les tableaux sont l’une des structures de données les plus utilisées en langage C. Ils permettent de stocker plusieurs valeurs du même type sous un seul nom et d’y accéder via un indice.

### 1.Déclaration d'un tableau 
Un tableau (array) est une collection contiguë d’éléments en mémoire.
```c
type nom_tableau[taille];
int nombres[5]; // Tableau de 5 entiers
```
Ici, nombres peut stock 5 valeurs du type int.

### Initialisation d’un tableau
Il est possible d’initialiser un tableau au moment de sa déclaration :
```c
int nombres[5] = {10, 20, 30, 40, 50};

// Ou bien sans spécifier la taille, C le fera de lui même.
int nombres[] = {10, 20, 30, 40, 50}; // Tableau de taille 5

// Attention, si on initialise partiellement un tableau, les valeurs non spécifiées seront mises à 0.
int nombres[5] = {1, 2}; // nombres[2], nombres[3] et nombres[4] seront 0
```

### Accès aux éléments d'un tableau
Chaque élément du tableau est accessible grâce à son indice, qui commence toujours à 0 en C.
```c
#include <stdio.h>

int main() {
    int nombres[3] = {5, 10, 15};

    // Affichage des valeurs
    printf("Premier élément : %d\n", nombres[0]); // 5
    printf("Deuxième élément : %d\n", nombres[1]); // 10

    // Modification d’un élément
    nombres[2] = 20; // L'ancien 15 devient 20

    printf("Troisième élément après modification : %d\n", nombres[2]); // 20
    
    return 0;
}
```

### Parcourir un tableau avec une boucle
Il est courant d'utiliser une boucle for pour parcourir un tableau.

```c
#include <stdio.h>

int main() {
    int nombres[5] = {10, 20, 30, 40, 50};

    int taille_tableau = sizeof(nombres) / sizeof(nombres[0]);
    // sizeof(nombres) Taille totale du tableau en octets : 20
    // Taille d'un élément en octets : 4	

    for (int i = 0; i < taille_tableau; i++) {
        printf("Element %d : %d\n", i, nombres[i]);
    }

    return 0;
}
```

### Tableaux et mémoire
En mémoire, un tableau est stocké de manière contiguë. Chaque élément occupe un espace fixe en fonction de son type.
```c
#include <stdio.h>

int main() {
    int nombres[3] = {10, 20, 30};

    for (int i = 0; i < 3; i++) {
        printf("Adresse de nombres[%d] : %p\n", i, &nombres[i]);
    }

    return 0;
}
// 0x7ff7b42b425c
// 0x7ff7b42b4260
// 0x7ff7b42b4264
```
💡 On remarque que les adresses sont consécutives.

### Tableaux dynamiques avec malloc
En C, la taille des tableaux statiques (déclarés comme int tab[10]) ne peut pas être modifiée après compilation.
Si l'on veut un tableau dynamique, on utilise malloc().

📌 Exemple : Allocation dynamique d’un tableau de 5 entiers
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *tableaux = malloc(5 * sizeof(int)); // Allocation dynamique

    if (tableaux == NULL) { // Vérification de l'allocation mémoire
        printf("Échec de l'allocation mémoire\n");
        return 1; // Quitter avec une erreur
    }

    for (int i = 0; i < 5; i++) {
        tableaux[i] = (i + 1) * 2;
        printf("%d ", tableaux[i]);
    }

    printf("\n");

    free(tableaux); // Libérer la mémoire allouée

    return 0;
}
```
- Ici, tableau est un pointeur (int *tableau), mais la mémoire allouée par malloc() correspond à un tableau dynamique de 5 entiers (puisque tu alloues 5 * sizeof(int) octets).
- Même si tu n'utilises pas les crochets [], tu alloues de la mémoire pour plusieurs entiers. Tu traites donc ce pointeur comme un tableau dynamique (tableau qui peut être redimensionné, contrairement aux tableaux statiques).
- La mémoire est allouée de manière contiguë, comme un tableau, et tu peux y accéder via des indices, un peu comme un tableau classique.
- Exemple d'accès à un élément : tableau[0], tableau[1], etc. Ce sont des accès à la mémoire allouée dynamiquement via malloc().
  
```c
free(tableaux)
// Car malloc() réserve une zone mémoire hors de la pile, il faut donc libérer cette mémoire pour éviter les fuites.
```

#### Pourquoi malloc réserve une zone mémoire hors de la pile et pourquoi faut-il libérer la mémoire ? 
En C, la mémoire d'un programme est divisée en plusieurs segments :

#### 1. La pile (Stack)
- Utilisée pour stocker les variables locales et les appels de fonctions.
- Elle fonctionne comme une "pile" (dernier entré, premier sorti - LIFO).
- La mémoire est automatiquement libérée lorsqu'une fonction se termine.

```c
void fonction() {
    int x = 10; // Stocké dans la pile
} // "x" est automatiquement supprimé à la fin de la fonction
```

#### 2. Le tas (heap)
- Utilisé pour l’allocation dynamique de mémoire (malloc, calloc, realloc).
- La mémoire allouée ici n'est pas libérée automatiquement, le programmeur doit le faire avec free().
- Permet de gérer des structures de données de taille inconnue à la compilation.

```c
int *ptr = malloc(sizeof(int)); // Réservé dans le tas
*ptr = 42; // Utilisation de la mémoire
free(ptr); // Libération explicite nécessaire !
```

#### Pourquoi malloc() n'utilise pas la pile ?
- Les variables sur la pile sont limitées en taille et en durée de vie
- La pile est restreinte en mémoire (quelques Mo). Si tu essaies d'y stocker un gros tableau, tu risques un dépassement de pile (stack overflow).
- Tout ce qui est alloué dans la pile disparaît une fois la fonction terminée.
- Le tas permet de gérer des structures dynamiques
- Un programme peut allouer et libérer de la mémoire selon ses besoins, contrairement à la pile où tout doit être préalablement défini.

#### Pourquoi faut-il libérer la mémoire allouée par malloc() ?
- Éviter les fuites de mémoire : Si tu alloues de la mémoire mais que tu ne la libères pas, elle reste inutilisée jusqu'à la fin du programme, ce qui peut provoquer une consommation excessive de mémoire.
- Améliorer la gestion mémoire : Un programme bien écrit libère la mémoire inutilisée pour la rendre disponible à d'autres parties du programme.
- Empêcher des crashs ou ralentissements : Trop de mémoire non libérée peut ralentir un programme ou le faire planter sur des systèmes avec peu de mémoire.

Exemple de fuite mémoire :
```c
void fuite() {
    int *p = malloc(10 * sizeof(int)); // Alloue un tableau de 10 entiers
    p[0] = 42; // Utilisation de la mémoire

    // Pas de free(p) -> Fuite mémoire !    
}

```



### Tableau a plusieurs dimensions
En C, il est possible de créer des tableaux multidimensionnels.

#### Tableaux à 2 dimensions (matrices)

Un tableau à 2 dimensions est un tableau de tableaux.

📌 Exemple : Déclaration et affichage d’une matrice 2x3
```c
// TODO : A creuser car pas compréhensible 
#include <stdio.h>

int main() {
    int matrice[2][3] = { {1, 2, 3}, {4, 5, 6} };

    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 3; j++) {
            printf("%d ", matrice[i][j]);
        }
        printf("\n");
    }

    return 0;
}

```
Représentation :
```c
1  2  3
4  5  6
// Chaque ligne est un tableau de 3 éléments.
```

### Passage d’un tableau en paramètre à une fonction
En C, les tableaux sont toujours passés par adresse aux fonctions. 
Donc l'utilisation de sizeof(tab) ne donnera pas la taille du tableau 

📌 Exemple : Fonction qui affiche un tableau
```c
#include <stdio.h>

void afficherTableau(int tab[], int taille) {
    for (int i = 0; i < taille; i++) {
        printf("%d ", tab[i]);
    }
    printf("\n");
}

int main() {
    int valeurs[5] = {10, 20, 30, 40, 50};
    afficherTableau(valeurs, 5);
    return 0;
}
```

#### 💡 Pourquoi ne pas utiliser sizeof(tab) dans la fonction ?
Car un tableau est converti en pointeur lorsqu’il est passé à une fonction, donc sizeof(tab) ne donnera pas la taille du tableau.

#### Exercice 
Écris un programme qui :
- Demande à l'utilisateur combien de nombres il veut stocker.
- Alloue dynamiquement un tableau de cette taille.
- Remplit ce tableau avec des valeurs entrées par l’utilisateur.
- Affiche les valeurs.
- Libère la mémoire.


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

## Script

### Lancement du script pour créer un projet C de base 
Ajout à faire : 
- Récupérer le nom du dossier créer est l'utiliser pour créer un fichier.c et .h, importer le .h dans main.c et nom_du_dossier.c
- Faire la meme chose pour les tests.
- Vérifier pour la compilation car probleme a chqaue fois.
```
chmod +x create_project.sh
./create_project.sh
```
