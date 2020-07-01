# Les pointeurs, une drôle d'histoire


Les pointeurs est un concept clef du C. C'est ce qui fait sa force et ce qui fait aussi sa difficulté (enfin perso je trouve le concept plutôt facile à comprendre mais difficile à maitriser). Les pointeurs permettent de manipuler la mémoire (la RAM) directement.

Les languages basé sur le C, cachent en quelques sortes cette aspect en créant des automatismes.

En C pour obtenir l'addresse mémoire d'une variable il faut faire ca:
```c
  int prix_voiture = 3000;

  &prix_voiture;
```
Le & permet d'obtenir l'addresse mémoire de la variable prix_voiture qui contient la valeur 3000, qui correspond au prix de la voiture.

Pour stocker cette addresse il faut utiliser une variable spéciale que l'on nomme pointeur.

Pour ce faire:
```c
int* p_prix = &prix_voiture;
```

Le int * permet de crée un pointeur sur une variable de type int. Ce pointeur, qui est une variable, qui contient une addresse, l'addresse de la variable prix_voiture.

Maintenant que l'on à l'addresse mémoire de la variable prix_voiture si l'on veut savoir qu'elle est la valeur contenue dans cette variable il faut faire ce que l'on appel un déréférencement. C'est à dire simplement obtenir la valeur à cette addresse.

Pour ce faire:
```c
int val = 0;

val = *p_prix;
```

Le * devant p_prix permet cette fois ci de déréférencer. Alors que lors de la création l'étoile indique que la valeur est de type pointeur. Du coup val vaut 3000.

Avec les fonctions

L'utilisation de pointeur peut etre utile lorsque l'on utilise des fonctions. En effet un des problème avec les fonctions c'est que les variables à l'intérieur sont temporaires, elle sont détruites lorsque l'on arrive à la fin de la fonction.

Mais la fonction nous renvoie qu'une seul valeur (qui peut en fait etre plusieurs, si c'est un tableau, ou un objet) alors que si l'on veut modifier plusieurs variables il faut utiliser des pointeurs.

Demonstration:
```c
	main() {
		int x = 7;
		int y = 4;
		int x = multiplier_par_deux(x, y);
		return 0;
	}
	int multiplier_par_deux(int n, int m) {
		n = n * 2;
		m = m * 2;
		return n;
	}
```

Seul la valeur de x est affecter, le y ne sert à rien ici.

```c
	main() {
		int x = 7;
		int y = 4;
		int* p_x = &x;
		int* p_y = &y;
		multiplier_par_deux(p_x, p_y);
		return 0;
	}

	void multiplier_par_deux(int* n, int* m) {
		*n = *n * 2;
		*m = *m * 2;
	}
```
Ici on envoie les addresses de x et de y à la fonction. La fonction elle ne connait pas x ou y mais par contre elle connait l'addresse de x et de y, qui est contenue dans la variable n et m.

Lorsqu'elle fait *n, elle prend l'addresse contenue dans n et ensuite elle l'a déréference. Elle va à l'addresse mémoire correspondent et récupère la valeur. Ensuite elle multiplie cette valeur par deux et elle la met à cette addresse mémoire la nouvelle valeur (qui aurait pu etre n'importe quoi). On fait deux opérations différentes. A gauche on assigne une valeur à l'emplacement mémoire n, à droite on obtient la valeur contenue à l'emplacement mémoire n.

Très important: n est crée au début de la fonction et est détruite à la fin, ce n'est pas la même variable que p_x, c'est une copie de celle ci qui contient la même addresse. Au début de la fonction on lui assigne la valeur (l'addresse) contenue dans p_x, ensuite grâce à cette addresse on accède à la valeur de x, puis à la fin on supprime n. L'addresse de n (et non l'addresse contenue dans n, qui est donc sa valeur) est différente de celle de p_x.

Pour accéder à leur adresse on fait:
```c
&p_x;

&n;
```

Egalement:
```c
  &p_x // permet donc d'accéder à l'adresse du pointeur (= 000EE10)
  p_x // permet d'accéder à l'adresse de la variable pointer (x) (donc la valeur du pointeur) (= 000EF17)
  *p_x // permet d'accéder à la valeur de la variable pointer (= 7)
  
  p_p_x = 000EE10; // pointeur sur pointeur (qui pointe vers un int)
  000EE10 = 000EF17;
  p_x = 000EF17;
  000EF17 = 7
```


## Concept Avancée, les pointeur sur fonction

Avec les pointeurs on peut également pointer sur une fonction, le pointeur stockera alors l'adresse d'une fonction au lieu de l'adresse d'une variable. Lorsque l'on dereferencera le pointeur on pourra alors utiliser la fonction. C'est utile lors de l'utilisation en parralèle avec les structs pour que celle-ci resemble à des classes.

Pour ce faire:
```c
	void printHello();
	void printMsg(char* msg);
	
	int main()
	{
		// initialization du pointeur sur fonction, void est le type de retour de la fonction
		// pointé vers, entre les () on met les paramètres que prend cette fonction et printH 
		// est le nom de la fonction
		void (*printH)();
		
		// on assigne la fonction printHello au pointeur printH
    	printH = &printHello;
		// on fait l'initialization et l'assignation en même temps
    	void (*printM)(char* msg) = &printMsg;

		(*printH)();
    	(*printM)("Mais comment ca va mon pote ?");

	    return 0;
	}

	void printHello() {
    	printf("Hello\n");
	}

	void printMsg(char* msg) {
    	printf("%s\n", msg);
	}
```
