# Le Malloc

Le Malloc est une fonctionnalité de base du C et est une notion liée aux pointeurs et à la mémoire. Malloc est une fonction qui permet au programme de demander une certaine quantité de mémoire, exprimer en octet (ou bytes = 8 bit), à l'OS. Le malloc est très important car l'un des deux seuls moyens d'obtenir de la mémoire pour le programme.
La première, la plus classique, est effectuer automatiquement par le compilateur lorsque l'on crée une variable mais on à un espace mémoire qui est assez limité, si l'on dépasse cette mémoire on obtient le fameux stackoverflow. Malloc permet de dépasser cette limitation et permet d'avoir bien plus de mémoire (le maximum étant la RAM disponible dans le pc).

## Entrons dans le détail

Pour faire appel au malloc on fait comme suit:

```c
  int* p_avion;
  int nb_avion = 1;
  p_avion = malloc(sizeof(*p_avion) * nb_avion);
```

Pour commencer on crée un pointeur sur int qui pour l'instant ne contient rien (ne contient aucune adresse).
Ensuite dans la fonction malloc on utilise la fonction sizeof(). Cette fonction permet de récupérer la taille en octet du type de la variable qui se trouve à l'intérieur.
Ici la variable qui se trouve en paramètre est le '*p_avion', donc le déréférencement de p_avion, qui référence donc une varibale de type int. 
C'est comme si l'on avait fait sizeof(int). Celui ci renvoie tout simplement 4, car un int, en générale, fait 4 octets. 
Donc pour simplifier on aurait pue remplacer par malloc(4 * nb_avion) ou même malloc(4).

### Qu'est ce que malloc va faire de cela ?

Malloc va demander à l'OS d'allouer 4 octets de mémoire pour le programme et va nous retourner son adresse. 
La variable p_avion va donc au final recevoir une adresse. Cette adresse pointe vers l'espace nouvellement reserver. 
Cet espace fait 4 octet soit assez pour contenir une variable "avion" (qui est de type int).
Si l'on veut reserver plus d'espace on à juste à multiplier par un nombre plus grand, ici on augmenterais nb_avion. 
Cela nous permetais de reserver plus d'espace.

### Maintenant que l'on à l'adresse on fait quoi ?

Bah maintenant on se retrouve avec un pointeur qui pointe vers un espace de 4 octet. On peut y placer donc ce que l'on veut qui ne dépasse pas 4 octet.

Pour faire cela on fait:

```c
  int vieux_cesna = 350;
  *p_avion = vieux_cesna;
```

Ainsi à l'emplacement mémoire p_avion il y a la valeur 350.


## Le Free

Après avoir demander à l'OS d'allouer de l'espace à notre programme il est judicieux de faire ce que l'on appel un free, c'est à dire libérer cette espace. On dit à l'OS que l'on à plus besoin de cette espace, et qu'il peut donc etre utiliser par un autre programme. Si l'on fait pas cela, ou que l'on ne le fait pas correctement notre programme sera sujet à des "memory leak", c'est à dire des fuites de mémoires. Derrière ces mots un peu effrayant il y a juste le fait que notre programme prend de plus en plus d'espace mémoire, ce qu'il fait qu'il peut utiliser bien plus de RAM que nécaissaire, cela peut même faire planter le programme si y'a plus de RAM disponible.

Pour cela on fait:

```c
  free(p_avion);
```

On met en paramètre de free tout simplement le pointeur (la variable) qui contient l'adresse de l'emplacement mémoire qui nous avez était allouer.
//Après cette opération notre pointeur ne pointe plus vers l'emplacement mémoire précedent.

// est ce qu'il faut mettre NULL avant de faire une free? Ca serait intéressant de le savoir et ca parait logique. *p_avion = NULL
