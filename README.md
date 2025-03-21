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


# 2. Partie 1 : Structure du projet

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
    
###ifndef 
signifie "If Not Defined" en anglais, ou "Si non défini" en français.
- Cela veut dire : "Si la macro FAHRENHEIT_H n’est pas encore définie".
- Si FAHRENHEIT_H n'est pas encore défini, alors le code entre #ifndef et #endif va être exécuté.

Cela sert à dire au préprocesseur qu'il doit vérifier si la macro FAHRENHEIT_H existe déjà. Si elle n'existe pas, il va inclure le code qu'il y a après. Si la macro existe déjà (c’est-à-dire si le fichier a déjà été inclus), alors le préprocesseur ignorera ce bloc de code.

###define FAHRENHEIT_H (Définir FAHRENHEIT_H)
-define est une directive de préprocesseur qui permet de définir une macro. Cela signifie que tu donnes un nom (dans ce cas, FAHRENHEIT_H) et tu le "définis" pour qu'il existe dans ton programme.
-Une fois qu'une macro est définie, son nom peut être utilisé pour vérifier dans d'autres parties du programme, afin de savoir si une certaine section de code a déjà été incluse ou non.

Dans ton exemple, #define FAHRENHEIT_H sert à dire "Maintenant, la macro FAHRENHEIT_H existe". Cela indique au préprocesseur qu'il a déjà inclus ce fichier d'en-tête et qu'il ne doit pas le réinclure si cela se reproduit.

###endif (Fin de la condition)

- endif est une directive de préprocesseur qui marque la fin d'une section conditionnelle commencée avec #if, #ifndef ou #ifdef.
- Dans ce cas, cela marque la fin de la section conditionnelle où le préprocesseur a vérifié si la macro FAHRENHEIT_H était déjà définie.

Donc, #endif signifie simplement "fin de la condition". Cela indique que le bloc conditionnel est terminé et que le préprocesseur peut continuer avec le reste du code.



## Contenu des fichiers `/tests`
## Contenu des fichiers `/Makefile`
