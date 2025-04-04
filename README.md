## Table des Matières
* [Octal, Binary, Hexadecimals & More](#octal-binary-hexadeciaml-&-more)
* [C Strucuture d'un programme](#c-structure-programme)
* [Strings](#strings)
* [Buffer](#buffer)
* [Variables](#variables)
	* [Reading input from user](#reading-input-from-user)
 	* [Casting](#casting)
* [Control flow] (#control-flow) 
* [Structure de données](#structure-de-donnees)
	* [Tableaux](#tableaux)
  	* [struct](#struct)
  	* [Listes Chaînées](#liste-chainees)
  	* [Piles & files](#piles-et-files)
  	* [Arbres & graphes](#arbres-et-graphes)
  	* [Tables de hashage](#tables-de-hashage)
  	* [Set](#set)
  	* [Tas](#tas)
* [Pointeurs](#pointeurs)
  * [Introduction to pointers]()
  * [Working with pointers]()
  * [Pointer types, pointer arithmetic, void pointers]()
  * [Pointers to pointers in C]()
  * [Pointer as function arguments]()
  * [Pointers and arrays]()
  * [Array as function arguments]()
  * [Character arrays and pointers]()
  * [Pointers and 2-D arrays]()
  * [Pointers and multidimensional arrays]()
  * [Pointers and dynamic memory - Stack vs Heap]()
  * [Dynamic memory allocation in C - malloc, calloc, realloc, free]()
  * [Pointers as function returns in C]()
  * [Function pointers in C]()
  * [Function pointers and callbacks]()
  * [Memory leak in C]()
 
* [Gestion de la mémoire](#gestion-de-la-memoire)
* [Data Types](#data-types)
* [Organisation des dossiers](#organisation-des-dossiers-du-projet)
* [Structure du projet](#structure-du-projet)
* [Script](#script)
	
# Octal Binary Hexadeciaml & more

## 🚀 Projets : Coder en C, la calculatrice Apple version programmeur : 
1. Comprendre comment elle est implémenter ansi que toutes les fonctions : ASCII, Unicode, Binaire, 8(bytes) - 10(Decimal) - 16(hexadecimal)
2. Operateur => XOR, AND, OR, NOR, NOT, <<, >>, NEG, x << Y, x >>Y, mod, rol, RoR, flip8, flip16, (, ).

### XOR (^) : Effectue un OU exclusif bit à bit. Résulte en 1 si les bits sont différents.
- Ex : 5 ^ 3 (101 ^ 011 → 110, soit 6).

### AND (&) : Effectue un ET bit à bit. Résulte en 1 si les deux bits sont 1.
- Ex : 5 & 3 (101 & 011 → 001, soit 1).

### OR (|) : Effectue un OU bit à bit. Résulte en 1 si au moins un des bits est 1.
- Ex : 5 | 3 (101 | 011 → 111, soit 7).

### NOR : Pas d'opérateur direct en C, mais c'est ~(A | B). Résulte en 1 seulement si les deux bits sont 0.
- Ex : 5 NOR 3 (~(101 | 011) → ~111 → 000, soit 0).

### NOT (~) : Inverse tous les bits d'un nombre (complément à 1)
- Ex : ~5 (~00000101 → 11111010 en 8 bits, soit -6 en complément à 2).

### << (décalage gauche) : Décale les bits vers la gauche, multipliant par 2^n.
- Ex : 5 << 1 (00000101 << 1 → 00001010, soit 10).

### >> (décalage droite) : Décale les bits vers la droite, divisant par 2^n.
- Ex : 5 >> 1 (00000101 >> 1 → 00000010, soit 2).

### NEG : Négation en complément à 2 (-x = ~x + 1).
- Ex : NEG 5 (~5 + 1 → -5).

### x << Y : Décale x de Y bits vers la gauche (x * 2^Y).

### x >> Y : Décale x de Y bits vers la droite (x / 2^Y).

### mod (%) : Reste de la division entière.
- Ex : 5 % 3 → 2.

### rol (rotate left) : Rotation circulaire des bits vers la gauche.
- Ex : ROL(10011010, 2) → 01101010.

### ror (rotate right) : Rotation circulaire des bits vers la droite.
- Ex : ROR(10011010, 2) → 10100110.

### flip8 : Inverse les bits d’un octet (8 bits).
- Ex : flip8(10110011) → 11001101.

### flip16 : Inverse les bits d’un mot de 16 bits.

### ( et ) : Parenthèses pour regrouper des expressions et prioriser les opérations.

## Bitwise Magic
### 💡 Les opérateurs bitwise en C
En C, les opérateurs bitwise permettent d’effectuer des opérations directement sur les bits d’un nombre.
Ils sont souvent utilisés pour :
- Optimiser la mémoire (stockage compact de données)
- Manipuler les flags et les permissions
- Accélérer certains calculs en remplaçant des multiplications/divisions
- Interagir avec du matériel bas niveau (ports, registres, etc.)

### 1️⃣ Opérateur AND &
📌 Fonctionnement :
Effectue une conjonction bit à bit (1 si les deux bits sont 1, sinon 0).
Exemple : Filtrer des bits spécifiques
```c
int a = 0b1101;  // 13 en décimal
int b = 0b1011;  // 11 en décimal
//      0b1001  
int result = a & b;

printf("%d\n", result);  // ➝ 9 (0b1001)
```
A quoi bin faire cela ? 

### 2️⃣ Opérateur OR |
📌 Fonctionnement :
Effectue une disjonction bit à bit (1 si au moins un des bits est 1).
Exemple : Activer un bit
```c
int a = 0b1101;  // 13
int b = 0b1011;  // 11
int result = a | b;
printf("%d\n", result);  // ➝ 15 (0b1111)
```
💡 Cas d’usage :
✅ Activer un bit sans toucher aux autres → x |= (1 << n);
✅ Combiner des permissions / flags
🔹 Lien avec les exercices : Utilisé pour activer un bit (Exercice 7).

### 3️⃣ Opérateur XOR ^
📌 Fonctionnement :
Effectue un OU exclusif : 1 si les bits sont différents, 0 s’ils sont identiques.
Exemple : Inverser un bit sans affecter les autres
```c
int a = 0b1101;  // 13
int b = 0b1011;  // 11
int result = a ^ b;
printf("%d\n", result);  // ➝ 6 (0b0110)
```
💡 Cas d’usage :
✅ Inverser un bit : x ^= (1 << n);
✅ Trouver l’unique élément d’un tableau (a ^ a = 0, voir Exercice 8)
✅ Détecter des changements d’état

### 4️⃣ Opérateur NOT ~
📌 Fonctionnement :
Inverse tous les bits (complément à un).
Exemple : Inverser tous les bits d’un entier
```c
int a = 0b1101;  // 13
int result = ~a;
printf("%d\n", result);  // ➝ -14 (complément à deux)
```
💡 Cas d’usage :
✅ Créer des masques inversés → x & ~mask
✅ Complément à deux pour représenter un nombre négatif

###5️⃣ Décalages de bits << et >>

Ces opérateurs permettent de décaler les bits vers la gauche ou la droite, ce qui revient à multiplier ou diviser par une puissance de 2.

#### Opérateur de décalage gauche <<
Multiplie par 2^n en décalant les bits à gauche.
```c
int a = 5;  // 0b0101
int result = a << 2;  // Décalage de 2 bits vers la gauche
printf("%d\n", result);  // ➝ 20 (0b10100)
```
💡 Cas d’usage :
✅ Multiplie rapidement par une puissance de 2
✅ Encodage compact de données (ex: stockage de couleurs en mémoire)


####Opérateur de décalage droite >>
Divise par 2^n en décalant les bits à droite.
```c
int a = 20;  // 0b10100
int result = a >> 2;
printf("%d\n", result);  // ➝ 5 (0b0101)
```
💡 Attention : Pour les nombres négatifs, un décalage logique >> peut propager le bit de signe (1 reste 1, dépend de l’implémentation).


### Exercices :
1️⃣ Affichage d’un entier en binaire (Niveau Facile)
📌 Objectif : Écrire une fonction print_binary(int n) qui affiche un nombre entier en binaire sur 32 bits.
✅ Contraintes :
- Afficher un espace tous les 4 bits pour la lisibilité.
- Accepter les nombres négatifs (utiliser le complément à deux).
```c
print_binary(42);  // ➝ 0000 0000 0000 0000 0000 0000 0010 1010
print_binary(-5);  // ➝ 1111 1111 1111 1111 1111 1111 1111 1011
```

2️⃣ Conversion entre bases (Niveau Facile)
📌 Objectif : Écrire un programme qui convertit un nombre en binaire, octal et hexadécimal.
✅ Exemple :
```c
Entrée : 42
Sortie :
Binaire :  0b101010
Octal :    052
Hexa :     0x2A
```
💡 Indication : Utiliser %o, %x et la fonction print_binary().

3️⃣ Vérifier si un nombre est une puissance de 2 (Niveau Intermédiaire)
📌 Objectif : Écrire une fonction qui retourne 1 si un nombre est une puissance de 2, sinon 0.
✅ Propriétés :
- Une puissance de 2 a un seul bit à 1 (2, 4, 8, 16...).
- Utiliser x & (x - 1) == 0 pour la vérification.
```c
is_power_of_two(8);  // ➝ 1 (true)
is_power_of_two(10); // ➝ 0 (false)
```

4️⃣ Compter le nombre de bits à 1 (Niveau Intermédiaire)
📌 Objectif : Implémenter count_bits(int n) qui retourne le nombre de bits activés à 1 dans un entier.
💡 Astuce : Utiliser n & (n - 1) pour éliminer le dernier bit à 1 à chaque itération.

🔹 Exemple :
```c
count_bits(42);  // ➝ 3   (101010)
count_bits(15);  // ➝ 4   (1111)
```

5️⃣ Inverser les bits d'un entier (Niveau Intermédiaire)
📌 Objectif : Écrire une fonction reverse_bits(int n) qui inverse les bits d'un nombre.
🔹 Exemple :
```c
Entrée : 0b00000000000000000000000000001010 (10)
Sortie  : 0b01010000000000000000000000000000 (inverse)
```

6️⃣ Extraire un bit spécifique d’un entier (Niveau Intermédiaire)
📌 Objectif : Écrire une fonction get_bit(int n, int pos) qui retourne la valeur du bit (0 ou 1) à la position donnée (de droite à gauche).
🔹 Exemple :
```c
get_bit(42, 1);  // ➝ 1 (42 = 101010, bit à la position 1 = 1)
get_bit(42, 3);  // ➝ 0 (42 = 101010, bit à la position 3 = 0)
```

7️⃣ Activer et désactiver un bit (Niveau Intermédiaire)
📌 Objectif : Implémenter deux fonctions :
- set_bit(int n, int pos) → Active le bit à pos
- clear_bit(int n, int pos) → Désactive le bit à pos

🔹 Exemple :
```c
set_bit(42, 1);   // ➝ 0b101010 (42) -> Aucun changement
set_bit(42, 2);   // ➝ 0b101110 (46)
clear_bit(42, 1); // ➝ 0b101000 (40)
```

8️⃣ Trouver l’entier unique dans un tableau (Niveau Avancé)
📌 Objectif : Dans un tableau où chaque nombre apparaît deux fois sauf un seul, trouver l’unique sans utiliser de tableau supplémentaire.
💡 Astuce : Utiliser XOR (^) car a ^ a = 0.
🔹 Exemple :
```c
int arr[] = {1, 3, 5, 3, 1};
find_unique(arr, 5);  // ➝ 5
```

9️⃣ Vérifier si deux entiers ont des bits opposés (Niveau Avancé)
📌 Objectif : Implémenter une fonction has_opposite_signs(int x, int y) qui retourne 1 si x et y ont des signes opposés, sinon 0.
💡 Astuce : En complément à deux, les nombres négatifs ont le MSB à 1.
Solution rapide : x ^ y → Si le bit de signe change (x ^ y < 0), les signes sont opposés.
🔹 Exemple :
```c
has_opposite_signs(5, -10);  // ➝ 1 (true)
has_opposite_signs(-3, -8);  // ➝ 0 (false)
```

🔟 Convertir une adresse IP en entier 32 bits (Niveau Avancé)
📌 Objectif : Écrire une fonction ip_to_int(const char *ip) qui convertit une IP en un entier 32 bits.
🔹 Exemple :
```c
ip_to_int("192.168.1.1");  // ➝ 3232235777
```
💡 Indice :
- 192.168.1.1 = (192 << 24) | (168 << 16) | (1 << 8) | 1
- Utiliser sscanf(ip, "%d.%d.%d.%d", &a, &b, &c, &d)  

#### 🚀 Challenge Bonus : Implémenter un mini BitMap
📌 Objectif : Implémenter un BitMap permettant d’allouer un tableau compact pour stocker des bits.
✅ Fonctions :
- void set_bit(uint8_t *bitmap, int pos);
- void clear_bit(uint8_t *bitmap, int pos);
- int get_bit(uint8_t *bitmap, int pos);


# C structure programme 

Le plus simple programme en C est : 
```c
int main() {
    return 0;
}
```

- Une fonction nommée `main` est toujours le point d'entrée d'un programme en C (contrairement à Python, qui commence au début du fichier).
- `int` est le type de retour de la fonction et signifie "entier". Comme c'est la fonction principale, la valeur de retour est le code de sortie du programme. 0 signifie succès, tout autre chiffre signifie échec.
    - Vous trouverez beaucoup d'abréviations en C car 1) les programmeurs sont paresseux, et 2) cela comptait autrefois combien de bytes votre code source faisait.
- Le crochet ouvrant `{` marque le début du corps de la fonction (C ignore les espaces blancs, donc l'indentation est juste pour le style, pas pour la syntaxe).
- `return 0` renvoie la valeur 0 (un entier) de la fonction. Encore une fois, c'est le code de sortie car c'est la fonction principale.
    - 0 représente "rien de mal ne s'est produit" comme valeur de retour.
- Le vilain `;` à la fin de `return 0;` est nécessaire en C pour terminer les instructions.
- Le crochet fermant `}` marque la fin du corps de la fonction.

### Printf

- Cela semble très différent si vous venez de Python, mais l'affichage en C se fait avec une fonction appelée `printf` provenant de la bibliothèque `stdio.h` (entrée/sortie standard) avec de nombreuses règles de formatage étranges.
- Pour l'utiliser, vous devez inclure `#include` en haut de votre fichier.
```c
#include <stdio.h>
printf("Hello, world!\n");
```

- `\n` : il est nécessaire d'imprimer un caractère de nouvelle ligne (et de vider le tampon dans le navigateur), ce que fait automatiquement `print()` en Python.
- Si vous vous demandez, le `f` dans `printf` signifie "print formatted" (impression formatée).


# Strings
En C, les chaînes de caractères sont représentées par des tableaux de caractères terminés par un caractère spécial \0, appelé le caractère nul. C’est ainsi que C identifie la fin de la chaîne.
En C, une chaîne de caractères est en fait un tableau de caractères (de type char[]). Voici quelques exemples de déclarations :
```c
char str1[10];       // Déclare un tableau de 10 caractères (inclus le caractère nul '\0')
char str2[] = "Hello"; // Le compilateur détermine automatiquement la taille (ici, 6 caractères : 'H', 'e', 'l', 'l', 'o', '\0')
```

## 2. Initialisation d’une chaîne de caractères
- Utiliser une chaîne littérale : Les chaînes de caractères en C sont souvent initialisées à l’aide de chaînes littérales, comme montré dans l'exemple précédent. Cela permet de directement attribuer une chaîne à un tableau de char.

```c
char str[] = "Hello, World!";
```

- Avec une taille spécifique : Vous pouvez également déclarer un tableau de caractères avec une taille fixe. Par exemple, si vous savez que votre chaîne ne dépassera pas 10 caractères, vous pouvez faire :
```c
char str[10] = "Hello"; // La chaîne "Hello" et le caractère nul '\0' sont stockés
str[0] = 'H'
str[1] = 'e'
str[2] = 'l'
str[3] = 'l'
str[4] = 'o'
str[5] = '\0' // Caractère nul qui termine la chaîne
str[6 ..9] seront des valeurs aléatoires car on a déclaré un tableau de char de 10 éléments, représentant une string.
```

## 3. Manipulation des chaînes de caractères
### a. Accéder aux caractères individuels

Comme toute autre variable de type tableau en C, chaque caractère dans une chaîne peut être accédé par son index :
```c
char str[] = "Hello";
printf("%c\n", str[0]); // Affiche 'H'
printf("%c\n", str[1]); // Affiche 'e'
```

### b. Modifier une chaîne de caractères
Les chaînes en C peuvent être modifiées, mais seulement si elles ont été déclarées comme tableau de caractères (et non comme const ou pointeur vers une chaîne littérale).
```c
char str[] = "Hello";
str[0] = 'J'; // Modifie le premier caractère en 'J'
printf("%s\n", str); // Affiche "Jello"
```

### c. Affichage d’une chaîne de caractères
Pour afficher une chaîne de caractères en C, vous utilisez la fonction printf() avec le spécificateur %s.
```c
char str[] = "Hello, World!";
printf("%s\n", str); // Affiche "Hello, World!"
```

### d. Taille d’une chaîne de caractères
La fonction strlen() de la bibliothèque <string.h> retourne la longueur d’une chaîne de caractères, sans compter le caractère nul \0.
```c
#include <string.h>

char str[] = "Hello";
printf("La longueur de la chaîne est : %lu\n", strlen(str)); // Affiche 5
```

## 5. Fonctions de manipulation des chaînes de caractères

Voici quelques fonctions très utiles de la bibliothèque <string.h> pour manipuler les chaînes :
- strcpy(destination, source) : Copie la chaîne source dans la chaîne destination.
```c
char src[] = "Hello";
char dest[10];
strcpy(dest, src); // Copie "Hello" dans dest
printf("%s\n", dest); // Affiche "Hello"
```

- strcat(destination, source) : Concatène (ajoute) la chaîne source à la fin de la chaîne destination.
```c
char str1[20] = "Hello";
char str2[] = " World!";
strcat(str1, str2); // Concatène " World!" à "Hello"
printf("%s\n", str1); // Affiche "Hello World!"
```

- strcmp(str1, str2) : Compare deux chaînes de caractères. Retourne 0 si elles sont égales, un nombre négatif si str1 est inférieure à str2, et un nombre positif si str1 est supérieure à str2.
```c
char str1[] = "Hello";
char str2[] = "Hello";
int result = strcmp(str1, str2); // Retourne 0 (elles sont égales)
```

- strchr(str, character) : Trouve la première occurrence d’un caractère dans une chaîne de caractères. Retourne un pointeur vers ce caractère ou NULL si le caractère n’est pas trouvé.
```c
char str[] = "Hello";
char *ptr = strchr(str, 'e');
if (ptr) {
    printf("Trouvé : %c\n", *ptr); // Affiche 'e'
}
```

##  et chaînes de caractères
Les  et les chaînes de caractères sont des concepts clés en langage C, et leur interaction est essentielle pour bien comprendre la gestion des chaînes de caractères dans ce langage. Les  en C permettent de manipuler directement les adresses mémoire, ce qui les rend particulièrement utiles lorsqu'il s'agit de travailler avec des chaînes de caractères, car une chaîne est en réalité un tableau de caractères et peut être manipulée via un pointeur.

### 1. Les chaînes de caractères en C
En C, une chaîne de caractères est un tableau de caractères qui se termine toujours par un caractère nul ('\0'), ce qui permet au programme de savoir où la chaîne se termine. Par exemple, la chaîne "Hello" est en fait un tableau de caractères contenant cinq lettres, suivies d'un caractère nul, soit :
```c
'H' 'e' 'l' 'l' 'o' '\0'
```
Cela signifie qu'une chaîne de caractères en C est toujours un tableau de caractères, et c'est ce tableau que nous manipulons lorsqu'on travaille avec des chaînes.

### 2.  vers des chaînes de caractères

Un pointeur vers une chaîne de caractères est simplement un pointeur qui pointe vers le premier caractère d'une chaîne. En d'autres termes, au lieu de stocker la chaîne entière dans une variable, nous stockons une référence à la première case mémoire où la chaîne commence.
Exemple de déclaration d'un pointeur vers une chaîne de caractères :
```c
#include <stdio.h>

int main() {
    char *str = "Hello";  // Pointeur vers une chaîne littérale

    printf("%s\n", str);  // Affiche "Hello"

    return 0;
}
```
- char *str = "Hello"; : Ici, str est un pointeur qui pointe vers le premier caractère de la chaîne littérale "Hello". En C, les chaînes littérales sont en fait des tableaux de caractères constants, et le pointeur str pointe vers la première adresse de mémoire de ce tableau.
- printf("%s\n", str); : Lorsque nous passons le pointeur str à printf, la fonction affiche la chaîne à l'adresse pointée par str.

Fonctionnement interne :
"Hello" est une chaîne littérale stockée dans une zone mémoire en lecture seule. Le pointeur str pointe donc vers le début de cette zone mémoire. Cela signifie que str contient l'adresse de la première case mémoire où 'H' est stocké, et printf sait comment afficher la chaîne en suivant la séquence de caractères jusqu'à ce qu'il rencontre le caractère nul '\0'.

### 3. Modifications avec les 

Le fait qu'un pointeur pointe vers une chaîne de caractères permet de manipuler la chaîne de différentes manières, mais il est important de noter que cela dépend de la façon dont la chaîne a été déclarée.

Exemple : Modification d'un tableau de caractères
Si tu as une chaîne déclarée comme un tableau de caractères, tu peux modifier directement ses caractères, car la chaîne elle-même est mutable.
```c
#include <stdio.h>

int main() {
    char str[] = "Hello";  // Tableau de caractères

    printf("Avant modification : %s\n", str); // Affiche "Hello"
    
    str[0] = 'h';  // Modification du premier caractère
    printf("Après modification : %s\n", str);  // Affiche "hello"

    return 0;
}
```

- char str[] = "Hello"; : Ici, str est un tableau de caractères, ce qui signifie que tu peux directement modifier le contenu des caractères.
- str[0] = 'h'; : Modifie le premier caractère du tableau, ce qui change "Hello" en "hello".

### Exemple : Pointeur vers une chaîne littérale
Si tu utilises un pointeur vers une chaîne littérale, tu ne peux pas modifier la chaîne, car les chaînes littérales sont stockées en mémoire en lecture seule.
```c
#include <stdio.h>

int main() {
    char *str = "Hello";  // Pointeur vers une chaîne littérale

    printf("Avant modification : %s\n", str);
    
    // str[0] = 'h';  // Impossible de modifier une chaîne littérale, cela entraînera un comportement indéfini

    printf("Après modification : %s\n", str);  // Affiche toujours "Hello"

    return 0;
}
```
str[0] = 'h'; : Si tu essaies de modifier une chaîne littérale, comme ici, cela entraînera un comportement indéfini (souvent un segmentation fault)..

Cela signifie que la mémoire où la chaîne de caractères est stockée ne peut pas être modifiée une fois que la chaîne est définie. Examinons de plus près comment cela fonctionne et pourquoi c'est important.

### Pourquoi en lecture seule ?
En C, les chaînes littérales sont placées dans une zone de mémoire qui est en lecture seule.
Cette zone est utilisée pour optimiser la gestion des chaînes, car une chaîne littérale, une fois définie, n'a généralement pas besoin d'être modifiée. Elle est donc stockée dans une section mémoire protégée pour éviter toute modification accidentelle. Cela permet également de partager la même instance de la chaîne dans le programme, économisant ainsi de la mémoire.
- Caractéristique clé : La chaîne "Hello" est immuable, c'est-à-dire qu'elle ne peut pas être modifiée pendant l'exécution du programme.
- Stockage en mémoire : Les chaînes littérales sont souvent stockées dans une zone spéciale, comme .rodata (read-only data), qui est une section protégée en mémoire, en lecture seule. Cela empêche l'utilisateur de modifier la chaîne.

### Fonctionnement interne : Où est stockée la chaîne ?
Lorsque tu écris :
```c
char *str = "Hello";
```
Voici ce qui se passe en coulisses :
- Le compilateur crée la chaîne littérale "Hello" dans une zone en lecture seule de la mémoire.
- Il place cette chaîne dans la mémoire et associe un pointeur str à l'adresse de la première case mémoire de la chaîne, c'est-à-dire à l'adresse où le caractère 'H' est stocké.
- Si on considère que l'adresse mémoire où "Hello" commence est 0x1000, alors str contiendra l'adresse 0x1000, qui est l'emplacement de 'H'.
- Le caractère 'H' est suivi par 'e', 'l', 'l', 'o' et se termine par le caractère nul '\0', qui marque la fin de la chaîne en C. La mémoire est donc organisée ainsi (en supposant que les adresses commencent à 0x1000) :
```c
Adresse       Valeur
0x1000         'H'
0x1001         'e'
0x1002         'l'
0x1003         'l'
0x1004         'o'
0x1005         '\0'
```
- Lorsque tu appelles printf("%s", str);, printf utilise le pointeur str pour accéder à la première case mémoire de la chaîne et continue à afficher chaque caractère jusqu'à ce qu'il rencontre le caractère nul '\0' qui marque la fin de la chaîne.

### Pourquoi est-ce important que la chaîne soit en lecture seule ?
Sécurité mémoire : Si tu essaies de modifier une chaîne littérale en mémoire (par exemple, avec str[0] = 'J';), cela provoquera une erreur de segmentation (segfault), car les chaînes littérales sont stockées dans une zone mémoire en lecture seule.
```c
char *str = "Hello";
str[0] = 'J'; // Cela entraînera un segfault car la chaîne est en lecture seule.
```
- Optimisation : En plaçant les chaînes littérales dans une zone en lecture seule, le compilateur peut optimiser l'utilisation de la mémoire, car il peut partager des chaînes identiques entre différentes parties du programme sans avoir besoin de les dupliquer.
- Protection contre les erreurs : Empêcher la modification accidentelle des chaînes littérales améliore la robustesse du programme. Cela évite des bugs difficiles à repérer où une chaîne de caractères pourrait être modifiée par erreur.

### 5.  vers des chaînes littérales
Les chaînes de caractères peuvent être manipulées à l'aide de . Un pointeur vers une chaîne littérale est un pointeur constant qui pointe vers une zone mémoire en lecture seule. Par conséquent, tu peux modifier un pointeur pour qu'il pointe vers une autre chaîne, mais tu ne peux pas modifier le contenu de la chaîne elle-même.
```c
char *str = "Hello";  // Pointeur vers une chaîne littérale en mémoire
str = "World";        // Tu peux changer où pointe le pointeur, mais pas la chaîne originale

// Attention ce code entrainera une perte des données ainsi qu'une fuite mémoire
// avant ré assignation libérer la mémoire avec free() et réaffecter.
```

## 4. Manipulation de chaînes avec des 

Les  permettent de manipuler les chaînes de manière plus flexible, comme dans les exemples suivants :

### Accès aux caractères via des 

Un pointeur peut être utilisé pour parcourir chaque caractère de la chaîne et effectuer des opérations sur chaque caractère.
```c
#include <stdio.h>

int main() {
    char str[] = "Hello";
    char *ptr = str;  // Pointeur sur la première case du tableau

    // Utilisation du pointeur pour parcourir la chaîne
    while (*ptr != '\0') {
        printf("%c ", *ptr);  // Affiche chaque caractère
        ptr++;  // Déplace le pointeur vers le caractère suivant
    }

    printf("\n");

    return 0;
}
```
- char *ptr = str; : Ici, le pointeur ptr pointe vers le début du tableau str.
- *ptr : L'expression *ptr donne le caractère auquel ptr pointe.
- ptr++ : Cette ligne déplace le pointeur vers le caractère suivant dans la chaîne.
- Condition *ptr != '\0' : Le processus continue tant que le caractère pointé par ptr n'est pas le caractère nul '\0', ce qui marque la fin de la chaîne.

## 5. Passage de chaînes de caractères aux fonctions avec des 

Les chaînes de caractères sont souvent passées aux fonctions via des  pour économiser de la mémoire, car elles peuvent être grandes. Voici un exemple :

```c
#include <stdio.h>

void print_string(char *str) {
    printf("%s\n", str);  // Affiche la chaîne pointée par str
}

int main() {
    char str[] = "Hello, World!";
    print_string(str);  // Passer le tableau de caractères à la fonction

    return 0;
}
```
- char *str : Dans la fonction print_string, str est un pointeur vers une chaîne de caractères. Lorsque tu passes str à la fonction, le pointeur est copié, et la fonction peut accéder directement aux caractères de la chaîne.

## 6. Utilisation des  avec strlen et d'autres fonctions de la bibliothèque C

La bibliothèque standard C fournit de nombreuses fonctions utiles pour travailler avec des chaînes de caractères. Par exemple, strlen retourne la longueur d'une chaîne, et il fonctionne avec des .
```c
#include <stdio.h>
#include <string.h>  // Pour strlen

int main() {
    char str[] = "Hello, World!";
    
    printf("Longueur de la chaîne : %lu\n", strlen(str));  // Affiche 13
    
    return 0;
}
```
- strlen(str) : Cette fonction prend un pointeur vers une chaîne et retourne sa longueur (le nombre de caractères avant le caractère nul).

# Caractères et chaine de caractères en C
En C, la manipulation de texte est fondamentale, mais elle fonctionne différemment des langages plus modernes. Il est crucial de bien comprendre les bases.

## Partie 1 : Le Type char (Le Caractère Unique)

### Qu'est-ce qu'un char ?
- En C, le type char est le plus petit type de données entier. Il est conçu pour stocker un seul caractère.
- Techniquement, il stocke une valeur numérique (généralement sur 8 bits, soit 1 octet). Cette valeur numérique correspond à un caractère selon un jeu de caractères (le plus souvent ASCII ou un de ses dérivés comme UTF-8 pour les caractères plus modernes).
- Par exemple, la valeur 65 représente le caractère 'A', 97 représente 'a', 48 représente '0'.

### Déclaration et initialisation d'un char
- On déclare une variable de type char comme n'importe quelle autre variable.
- Pour assigner une valeur caractère littérale, on utilise des apostrophes simples (' ').

```c
#include <stdio.h> // Pour printf

int main() {
    char monCaractere;   // Déclaration d'une variable char
    monCaractere = 'B'; // Initialisation avec le caractère 'B'

    char autreCaractere = '$'; // Déclaration et initialisation en une ligne

    char chiffreCaractere = '7'; // IMPORTANT: '7' (caractère) est différent de 7 (entier)

    // Afficher les caractères avec le format %c
    printf("Mon caractère : %c\n", monCaractere);
    printf("Autre caractère : %c\n", autreCaractere);
    printf("Caractère chiffre : %c\n", chiffreCaractere);

    // On peut aussi voir leur valeur numérique (code ASCII) avec %d
    printf("Valeur ASCII de %c : %d\n", monCaractere, monCaractere); // Affichera 66 pour 'B'
    printf("Valeur ASCII de %c : %d\n", chiffreCaractere, chiffreCaractere); // Affichera 55 pour '7'

    return 0;
}
```

### Subtilité : char signé ou non signé (signed char / unsigned char)
 - Par défaut, le fait que char soit signed (peut contenir des valeurs négatives, typiquement -128 à 127) ou unsigned (0 à 255) dépend du compilateur.
 - Cela a rarement un impact quand on manipule des caractères ASCII standards (0-127), mais peut être important si on utilise des char pour stocker de petites valeurs numériques ou des caractères étendus. Pour la manipulation de texte standard, on utilise généralement char sans se soucier de ce détail au début.


## Partie 2 : Les Chaînes comme Tableaux (char nom_tableau[TAILLE];)
C'est la manière la plus fondamentale de représenter une chaîne de caractères en C.

### Definition
- Une chaîne de caractères en C n'est pas un type de données unique. C'est un tableau (array) de char.
- Subtilité CRUCIALE : Pour que C sache où se termine la chaîne dans le tableau, on utilise une convention : la chaîne doit se terminer par un caractère spécial appelé caractère nul ou terminateur nul. Ce caractère est représenté par \0 et a la valeur ASCII 0.
- Donc, un tableau pour stocker la chaîne "Salut" (5 caractères) doit en réalité avoir une taille d'au moins 6 char pour inclure le \0 final ('S', 'a', 'l', 'u', 't', '\0').

### Déclaration et initialisation
- Avec une taille fixe et initialisation via une chaîne littérale : Les chaînes littérales en C sont écrites entre guillemets doubles (" "). Le compilateur ajoute automatiquement le \0 final.
```c
#include <stdio.h>

int main() {
    // Déclare un tableau de char assez grand pour "Bonjour" + '\0'
    // Le compilateur calcule la taille automatiquement (7 + 1 = 8)
    char salutation[] = "Bonjour";

    // Déclare un tableau avec une taille explicite (doit être >= taille utile + 1)
    char nom[30] = "Alice"; // Ok, 30 est bien plus grand que 5 + 1

    // Afficher les chaînes avec le format %s
    printf("Salutation : %s\n", salutation);
    printf("Nom : %s\n", nom);

    // Accéder aux caractères individuels (comme un tableau normal)
    printf("Le premier caractère de salutation est : %c\n", salutation[0]); // 'B'
    printf("Le dernier caractère utile de nom est : %c\n", nom[4]);     // 'e'

    // Le caractère après 'e' est le caractère nul :
    printf("Le caractère après 'e' (valeur ASCII) : %d\n", nom[5]); // Affichera 0

    return 0;
}
```

- Avec une taille fixe et initialisation caractère par caractère : Moins courant, mais montre bien le \0. Il faut ajouter le \0 manuellement !
```c
#include <stdio.h>

int main() {
    char mot[4]; // Taille 4 pour 'O', 'u', 'i', '\0'
    mot[0] = 'O';
    mot[1] = 'u';
    mot[2] = 'i';
    mot[3] = '\0'; // TRÈS IMPORTANT ! Sans ça, ce n'est pas une chaîne C valide.

    printf("Mot : %s\n", mot); // Affichera "Oui"

    return 0;
}
```

### Le Caractère Nul (\0) en Détail
- Ce n'est PAS le caractère '0' (qui a la valeur ASCII 48). C'est un caractère de contrôle avec la valeur ASCII 0.
- Toutes les fonctions standards de manipulation de chaînes en C (printf avec %s, strlen, strcpy, etc.) reposent sur la présence de ce \0 pour savoir où s'arrêter.
- Oublier le \0 (si on construit la chaîne manuellement) est une source fréquente de bugs. La fonction lira la mémoire au-delà de la fin prévue de votre chaîne, menant à des comportements indéfinis (affichage de "déchets", plantage...).

### Accès et Modification des Caractères
- Comme ce sont des tableaux, on accède aux caractères via leur index (commençant à 0).
- On peut modifier les caractères d'une chaîne stockée dans un tableau (sauf si le tableau lui-même est const).

```c
#include <stdio.h>

int main() {
    char message[] = "Salut !"; // Taille 8 ('S','a','l','u','t',' ','!','\0')
    printf("Original : %s\n", message);

    message[0] = 'B'; // Change 'S' en 'B'
    message[5] = '-'; // Change ' ' en '-'
    // message[7] = '?'; // Attention, message[7] est le '\0'. Le changer "casse" la chaîne.
                       // Si on veut ajouter, il faut un tableau plus grand au départ.

    printf("Modifié : %s\n", message); // Affichera "Balut-!"

    return 0;
}
```

### Limites des Tableaux de Chaînes
- Taille Fixe : Une fois déclaré (char monTableau[50];), la taille du tableau est fixée à la compilation. On ne peut pas la changer pour y mettre une chaîne plus longue que 49 caractères (+ \0). C'est une limitation majeure. (La solution est l'allocation dynamique de mémoire avec malloc.

- Pas d'Affectation Directe : Après l'initialisation, on ne peut PAS faire ceci :
```c
char texte[20] = "Initial";
// texte = "Nouveau"; // ERREUR DE COMPILATION !
```
On ne peut pas assigner un tableau entier à un autre avec =. Il faut copier le contenu 
```c
char texte[20] = "Initial";
strcpy(texte, "Nouveau");
```

## Partie 3 : Les Chaînes comme Pointeurs (char *nom_pointeur;)
C'est l'autre façon très courante de manipuler des chaînes, offrant plus de flexibilité mais nécessitant plus d'attention.

### Définition
- Un char * est un pointeur, c'est-à-dire une variable qui contient l'adresse mémoire du premier caractère (char) de la chaîne.
- La chaîne elle-même (la séquence de char se terminant par \0) se trouve ailleurs en mémoire.
- Seul le pointeur est modifiable, pas le contenu : name[0] = 'B'; provoquerait une erreur à l'exécution

### Déclaration et initialisation
```c
#include <stdio.h>

int main() {
    // ptr pointe vers l'adresse du 'H' de la chaîne "Hello"
    // La chaîne "Hello" est stockée quelque part en mémoire (souvent en lecture seule).
    const char *ptr = "Hello";

    printf("Chaîne pointée : %s\n", ptr);
    printf("Adresse mémoire contenue dans ptr : %p\n", (void *)ptr);
    printf("Premier caractère via le pointeur : %c\n", *ptr); // Déréférencement : donne la valeur à l'adresse

    // On peut changer où pointe le pointeur
    ptr = "World"; // ptr contient maintenant l'adresse du 'W' de "World"
    printf("Nouvelle chaîne pointée : %s\n", ptr);

    return 0;
}
```

Subtilité TRÈS importante : 
- Quand un char * pointe vers une chaîne littérale ("comme ceci"), cette chaîne est souvent placée par le compilateur dans une zone mémoire en lecture seule.
- Essayer de la modifier via le pointeur provoque un comportement indéfini (souvent un plantage). C'est pourquoi on utilise souvent const char * pour indiquer cette intention.
```c
const char *message = "Immutable";
// message[0] = 'X'; // ERREUR ou PLANTAGE ! On ne modifie pas un littéral.
```

### Pointer vers un tableau de char existant :
```c
#include <stdio.h>

int main() {
    char monTableau[] = "Modifiable";
    char *pointeurVersTableau = monTableau; // Le pointeur contient l'adresse de monTableau[0]

    printf("Via pointeur: %s\n", pointeurVersTableau);

    // On PEUT modifier via le pointeur, car il pointe vers un tableau modifiable
    pointeurVersTableau[0] = 'm'; // Équivalent à monTableau[0] = 'm';
    printf("Tableau modifié via pointeur: %s\n", monTableau); // Affiche "modifiable"

    return 0;
}
```

### Différence Cruciale : char s[] = "texte"; vs const char *s = "texte";
- char s[] = "texte"; : Crée un tableau nommé s sur la pile (stack). Le contenu de "texte" (y compris \0) est copié dans ce tableau. s est modifiable. La taille est fixée par l'initialisation.
- const char *s = "texte"; : Crée un pointeur nommé s. La chaîne littérale "texte" est stockée ailleurs (zone de données statiques/lecture seule). s contient l'adresse de cette chaîne littérale. On ne doit pas essayer de modifier le contenu via s. On peut par contre faire pointer s vers une autre adresse.

### Utilisation des Pointeurs
- Les pointeurs sont très utilisés dans les fonctions qui manipulent des chaînes (comme celles de <string.h>).
- L'arithmétique des pointeurs permet de parcourir la chaîne : ptr++ fait pointer ptr vers le caractère suivant.

## Partie 4 : La Bibliothèque Standard <string.h> (Fonctions Utiles)
Le C fournit une bibliothèque standard (#include <string.h>) avec des fonctions essentielles pour manipuler ces tableaux/pointeurs de char terminés par \0.

### Obtenir la longueur : strlen(const char *s)
- Renvoie le nombre de caractères dans s avant le \0.
- strlen("Bonjour") renvoie 7.

### Copier des chaînes
- strcpy(char *destination, const char *source) : Copie source (y compris \0) dans destination. DANGEREUX ! Ne vérifie pas la taille de destination. À ÉVITER si possible.
- strncpy(char *destination, const char *source, size_t n) : Copie au plus n caractères de source vers destination. PLUS SÛR, mais attention, si source a n caractères ou plus, destination ne sera PAS terminée par \0 automatiquement. Il faut souvent l'ajouter manuellement.
```c
char dest[10];
strncpy(dest, "Trop long pour ici", 9); // Copie 9 caractères: "Trop long"
dest[9] = '\0'; // Ajout manuel indispensable!
```

- Alternative Sûre :  (de <stdio.h>) est souvent préféré pour copier de manière sûre :
```c
char destination[10];
const char *source = "Un exemple";
snprintf(destination, sizeof(destination), "%s", source);
// Garantit que destination est terminée par \0 et ne déborde pas.
// sizeof(destination) donne la taille totale du buffer (10).
```

### Concaténer des chaînes (ajouter à la fin)
- strcat(char *destination, const char *source) : Ajoute source à la fin de destination. Le premier caractère de source écrase le \0 de destination. DANGEREUX ! Ne vérifie pas si destination est assez grande pour contenir le résultat. À ÉVITER.
- strncat(char *destination, const char *source, size_t n) : Ajoute au plus n caractères de source à destination. Termine toujours par \0. PLUS SÛR. destination doit être assez grande pour strlen(destination) + n + 1.

### Comparer des chaînes
- strcmp(const char *s1, const char *s2) : Compare s1 et s2 lexicographiquement (ordre du dictionnaire).
- Renvoie 0 si s1 et s2 sont identiques.
- Renvoie une valeur < 0 si s1 vient avant s2.
- Renvoie une valeur > 0 si s1 vient après s2.
strncmp(const char *s1, const char *s2, size_t n) : Compare au plus les n premiers caractères. Utile pour vérifier des préfixes.

### Chercher dans une chaîne
- strchr(const char *s, int c) : Cherche la première occurrence du caractère c dans s. Renvoie un pointeur vers cette occurrence, ou NULL si non trouvé.
- strstr(const char *haystack, const char *needle) : Cherche la première occurrence de la sous-chaîne needle dans haystack. Renvoie un pointeur vers le début de l'occurrence, ou NULL.

### Focus sécurité : Le dépassement de Tampon(buffer overflow)
- C'est LE danger principal avec les chaînes en C.
- Si vous écrivez (avec strcpy, strcat, scanf non contrôlé, etc.) plus de données dans un tableau (buffer) qu'il ne peut en contenir, vous écrasez la mémoire qui se trouve après ce tableau.
- Conséquences : corruption de données d'autres variables, plantage du programme, et pire, failles de sécurité exploitables par des attaquants.
- Règle d'or : Toujours connaître la taille de vos buffers de destination et utiliser des fonctions qui respectent cette taille (strncpy, snprintf, strncat, fgets).

  
## Partie 5 : Lire les entrées utilisateurs : scanf, fgets
- scanf("%s", buffer) : Lit une séquence de caractères depuis l'entrée standard jusqu'au premier espace blanc (espace,  tabulation, nouvelle ligne). EXTRÊMEMENT DANGEREUX ! Ne connaît pas la taille de buffer et provoquera un dépassement de tampon si l'utilisateur tape plus de caractères que buffer ne peut en contenir (sans compter le \0).

- Pour sécuriser scanf (partiellement) : On peut spécifier une largeur maximale : scanf("%19s", buffer); lira au maximum 19 caractères dans buffer (qui doit avoir une taille d'au moins 20 pour le \0). C'est mieux, mais scanf reste délicat (gestion des espaces, etc.).

- fgets(char *buffer, int taille, FILE *stream) : LA MÉTHODE RECOMMANDÉE ET SÛRE.
  - Lit une ligne entière (y compris les espaces) depuis un flux (stream, souvent stdin pour le clavier).
  - Lit au maximum taille - 1 caractères et stocke le résultat dans buffer.
  - Ajoute toujours un \0 final.
  - S'arrête à la fin de ligne (\n) ou quand taille - 1 caractères sont lus.
  - Subtilité : fgets conserve le caractère de nouvelle ligne (\n) dans le buffer s'il y a assez de place. Il faut souvent le supprimer manuellement si on n'en veut pas.
```c
#include <stdio.h>
#include <string.h> // Pour strcspn ou strlen

int main() {
    char nomUtilisateur[50]; // Buffer de 50 chars

    printf("Entrez votre nom (max 49 car.) : ");

    // Lire depuis l'entrée standard (clavier) dans nomUtilisateur, max 50 octets
    if (fgets(nomUtilisateur, sizeof(nomUtilisateur), stdin) != NULL) {

        // Enlever le '\n' final si présent
        // strcspn cherche l'index du premier caractère qui est dans la chaîne fournie ("\n" ici)
        nomUtilisateur[strcspn(nomUtilisateur, "\n")] = '\0';

        // Ou alternative pour enlever le '\n'
        /*
        size_t len = strlen(nomUtilisateur);
        if (len > 0 && nomUtilisateur[len - 1] == '\n') {
            nomUtilisateur[len - 1] = '\0';
        }
        */

        printf("Bonjour, %s !\n", nomUtilisateur);

    } else {
        printf("Erreur de lecture.\n");
    }

    return 0;
}
``` 

# Buffer 
Un buffer est souvent simplement un tableau en mémoire, mais l'important est de comprendre comment il fonctionne dans le contexte des entrées/sorties, et comment il est utilisé pour stocker des données temporairement avant qu'elles ne soient traitées.

Imaginons un buffer comme une "boîte" dans laquelle on met des éléments, et cette boîte peut contenir un nombre fixe d'éléments. Par exemple, si vous avez un buffer de 100 caractères, vous avez une boîte où vous pouvez stocker jusqu'à 100 caractères. Vous allez y insérer des éléments (caractères, nombres, etc.), et une fois que le buffer est rempli, il faut soit le vider pour ajouter de nouveaux éléments, soit traiter les éléments déjà présents dans le buffer.

## Représentation du buffer dans le code
Prenons un exemple simple avec un tableau de 100 caractères, char buffer[100]; en C. On va visualiser ce qui se passe avec des commentaires.
```c
#include <stdio.h>

int main() {
    char buffer[100];  // Crée un buffer de 100 caractères
    // Imaginons que ce buffer est une série de cases mémoires que l'on peut remplir.
    // [0] [1] [2] [3] ... [99]  --> 100 cases, chaque case peut contenir un caractère (char).

    // Pour l'exemple, supposons que l'utilisateur entre la chaîne "Bonjour":
    // Le buffer va ressembler à ceci après avoir utilisé fgets():
    // [B] [o] [n] [j] [o] [u] [r] [\0] [ ] [ ] [ ] [ ] ... [ ] (les espaces sont vides)
    // [ ] [ ] [ ] [ ] ... [ ] [ ] [ ] [ ] (cases restantes vides)

    fgets(buffer, sizeof(buffer), stdin);  // On lit une ligne et on la stocke dans buffer

    printf("Buffer contient: %s\n", buffer);  // Affiche le contenu du buffer

    return 0;
}
```

Explication détaillée :
- Le buffer de 100 caractères (char buffer[100];) est simplement un tableau qui peut contenir jusqu'à 100 caractères.
- Lorsque vous utilisez fgets(buffer, sizeof(buffer), stdin), vous lisez un certain nombre de caractères du clavier et les placez dans ce tableau.
- Par exemple, si vous tapez "Bonjour", le tableau buffer va stocker chaque caractère à une position différente. Après cette lecture, le tableau ressemble à ceci (en mettant chaque caractère dans sa propre case de mémoire) :

```c
buffer[0] = 'B'
buffer[1] = 'o'
buffer[2] = 'n'
buffer[3] = 'j'
buffer[4] = 'o'
buffer[5] = 'u'
buffer[6] = 'r'
buffer[7] = '\0'  // Le caractère de fin de chaîne, signifiant que la chaîne est terminée.
buffer[8] = ' '   // Un espace vide après la chaîne.
buffer[9] = ' '   // Espace vide.
...
buffer[99] = ' '  // Espace vide.
```

## Déclarer un Buffer en C : Plusieurs Méthodes
Il y a principalement trois façons de déclarer un buffer en C :
### 1️⃣ Déclaration avec un tableau statique
```c
char buffer[100];  // Un buffer de 100 éléments (stocké sur la stack)
```
#### 📌 Explication :
- buffer est un tableau de 100 char (1 octet chacun).
- 100 signifie 100 octets (car char fait 1 octet en C).
- Stocké sur la stack, donc libéré automatiquement à la fin de la fonction.

### 2️⃣ Allocation dynamique avec malloc() ou calloc()
```c
uint8_t *memory_container = (uint8_t *)calloc(4, sizeof(uint8_t));
```

### 📌 Explication :
- uint8_t est un alias pour unsigned char (toujours 1 octet).
- calloc(4, sizeof(uint8_t)) alloue 4 octets en mémoire dynamique.
- Stocké sur le heap (nécessite free() après usage).

#### Équivalent avec malloc() :
```c
uint8_t *buffer = (uint8_t *)malloc(100 * sizeof(uint8_t));
```
📌 Ici, buffer stocke 100 octets sur le heap, et doit être libéré avec free(buffer);.

### Utiliser une structure pour gérer un buffer plus avancé
```c
typedef struct {
    uint8_t data[100];  // 100 octets de stockage
    size_t size;        // Taille actuelle
} Buffer;
```
📌 Explication :
- data[100] est un buffer de 100 octets.
- size permet de suivre combien d’octets sont réellement utilisés.

## 🔍 Que représente le 100 dans buffer[100] ?
Le 100 signifie 100 éléments du type du tableau.

| Type de buffer        | Taille d'un élément       | Taille totale en mémoire |
|-----------------------|--------------------------|--------------------------|
| `char buffer[100];`   | 1 octet                   | 100 octets               |
| `int buffer[100];`    | 4 octets (sur x86_64)     | 400 octets               |
| `uint8_t buffer[100];`| 1 octet                   | 100 octets               |
| `double buffer[100];` | 8 octets                  | 800 octets               |


👉 Ce n'est ni des bits, ni de l’hexadécimal, c’est juste un nombre d’éléments, et la taille réelle dépend du type.


## 🚀 Comparaison entre Stack et Heap pour un Buffer

| Critère         | Tableau statique (`buffer[100]`) | Allocation dynamique (`malloc()`) |
|----------------|--------------------------------|----------------------------------|
| **Taille**     | Fixe (définie à la compilation) | Dynamique (modifiable à l’exécution) |
| **Stockage**   | Stocké dans la **pile** (stack) | Stocké dans le **tas** (heap) |
| **Performance** | ⚡ Très rapide, car la mémoire est gérée automatiquement | 🐢 Plus lent, car il faut demander la mémoire au système |
| **Libération** | ✅ Automatique, dès que la fonction se termine | ❗ Manuelle, il faut appeler `free()` pour libérer la mémoire |
| **Risque**     | ⚠️ Risque d'overflow si la taille est trop grande | ❌ Risque d'erreur d’allocation si la mémoire est insuffisante |



## Pourquoi utiliser un buffer ?
- Performance : Plutôt que de lire un caractère à la fois, les programmes lisent et écrivent souvent en blocs. Cela réduit les appels système coûteux (comme read() et write()).
- Gestion de la mémoire : Un buffer vous permet de stocker temporairement des données dans la mémoire et de les traiter en toute sécurité avant de les utiliser dans votre programme.
- Entrées/Sorties (I/O) : Lorsque vous lisez ou écrivez dans des fichiers ou d'autres périphériques, un buffer est utilisé pour accumuler ou vider des données plus efficacement.


Au final Un buffer est essentiellement un tableau de mémoire dans lequel vous stockez temporairement des données. En utilisant des buffers, vous gérez efficacement la lecture et l'écriture de données, que ce soit dans des fichiers, des périphériques, ou l'entrée/sortie standard. Le buffer facilite la gestion de ces données en lot et améliore les performances du programme.


## SÉRIE D’EXERCICES : Maîtriser les Buffers en C

###🟢 Niveau 1 : Bases des Buffers
#### 1. Lire et afficher une chaîne avec fgets()
Objectif : Comprendre comment un buffer stocke une chaîne de caractères.
📌 Écrivez un programme qui :
- Demande à l’utilisateur d’entrer une chaîne de caractères (max 50 caractères
- Stocke cette entrée dans un buffer.
- Affiche le contenu du buffer.
⚠️ Attention : fgets() stocke aussi le \n, assurez-vous de le gérer si nécessaire.

#### 2. Expérimenter avec scanf("%c") et le buffer d’entrée
Objectif : Comprendre comment fonctionne le buffer du clavier.
📌 Écrivez un programme qui :
- Demande un caractère à l’utilisateur.
- Demande un second caractère juste après.
- Affiche les deux caractères.
❓ Problème : scanf("%c", &c); pose souvent problème à cause du buffer stdin qui garde les \n. Testez et corrigez !

### 🟡 Niveau 2 : Manipulation Avancée des Buffers
#### 3. Lire une ligne de texte sans fgets()
Objectif : Implémenter fgets() soi-même.
📌 Écrivez une fonction my_gets() qui :
- Lit caractère par caractère avec getchar().
- Stocke ces caractères dans un buffer.
- S’arrête lorsque \n est rencontré ou si le buffer est plein.
- Ajoute \0 à la fin.
```c
char buffer[100];
my_gets(buffer, 100);
printf("Vous avez écrit : %s\n", buffer);
```

### 4. Effacer le buffer d’entrée (stdin)
Objectif : Nettoyer le buffer après une mauvaise lecture.
📌 Implémentez une fonction clear_stdin() qui :
- Lit et vide tous les caractères restants jusqu’à \n.
- À utiliser après un scanf("%d") pour éviter des erreurs avec fgets() ensuite.
```c
int n;
char buffer[50];
printf("Entrez un nombre : ");
scanf("%d", &n);
clear_stdin();
printf("Entrez une phrase : ");
fgets(buffer, 50, stdin);
printf("Vous avez écrit : %s\n", buffer);
```

### 5. Lire une chaîne avec read() au lieu de fgets()
Objectif : Comprendre les buffers bas niveau.
📌 Utilisez read() au lieu de fgets() pour lire dans stdin :
```c
char buffer[50];
read(0, buffer, 50);
printf("Buffer : %s\n", buffer);
```
Que remarquez-vous ? Pourquoi y a-t-il des différences avec fgets() ?

### 🔴 Niveau 3 : Travaux pratiques sur les Buffers
#### 6. Lire un fichier en mémoire avec un buffer
Objectif : Lire un fichier par morceaux en utilisant un buffer.
📌 Écrivez un programme qui :
- Ouvre un fichier texte.txt.
- Lit 20 caractères à la fois avec fread().
- Affiche le contenu lu.
- Continue jusqu'à la fin du fichier.
```c
FILE *file = fopen("texte.txt", "r");
char buffer[20];
while (fread(buffer, 1, 20, file) > 0) {
    printf("%s", buffer);
}
fclose(file);
```

#### 7. Écrire dans un fichier avec un buffer
Objectif : Écrire progressivement dans un fichier
📌 Implémentez un programme qui :
- Ouvre output.txt en mode écriture.
- Écrit un texte dans le fichier en utilisant un buffer.
- Ferme le fichier.
Testez avec fprintf() vs fwrite() et comparez.

#### 8. Implémenter un getline() personnalisé
Objectif : Lire une ligne sans savoir sa taille à l’avance.
📌 Écrivez une fonction my_getline() qui :
- Alloue dynamiquement de la mémoire.
- Lit caractère par caractère.
- Agrandit le buffer dynamiquement si nécessaire (realloc()).
- Retourne une chaîne de caractères complète.


### 🟣 Niveau 4 : Défi Final - Buffer Circulaire
9. Implémenter un Circular Buffer (Buffer Circulaire)
Objectif : Créer un buffer circulaire capable de stocker un nombre limité de données et de les récupérer dans l’ordre.
📌 Le buffer doit :
- Stocker N éléments dans un tableau fixe.
- Avoir un pointeur de lecture et un pointeur d’écriture.
- Gérer les écrasements quand il est plein.

Exemple de fonctionnement attendu :
```c
CircularBuffer cb;
cb_init(&cb, 5);
cb_push(&cb, 'A');
cb_push(&cb, 'B');
cb_push(&cb, 'C');
char ch = cb_pop(&cb); // Doit retourner 'A'
```


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

#### a. Convertir un nombre en string
En C, voici plusieurs façons de convertir un int en string :
- Utiliser sprintf : Convertir un entier en une chaîne stockée dans un tableau de caractères.
- Utiliser itoa (non standard, disponible sur certaines implémentations comme MSVC).
- Utiliser snprintf : Similaire à sprintf, mais plus sûr pour éviter les dépassements de mémoire.
- Diviser manuellement le nombre et remplir un tableau de caractères en extrayant chaque chiffre (utile si on veut un contrôle total sans utiliser de bibliothèque).

```c
sprintf(buffer, format, valeurs...);
```
- buffer est un tableau de caractères où sera stockée la chaîne résultante.
- format est une chaîne de formatage (comme dans printf).
- valeurs... représente les valeurs à insérer dans la chaîne formatée.

```c
int nombre = 531;
char buffer[10];  // Assurez-vous que le buffer est assez grand
sprintf(buffer, "%d", nombre);
```

# Control flow
..todo


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


### Passer un tableau en paramêtre d'une fonction
#### 1. Pourquoi int my_array[] est équivalent à int *my_array ?
En C, lorsqu’un tableau est passé en argument à une fonction, il décaye automatiquement en pointeur vers son premier élément. Cela signifie que :
```c
int find_maximum_value(int my_array[]) { ... }
// Revient au même
int find_maximum_value(int *my_array){ ... }
```
Dans les deux cas, la fonction ne reçoit pas le tableau lui-même, mais l’adresse de son premier élément. Ainsi, toute modification faite à my_array dans la fonction affectera directement le tableau original.

#### 2. Problème : La perte de la taille du tableau
Le problème avec cette approche est que la fonction ne connaît pas la taille du tableau.
Exemple :
```c
void print_array(int my_array[]) {
    printf("Taille du tableau : %zu\n", sizeof(my_array) / sizeof(my_array[0]));
}
```

Si tu appelles print_array comme ceci :
```c
int tab[5] = {1, 2, 3, 4, 5};
print_array(tab);
```
Le résultat ne sera pas 5 mais une valeur incorrecte, car sizeof(my_array) ne donne pas la taille du tableau mais celle d’un pointeur (sizeof(int *)).

### Solution : Toujours passer explicitement la taille du tableau !
```c
void print_array(int my_array[], int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", my_array[i]);
    }
}
```

#### 3. Bonne pratique : Ajouter const si le tableau n’est pas modifié
Si ta fonction ne doit pas modifier le tableau, il est recommandé d’utiliser const :
```c
int find_maximum_value(const int my_array[], int size);
```
Cela empêche toute modification accidentelle et améliore la lisibilité du code.

#### Meilleure façon de déclarer une fonction qui prend un tableau en paramètre :

```c
int find_maximum_value(const int *my_array, int size);
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

# Pointeurs
## I. Introduction aux pointeurs

### Exercice 1 : Déclaration et affichage d’un pointeur (Facile)
📌 **Consigne** :  
- Déclare un entier et un pointeur vers cet entier.  
- Affiche l'adresse de la variable avec et sans le pointeur.  

💡 **Objectifs** : Comprendre comment déclarer un pointeur et afficher une adresse mémoire.  

### 📝 Instructions :
1. Déclare une variable `int a = 10;`
2. Déclare un pointeur `p` qui stocke l’adresse de `a`.
3. Affiche l’adresse de `a` en utilisant `&a`.
4. Affiche l’adresse de `a` en utilisant `p`.
5. Affiche la valeur de `a` en utilisant `p`.

### Exercice 2 : Modification d’une valeur via un pointeur (Facile)
📌 **Consigne** :  
Utilise un pointeur pour modifier la valeur d'une variable.  

💡 **Objectifs** : Comprendre l'utilisation de l'opérateur `*` pour accéder à la valeur pointée.  

### 📝 Instructions :
1. Déclare une variable `int b = 5;`.
2. Déclare un pointeur qui pointe vers `b`.
3. Modifie la valeur de `b` via le pointeur.
4. Affiche la valeur de `b` avant et après modification.

### Exercice 3 : Échange de deux variables avec pointeurs (Intermédiaire)
📌 **Consigne** :  
Échange les valeurs de deux variables en utilisant des pointeurs.  

💡 **Objectifs** : Comprendre comment utiliser des pointeurs pour modifier plusieurs variables.  
### 📝 Instructions :
1. Déclare deux entiers `int x = 3;` et `int y = 7;`.
2. Déclare deux pointeurs pointant vers `x` et `y`.
3. Échange leurs valeurs en utilisant uniquement les pointeurs.
4. Affiche les valeurs avant et après l’échange.

### Exercice 4 : Pointeur non initialisé et erreurs courantes (Intermédiaire)
📌 **Consigne** :  
Analyse ce qui se passe lorsque tu utilises un pointeur non initialisé.  

💡 **Objectifs** : Comprendre les risques liés aux pointeurs non initialisés.  

### 📝 Instructions :
1. Déclare un pointeur `int *ptr;` mais ne l'initialise pas.
2. Essaie d'afficher `*ptr` et observe le résultat.
3. Explique pourquoi cela provoque une erreur et corrige en initialisant `ptr` à `NULL`.

### Exercice 5 : Pointeurs et fonctions (Avancé)
📌 **Consigne** :  
Écris une fonction qui modifie une variable en utilisant un pointeur.  

💡 **Objectifs** : Comprendre le passage par adresse dans une fonction.  
### 📝 Instructions :
1. Écris une fonction `void increment(int *p)` qui prend un pointeur en paramètre et incrémente la valeur pointée.
2. Déclare une variable `n = 10;`, passe son adresse à `increment()` et affiche `n` avant et après l’appel.

## II. Working with pointers
### Exercice 1 : Pointeurs et déréférencement (Facile)

📌 **Consigne** :  
Déréférence un pointeur pour accéder à la valeur d’une variable.  

💡 **Objectifs** : Comprendre l’opérateur `*` pour déréférencer un pointeur.  

### 📝 Instructions :
1. Déclare un entier `a = 20;`.
2. Déclare un pointeur `p` qui pointe vers `a`.
3. Utilise le pointeur pour afficher la valeur de `a` en utilisant `*p`.
4. Modifie la valeur de `a` via le pointeur et affiche-la avant et après la modification.

### Exercice 2 : Pointeur vers un tableau (Facile)
📌 **Consigne** :  
Utilise un pointeur pour accéder aux éléments d’un tableau.  

💡 **Objectifs** : Apprendre à manipuler un tableau via un pointeur.  
### 📝 Instructions :
1. Déclare un tableau `int arr[] = {1, 2, 3, 4, 5};`.
2. Déclare un pointeur `p` pointant sur le premier élément du tableau.
3. Utilise un pointeur pour afficher chaque élément du tableau (en utilisant l’arithmétique des pointeurs).
4. Affiche les éléments du tableau un par un avec et sans utiliser le pointeur.

### Exercice 3 : Arithmétique des pointeurs (Intermédiaire)
💡 **Objectifs** :  
Comprendre comment l’arithmétique des pointeurs fonctionne pour accéder aux éléments d’un tableau.  

📌 **Consigne** :  
Manipule les pointeurs à l’aide de l’arithmétique des pointeurs.

### 📝 Instructions :
1. Déclare un tableau `int arr[] = {10, 20, 30, 40, 50};`.
2. Utilise un pointeur pour accéder au deuxième élément du tableau (en utilisant l’arithmétique des pointeurs).
3. Modifie la valeur du quatrième élément du tableau via le pointeur.
4. Affiche les éléments du tableau avant et après modification.

### Exercice 4 : Pointeur vers une structure (Intermédiaire)
💡 **Objectifs** :  
Apprendre à utiliser des pointeurs avec des structures.

📌 **Consigne** :  
Utilise un pointeur pour manipuler une structure en C.

### 📝 Instructions :
1. Déclare une structure `struct Person { char name[20]; int age; };`.
2. Déclare une variable de type `struct Person` et initialise-la avec des valeurs.
3. Déclare un pointeur vers cette structure et affiche ses membres via le pointeur.
4. Modifie les valeurs des membres de la structure via le pointeur et affiche les résultats.

### Exercice 5 : Pointeur et tableau de structures (Avancé)
💡 **Objectifs** :  
Comprendre comment utiliser des pointeurs avec des tableaux de structures.

📌 **Consigne** :  
Manipule un tableau de structures avec des pointeurs.

### 📝 Instructions :
1. Déclare un tableau de structures `struct Person persons[3] = {{"Alice", 30}, {"Bob", 25}, {"Charlie", 35}};`.
2. Utilise un pointeur pour accéder à chaque élément du tableau et afficher les informations.
3. Modifie l’âge de la première personne et affiche le tableau avant et après modification.
4. Implémente une fonction qui prend un pointeur vers un tableau de structures et modifie les informations de la structure.

## III. Pointer types, pointer arithmetic, void pointers
### Exercice 1 : Pointeur vers un type différent (Facile)

💡 **Objectifs** :  
Comprendre comment déclarer et utiliser des pointeurs vers différents types.

📌 **Consigne** :  
Crée un pointeur vers un type différent de `int` (par exemple, `float` ou `char`), et utilise-le pour accéder à la variable correspondante.

### 📝 Instructions :
1. Déclare une variable `float f = 3.14;`.
2. Déclare un pointeur `p` qui pointe vers `f`.
3. Affiche la valeur de `f` en utilisant le pointeur.
4. Change la valeur de `f` via le pointeur et affiche la nouvelle valeur.

### Exercice 2 : Arithmétique des pointeurs avec différents types (Intermédiaire)
💡 **Objectifs** :  
Comprendre l'impact de l’arithmétique des pointeurs en fonction des types de données.

📌 **Consigne** :  
Utilise l’arithmétique des pointeurs pour naviguer à travers un tableau de différents types.

### 📝 Instructions :
1. Déclare un tableau `int arr[] = {10, 20, 30, 40, 50};`.
2. Déclare un pointeur `p` pointant vers le premier élément du tableau.
3. Utilise l’arithmétique des pointeurs pour accéder au troisième élément et affiche sa valeur.
4. Répète la même opération pour un tableau de `float` (par exemple `float arr2[] = {1.5, 2.5, 3.5, 4.5};`) et affiche le deuxième élément.

### Exercice 3 : Pointeur `void` et conversion de type (Intermédiaire)

💡 **Objectifs** :  
Apprendre à utiliser les pointeurs `void` et à les convertir en pointeurs vers des types spécifiques.

📌 **Consigne** :  
Utilise un pointeur `void` pour manipuler différentes variables et effectue des conversions de type.

### 📝 Instructions :
1. Déclare une variable `int x = 10;` et une variable `double y = 20.5;`.
2. Déclare un pointeur `void *ptr;`.
3. Assigne à `ptr` l’adresse de `x`, puis affiche la valeur pointée (n’oublie pas de la convertir en `int` pour l'afficher).
4. Assigne à `ptr` l’adresse de `y`, puis affiche la valeur pointée (convertir en `double` pour l'afficher).


### Exercice 4 : Pointeur `void` avec fonction générique (Avancé)
💡 **Objectifs** :  
Utiliser des pointeurs `void` dans une fonction générique et effectuer une conversion de type à l’intérieur de la fonction.

📌 **Consigne** :  
Crée une fonction générique qui accepte un pointeur `void` pour traiter différents types de données.

### 📝 Instructions :
1. Crée une fonction `void print_value(void *ptr, char type)` qui prend un pointeur `void` et un type pour déterminer comment afficher la valeur pointée.
2. Si le type est `'i'`, la fonction doit afficher un entier.
3. Si le type est `'f'`, la fonction doit afficher un `float`.
4. Si le type est `'c'`, la fonction doit afficher un `char`.
5. Teste la fonction avec différentes variables et types (par exemple `int`, `float`, et `char`).


### Exercice 5 : Tableau de pointeurs avec arithmétique (Avancé)
💡 **Objectifs** :  
Utiliser l'arithmétique des pointeurs pour naviguer à travers un tableau de pointeurs.

📌 **Consigne** :  
Crée un tableau de pointeurs et utilise l'arithmétique des pointeurs pour manipuler ces pointeurs.

### 📝 Instructions :
1. Crée un tableau `int arr[] = {10, 20, 30, 40, 50};`.
2. Crée un tableau de pointeurs vers `int` : `int *ptr_arr[5];`.
3. Assigne à chaque élément du tableau de pointeurs l’adresse des éléments du tableau `arr`.
4. Utilise un pointeur pour accéder à chaque élément du tableau `arr` en utilisant l’arithmétique des pointeurs sur le tableau `ptr_arr`.
5. Affiche chaque valeur pointée dans le tableau de pointeurs.


## IV. Pointers to pointers in C
### Exercice 1 : Déclaration et utilisation d’un pointeur de pointeur (Facile)
💡 **Objectifs** :  
Comprendre comment fonctionne un pointeur vers un pointeur.

📌 **Consigne** :
Déclare et manipule un pointeur de pointeur pour accéder à une variable.

### 📝 Instructions :
 1. Déclare un entier int a = 10;
 2. Déclare un pointeur int *p qui pointe vers a
 3. Déclare un pointeur de pointeur int **pp qui pointe vers p
 4. Affiche la valeur de a en utilisant pp (double déréférencement **pp)
 5. Modifie a via pp et affiche la nouvelle valeur

### Exercice 2 : Modifier une variable via un pointeur de pointeur (Facile)
💡 **Objectifs** :  
Apprendre à modifier une variable en utilisant un pointeur de pointeur.

📌 **Consigne** : 
Utilise un pointeur de pointeur pour modifier la valeur d'une variable.
### 📝 Instructions :
 1. Déclare une variable int x = 5;
 2. Crée un pointeur int *p = &x; et un pointeur de pointeur int **pp = &p;
 3. Écris une fonction void modify_value(int **pp, int new_value) qui modifie la valeur de x via pp
 4. Affiche x avant et après l'appel de la fonction

### Exercice 3 : Tableaux et pointeurs de pointeurs (Intermédiaire)
💡 **Objectifs** :
Comprendre l’utilité des pointeurs de pointeurs pour stocker des tableaux dynamiques.

📌 **Consigne** : 
Utilise un pointeur de pointeur pour manipuler un tableau dynamique de pointeurs.

### 📝 Instructions :
 1. Déclare un tableau d’entiers int arr[] = {1, 2, 3, 4, 5};
 2. Déclare un tableau de pointeurs int *ptr_arr[5]; qui stocke les adresses de arr
 3. Déclare un pointeur de pointeur int **pp = ptr_arr;
 4. Utilise pp pour afficher les valeurs du tableau arr
 5. Modifie un élément du tableau via pp et affiche les valeurs avant et après modification


### Exercice 4 : Allocation dynamique avec pointeurs de pointeurs (Avancé)
💡 **Objectifs** :  
Comprendre comment utiliser des pointeurs de pointeurs pour gérer une matrice dynamique.

📌 **Consigne** : 
Alloue dynamiquement un tableau 2D en utilisant des pointeurs de pointeurs.

### 📝 Instructions :
 1. Déclare un pointeur de pointeur int **matrix;
 2. Alloue dynamiquement un tableau de 3 lignes et 3 colonnes en utilisant malloc
 3. Remplis la matrice avec des valeurs croissantes (1, 2, 3, ...)
 4. Affiche la matrice sous forme de tableau
 5. Libère la mémoire allouée dynamiquement

### Exercice 5 : Manipulation de chaînes de caractères avec un pointeur de pointeur (Avancé) 
💡 **Objectifs** :  
Comprendre comment manipuler des tableaux de chaînes avec des pointeurs de pointeurs.

📌 **Consigne** : 
Utilise un pointeur de pointeur pour manipuler un tableau de chaînes de caractères.

### 📝 Instructions :
 1. Déclare un tableau de chaînes de caractères :
 ```c
 char *words[] = {"Bonjour", "Pointeurs", "C"};
 ```
 2. Déclare un pointeur de pointeur char **pp = words;
 3. Utilise pp pour afficher chaque mot du tableau-
 4. Modifie le deuxième mot en lui attribuant une nouvelle chaîne de caractères
 5. Affiche à nouveau la liste des mots

## V. Pointers as function arguments
### Exercice 1 : Modifier une variable via un pointeur (Facile)
💡 **Objectifs** : 
Comprendre comment une fonction peut modifier directement une variable en utilisant un pointeur.

📌 **Consigne** : 
Passe un pointeur en argument d’une fonction pour modifier une variable.

### 📝 Instructions :
 1. Déclare une fonction void update_value(int *p, int new_value) qui modifie la valeur pointée par p
 2. Déclare un entier int x = 5; et affiche sa valeur
 3. Appelle update_value(&x, 10); puis affiche la nouvelle valeur de x

### Exercice 2 : Échanger deux variables avec des pointeurs (Facile)
💡 **Objectifs** :  
Apprendre à manipuler plusieurs pointeurs dans une fonction.

📌 **Consigne** : 
Utilise une fonction qui prend deux pointeurs en argument pour échanger deux variables.

### 📝 Instructions :
 1. Déclare une fonction void swap(int *a, int *b) qui échange les valeurs de a et b
 2. Déclare deux entiers int x = 10, y = 20; et affiche leurs valeurs
 3. Appelle swap(&x, &y); puis affiche les nouvelles valeurs

### Exercice 3 : Manipuler un tableau avec un pointeur en argument (Intermédiaire)
💡 **Objectifs** :  
Comprendre comment un tableau est passé par référence dans une fonction.

📌 **Consigne** : 
Passe un tableau à une fonction et modifie son contenu.

### 📝 Instructions :
 1. Déclare une fonction void multiply_by_two(int *arr, int size) qui multiplie chaque élément du tableau par 2
 2. Déclare un tableau int numbers[] = {1, 2, 3, 4, 5};
 3. Affiche le tableau avant et après l’appel de la fonction

### Exercice 4 : Allouer dynamiquement un tableau dans une fonction (Avancé)
💡 **Objectifs** :
Comprendre comment une fonction peut allouer de la mémoire et modifier un pointeur passé en argument.

📌 **Consigne** : 
Utilise un pointeur passé en argument pour allouer dynamiquement un tableau.

### 📝 Instructions :
 1. Déclare une fonction void allocate_array(int **arr, int size) qui alloue un tableau dynamiquement et initialise ses valeurs à size * i
 2. Dans main(), déclare un pointeur int *array = NULL;
 3. Appelle allocate_array(&array, 5);
 4. Affiche le tableau puis libère la mémoire

### Exercice 5 : Fonction retournant un pointeur alloué dynamiquement (Avancé)

💡 **Objectifs** :  
Comprendre comment une fonction peut renvoyer un pointeur sur une zone allouée dynamiquement.

📌 **Consigne** : 
Écris une fonction qui alloue un tableau et retourne un pointeur vers celui-ci.

### 📝 Instructions :
 1. Déclare une fonction int* create_array(int size) qui retourne un tableau dynamique
 2. Alloue un tableau de size éléments, remplis-le avec des valeurs croissantes
 3. Retourne le pointeur du tableau
 4. Dans main(), appelle create_array(5), affiche les valeurs, puis libère la mémoire

## VI. Pointers and arrays

### Exercice 1 : Accéder aux éléments d’un tableau avec un pointeur (Facile)
💡 **Objectifs** :  
Comprendre comment un pointeur peut être utilisé pour accéder aux éléments d’un tableau.

📌 **Consigne** : 
Utilise un pointeur pour parcourir un tableau et afficher ses éléments.

### 📝 Instructions :
 1. Déclare un tableau int numbers[] = {10, 20, 30, 40, 50};
 2. Déclare un pointeur int *ptr = numbers;
 3. Utilise une boucle for pour afficher tous les éléments du tableau en utilisant ptr
 4. Incrémente ptr à chaque itération pour parcourir le tableau

### Exercice 2 : Modifier un tableau avec un pointeur (Facile)
💡 **Objectifs** :  
Apprendre à modifier les valeurs d’un tableau via un pointeur.

📌 **Consigne** : 
Utilise un pointeur pour modifier les éléments d’un tableau.

### 📝 Instructions :
 1. Déclare un tableau int numbers[] = {1, 2, 3, 4, 5};
 2. Déclare un pointeur int *ptr = numbers;
 3. Utilise une boucle pour multiplier chaque élément du tableau par 2 via le pointeur
 4. Affiche les valeurs du tableau avant et après modification

### Exercice 3 : Comparaison entre notation tableau et pointeur (Intermédiaire)
💡 **Objectifs** :  
Comprendre la relation entre array[i] et *(ptr + i).

📌 **Consigne** : 
Accède aux éléments d’un tableau en utilisant deux notations différentes.

### 📝 Instructions :
 1. Déclare un tableau int numbers[] = {3, 6, 9, 12, 15};
 2. Déclare un pointeur int *ptr = numbers;
 3. Affiche les éléments du tableau en utilisant les deux notations suivantes :
```c
    numbers[i]
    *(ptr + i)
```

### Exercice 4 : Fonction qui prend un tableau en paramètre (Avancé)

💡 **Objectifs** :  
Comprendre que lorsqu’un tableau est passé à une fonction, il est en fait passé sous forme de pointeur.

📌 **Consigne** : 
Crée une fonction qui prend un tableau comme argument et le modifie via un pointeur.

### 📝 Instructions :
 1. Déclare une fonction void square_elements(int *arr, int size) qui élève chaque élément au carré
 2. Déclare un tableau int values[] = {2, 4, 6, 8};
 3. Appelle la fonction et affiche les valeurs avant et après modification

### Exercice 5 : Trouver le plus grand élément d’un tableau avec un pointeur (Avancé)
💡 **Objectifs** : 
Apprendre à parcourir un tableau avec un pointeur pour effectuer une opération.

📌 **Consigne** : 
Écris une fonction qui trouve le plus grand élément d’un tableau en utilisant un pointeur.

### 📝 Instructions :
 1. Déclare une fonction int find_max(int *arr, int size) qui retourne la plus grande valeur d’un tableau
 2. Parcours le tableau avec un pointeur et trouve la valeur maximale
 3. Déclare un tableau int data[] = {10, 25, 35, 20, 50};
 4. Appelle la fonction et affiche la valeur maximale


// Depracated
Les * en C ont deux significations principales, et c’est là que la confusion vient souvent. Je vais t’expliquer ligne par ligne en détaillant ce qu’il se passe avec * et & pour que ce soit limpide.

## 🔹 1. Déclaration d'un pointeur
```c
int* number;
```
Ici, le * indique que number est un pointeur vers un entier.
👉 Cela signifie que number stocke une adresse mémoire, et non une valeur directe.

Par exemple :
```c
int x = 5;
int* ptr = &x;
```
- ptr est un pointeur qui contient l'adresse de x.
- &x signifie "donne-moi l'adresse de x", qu'on stocke dans ptr.

## 🔹 2. Dé-référencement d'un pointeur (* pour accéder à la valeur)
```c
*number = *number * 2;
```

```c
*number = quelque_chose;
// "Va à l'adresse contenue dans number et mets-y cette nouvelle valeur."
// On ne stocke pas une adresse ici, on stocke une valeur à l'endroit où pointe number.
```

Ensuite, *number * 2 → Lire la valeur avant de la modifier
```c
*number = *number * 2;
```
La partie *number * 2 est évaluée en premier :
- Dé-référence number pour obtenir la valeur stockée à son adresse.
- Multiplie cette valeur par 2.
- Stocke le résultat à la même adresse.

## Lorsqu'il est utilisé dans une déclaration de variable
Lorsqu'il est utilisé dans une déclaration de variable, comme int* nom_de_argument, cela signifie que la variable nom_de_argument est un pointeur vers un entier. Un pointeur est une variable qui stocke une adresse mémoire et non une valeur directe.

En C, les arguments sont passés par valeur par défaut, ce qui signifie que la fonction travaille avec une copie de la variable. Si tu veux que la fonction modifie la valeur d'une variable dans la fonction appelante, tu dois lui passer un pointeur (c'est-à-dire l'adresse de la variable).

En utilisant des pointeurs, la fonction get_unique_number peut modifier directement les valeurs des variables centaines, dizaines, et unites dans main, car elle travaille avec leurs adresses mémoire, et non une copie de leurs valeurs.

## 🔹 Synthèse des rôles de `*` et `&`

| Symbole       | Signification                                           |
|--------------|----------------------------------------------------------|
| `int* ptr;`  | `ptr` est un pointeur vers un `int` (stocke une adresse) |
| `ptr = &x;`  | `ptr` stocke l'adresse de `x`                            |
| `*ptr`       | Accède/modifie la valeur à l’adresse pointée             |
| `&x`         | Donne l'adresse de `x`                                   |

## Pointeurs de fonctions
Les pointeurs de fonction en C permettent de stocker l'adresse d'une fonction et de l'appeler via ce pointeur.  
- Ils sont utilisés dans divers cas où on a besoin de choisir dynamiquement quelle fonction appeler à l'exécution..
- Cela permet de rendre le code plus flexible et d'implémenter des concepts comme les callbacks, l'extension de bibliothèques, ou les fonctions de tri et de recherche paramétrables par des comparateurs.

### Qu'est-ce qu'un pointeur de fonction ?
Un pointeur de fonction est une variable qui contient l'adresse d'une fonction. De cette façon, tu peux appeler la fonction à partir du pointeur.

### Syntaxe des pointeurs de fonction
Pour déclarer un pointeur de fonction, on indique d'abord le type de la fonction pointée, puis on utilise un astérisque (*) pour le pointeur, suivi des paramètres de la fonction.
```c
return_type (*pointer_name)(parameter_type_1, parameter_type_2, ...);
```

Exemple concret : Supposons que nous ayons une fonction qui prend un int et retourne un int :
#### 1. Déclaration d'un pointeur de fonction.
```c
int add_one(int x) {
    return x + 1;
}

// Pour déclarer un pointeur vers cette fonction :

int(*p)(int)
// Même type de retour que celui de la fonction.
// *p nom du pointeur
// type du paramètre
```

#### 2. Initialisation d'un pointeur de fonction
Pour initialiser un pointeur de fonction, on assigne l'adresse de la fonction à ce pointeur :
```c
p = add_one;
```
Maintenant, p pointe vers la fonction add_one.

#### 3. Appel via le pointeur de fonction 
```c
int result = p(5);  // Appelle add_one(5) via le pointeur
```
Cela aura le même effet que d'appeler directement la fonction add_one(5).


# Gestion de la memoire
## Malloc
malloc() est utilisé pour allouer dynamiquement un bloc de mémoire sur le tas.
Syntaxe :
```c
void *malloc(size_t taille);
```
- Size_t taille : le nombre d'octets à allouer.
- Renvoie un pointeur vers la première adresse du bloc mémoire alloué.
- Si l'allocation échoue (manque de mémoire), malloc() renvoie NULL.
- Le contenu de la mémoire allouée n'est pas initialisé (elle peut contenir des valeurs aléatoires).

```c
int *tableau = malloc(5 * sizeof(int)); // Alloue un tableau de 5 entiers

if (tableau == NULL) {
    printf("Allocation échouée\n");
    return 1; // Sortie du programme
}

// Remplir le tableau
for (int i = 0; i < 5; i++) {
    tableau[i] = i * 2;
}

free(tableau); // Libérer la mémoire après utilisation
```

#### Exemple avec plusieurs fonctions et un pointeur de fonction : 
Cet exemple montre comment utiliser des pointeurs de fonction pour appeler différentes fonctions selon les besoins
```c
#include <stdio.h>

// Déclaration de fonctions
int add(int x, int y) {
    return x + y;
}

int subtract(int x, int y) {
    return x - y;
}

int multiply(int x, int y) {
    return x * y;
}

int main() {
    // Déclaration du pointeur de fonction
    int (*operation)(int, int);

    // Utilisation du pointeur pour appeler différentes fonctions
    operation = add;
    printf("Addition : %d\n", operation(3, 4)); // 7

    operation = subtract;
    printf("Soustraction : %d\n", operation(5, 2)); // 3

    operation = multiply;
    printf("Multiplication : %d\n", operation(2, 6)); // 12

    return 0;
}
```

#### Exemple avec un tableau de pointeurs de fonction
Si tu as plusieurs fonctions qui ont la même signature (même type de retour et même type d'arguments), tu peux aussi créer un tableau de pointeurs de fonction pour les gérer dynamiquement.
```c
#include <stdio.h>

// Déclaration de fonctions
int add(int x, int y) {
    return x + y;
}

int subtract(int x, int y) {
    return x - y;
}

int multiply(int x, int y) {
    return x * y;
}

int divide(int x, int y) {
    return y != 0 ? x / y : 0;  // Evite la division par 0
}

int main() {
    // Tableau de pointeurs de fonction
    int (*operations[])(int, int) = {add, subtract, multiply, divide};

    // Appel de chaque fonction via le tableau
    printf("Addition : %d\n", operations[0](3, 4));
    printf("Soustraction : %d\n", operations[1](7, 2));
    printf("Multiplication : %d\n", operations[2](3, 5));
    printf("Division : %d\n", operations[3](10, 2));

    return 0;
}
```

#### Fonction de comparaison par tri 
```c
#include <stdio.h>
#include <stdlib.h>

// Fonction de comparaison pour tri croissant
int compare_ascending(const void *a, const void *b) {
    return (*(int*)a - *(int*)b);
}

// Fonction de comparaison pour tri décroissant
int compare_descending(const void *a, const void *b) {
    return (*(int*)b - *(int*)a);
}

int main() {
    int arr[] = {5, 2, 9, 1, 5, 6};
    int size = sizeof(arr) / sizeof(arr[0]);

    // Tri croissant
    qsort(arr, size, sizeof(int), compare_ascending);

    // Affichage du tableau trié
    printf("Tri croissant : ");
    for (int i = 0; i < size; i++) printf("%d ", arr[i]);
    printf("\n");

    // Tri décroissant
    qsort(arr, size, sizeof(int), compare_descending);

    // Affichage du tableau trié
    printf("Tri décroissant : ");
    for (int i = 0; i < size; i++) printf("%d ", arr[i]);
    printf("\n");

    return 0;
}
```
#### 🔍 Où est le pointeur de fonction ?
- 👉 compare_ascending et compare_descending sont des fonctions.
- 👉 qsort() attend un pointeur de fonction comme dernier argument.
- 👉 On passe directement compare_ascending ou compare_descending à qsort(), ce qui lui permet de choisir dynamiquement la méthode de comparaison.

#### La fonction qsort() est définie ainsi :
```c
void qsort(void *base, size_t nitems, size_t size, 
           int (*compar)(const void *, const void *));
```
- 🔹 compar est un pointeur de fonction qui prend deux pointeurs génériques (void *) et retourne un int.
- 🔹 Ce pointeur permet à qsort() d’appeler dynamiquement la fonction de comparaison fournie par l’utilisateur.
- ✅ En lui passant compare_ascending, qsort() sait qu'il doit trier du plus petit au plus grand.
- ✅ En lui passant compare_descending, qsort() sait qu'il doit trier du plus grand au plus petit.

#### Utilisation des pointeurs de fonction pour des callbacks
Les pointeurs de fonction sont très utiles dans des situations où tu veux passer des fonctions comme arguments à d'autres fonctions. Cela permet une grande flexibilité, par exemple dans les bibliothèques de tri ou de recherche.
- Voici un exemple d'utilisation d'un pointeur de fonction comme "callback" dans une fonction de tri :
```c
#include <stdio.h>

// Fonction de tri par ordre croissant
int ascending(int a, int b) {
    return a - b;
}

// Fonction de tri par ordre décroissant
int descending(int a, int b) {
    return b - a;
}

// Fonction de tri générique
void sort(int arr[], int size, int (*cmp)(int, int)) {
    for (int i = 0; i < size - 1; i++) {
        for (int j = i + 1; j < size; j++) {
            if (cmp(arr[i], arr[j]) > 0) {
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }
}

// Fonction pour afficher un tableau
void print_array(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int arr[] = {7, 3, 9, 1, 5};
    int size = 5;

    // Trier par ordre croissant
    sort(arr, size, ascending);
    print_array(arr, size); // Affiche 1 3 5 7 9

    // Trier par ordre décroissant
    sort(arr, size, descending);
    print_array(arr, size); // Affiche 9 7 5 3 1

    return 0;
}
```
#### 📌 Conclusion : Quand utiliser les pointeurs de fonction ?
Les pointeurs de fonction sont utiles pour : ✔ Rendre le code générique : une seule fonction pour gérer plusieurs cas.
- ✔ Éviter la duplication de code : on ne répète pas la même logique avec juste des if différents.
- ✔ Choisir dynamiquement une fonction : par exemple en fonction d'un choix de l'utilisateur.
- ✔ Utiliser des callbacks : très utile dans les bibliothèques et les API.
- ✔ Créer des structures extensibles : comme une table d’événements ou une liste de traitements.

#### 📚 Exercice pratique
- Créer une fonction find_value() qui prend un tableau et un pointeur de fonction (min ou max) et retourne la valeur correspondante.
- Créer une calculatrice qui prend une opération (+, -, *, /) sous forme de paramètre et exécute dynamiquement la bonne fonction.
- Créer un menu dynamique : L’utilisateur choisit une option (1 : dire bonjour, 2 : dire au revoir, etc.), et un pointeur de fonction exécute la bonne fonction.



## Calloc (Clear allocation)
calloc() fonctionne comme malloc(), mais il initialise la mémoire à zéro.
Syntaxe : 
```c

```
- n : nombre d'éléments à allouer.
- taille : taille de chaque élément en octets.
- Renvoie un pointeur vers la mémoire allouée, initialisée à zéro.

#### Différences avec malloc() :
✅ Initialise la mémoire à zéro.
❌ Plus lent que malloc(), car il remplit la mémoire avec des 0.

Exemple :
```c
int *tableau = calloc(5, sizeof(int)); // Alloue et initialise un tableau de 5 entiers à 0

if (tableau == NULL) {
    printf("Allocation échouée\n");
    return 1;
}

// Afficher les valeurs (toutes initialisées à 0)
for (int i = 0; i < 5; i++) {
    printf("%d ", tableau[i]); // Affiche : 0 0 0 0 0
}

free(tableau); // Libérer la mémoire
```
- malloc() ne fait que réserver la mémoire, mais laisse les anciennes valeurs (potentiellement aléatoires).
- calloc() réserve ET initialise la mémoire à 0.

## Realloc (réallocation)
realloc() est utilisé pour redimensionner un bloc de mémoire alloué précédemment par malloc() ou calloc().

Syntaxe :
```c
void *realloc(void *ptr, size_t nouvelle_taille);
```
- ptr : pointeur vers la mémoire déjà allouée.
- nouvelle_taille : nouvelle taille en octets.
- Si ptr == NULL, realloc() se comporte comme malloc(nouvelle_taille).
- Si nouvelle_taille == 0, realloc() libère la mémoire et retourne NULL.
- Peut déplacer la mémoire si l'espace adjacent n'est pas disponible.

```c
int *tableau = malloc(3 * sizeof(int)); // Alloue un tableau de 3 entiers

if (tableau == NULL) {
    printf("Allocation échouée\n");
    return 1;
}

// Initialisation
for (int i = 0; i < 3; i++) {
    tableau[i] = i + 1; // 1, 2, 3
}

// Agrandir le tableau à 6 éléments
tableau = realloc(tableau, 6 * sizeof(int));

if (tableau == NULL) {
    printf("Reallocation échouée\n");
    return 1;
}

// Initialisation des nouvelles valeurs
for (int i = 3; i < 6; i++) {
    tableau[i] = (i + 1) * 2; // 8, 10, 12
}

// Affichage
for (int i = 0; i < 6; i++) {
    printf("%d ", tableau[i]); // Affiche : 1 2 3 8 10 12
}

free(tableau);
```
📌 À noter :
- realloc() peut changer l'adresse mémoire si l'espace contigu est insuffisant.
- Il copie les anciennes valeurs dans le nouvel emplacement si la mémoire est déplacée.

## Free (Libération de mémoire)
free() est utilisé pour libérer la mémoire allouée dynamiquement.

Syntaxe :

```c
void free(void *ptr);
```
- ptr : pointeur vers un bloc mémoire alloué par malloc(), calloc() ou realloc().
- Après free(ptr), ptr devient invalide.
- Ne remet pas à zéro le pointeur ! Il faut donc éviter d'accéder à ptr après un free().

Exemple : 
```c
int *tableau = malloc(5 * sizeof(int));

if (tableau == NULL) {
    printf("Allocation échouée\n");
    return 1;
}

// Faire quelque chose avec le tableau...

free(tableau); // Libération de la mémoire
tableau = NULL; // Bonne pratique : éviter l'accès à une mémoire libérée
```
📌 Pourquoi mettre tableau = NULL après free() ?
- Un accès à tableau après free() provoquerait un comportement indéfini (segmentation fault).
- Mettre NULL permet d'éviter un accès accidentel à une mémoire libérée.

⚠️ Bonnes pratiques à retenir
- ✔ Toujours vérifier si malloc(), calloc(), ou realloc() retourne NULL avant d'utiliser la mémoire allouée.
- ✔ Libérer la mémoire avec free() une fois qu'elle n'est plus nécessaire.
- ✔ Mettre NULL au pointeur après free() pour éviter des erreurs d’accès mémoire.
- ✔ Utiliser calloc() si on veut une mémoire déjà initialisée à 0.
- ✔ Faire attention avec realloc(), car l'adresse mémoire peut changer ! Toujours affecter le résultat à la même variable.

# Struct
Une struct (structure) en C permet de regrouper plusieurs variables sous un même type. C'est un moyen d'organiser des données associées dans un seul bloc mémoire.
💡 Exemple simple :
Si tu veux gérer un point en 2D, tu pourrais avoir :
- Un x
- Un y
➡️ Plutôt que d'utiliser deux variables séparées, une struct du nom de Point peut les regrouper.
```c
#include <stdio.h>

// Définition de la struct Point
struct Point {
    int x;
    int y;
};

int main() {
    struct Point p1 = {10, 20}; // Création et initialisation d'un point

    printf("Coordonnées du point : (%d, %d)\n", p1.x, p1.y);
    return 0;
}
```

# Retour multiple 
Le retour multiple de valeurs via return est impossible dans C car cette instruction ne permet de retourner qu'une seule valeur. 

## 📌 Solutions pour retourner plusieurs valeurs :

Il existe plusieurs méthodes pour contourner cette limitation et retourner plusieurs valeurs dans une fonction :

## 1. Utiliser des paramètres de sortie avec des pointeurs (méthode la plus courante)
Tu peux passer des pointeurs vers les variables qui doivent contenir les résultats, et la fonction modifiera directement ces variables.
```c
#include <stdio.h>

void update_value(int* number) {
    *number = *number * 2;  // On dé-référence pour modifier la valeur à l'adresse mémoire
}

int main() {
    int num = 5;
    update_value(&num);  // Passer l'adresse de num
    printf("Num après update_value : %d\n", num);  // Affiche 10
    return 0;
}
```
- Ici, la fonction update_value prend un pointeur vers un entier (int* number). En utilisant *number, on accède à la valeur de num dans main et on peut la modifier directement. Le résultat affiché sera 10, car la valeur de num a été modifiée par référence.


# Data type


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
