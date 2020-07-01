# Les structures avec Struct

Les structures sont une fonctionnalités avancées du language C et sont importante pour crée des types personnalisés dérivés des types de bases. Les structures sont très utiles lorsque l'on veut crée des structures de données spécifiques comme listes chainées par exemple. On peut voir les Struct comme une classe mais qui ne contient que des variables (attributs) mais pas de fonctions (méthodes). 

### Comment fait t on pour créer une Struct ?

On procède comme suit:

```c
  struct keyValuePair {
      int key;
      int value;
  };
```

Pour l'utiliser on fait ceci dans le code:

```c
    struct keyValuePair k;
    k.key = 7;
    k.value = 15;
    printf("%d\n", k.key);
```

Le type keyValuePair fait une taille de (int + int). En fait lorsque l'on crée un keyValuePair le programme fait comme si il crée deux type int cote à cote. 
Pour accéder au premier int on fait key et pour accéder au second int on fait value.


### Un pointeur sur fonction dans une structure, une class-like

On peut crée une structure qui ressemble à une classe à l'aide des pointeurs sur fonction.
On doit ajouter un pointeur sur fonction dans la structure.

On fait comme suit:

```c

  void printHello();
  void printMsg(char* msg);

  struct keyValuePair {
      int key;
      int lastIndex;
      void (*printHello)();
      void (*printM)(char* msg);
  };


  int main()
  {
      struct keyValuePair k;
      k.key = 7;
      k.lastIndex = 15;
      // assignation
      k.printHello = &printHello;
      k.printM = &printMsg;
      // utilisation
      k.printHello();
      k.printM("Hey mon pote\n");

      return 0;
   }

   void printHello() {
     printf("Hello\n");
    }

    void printMsg(char* msg) {
      printf("%s\n", msg);
    }
```
