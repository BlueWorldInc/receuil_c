# Les réfences, une histoire compliqué

Cela fait bientôt un an que j'ai du débuté l'avanture C++ et il y a une notion que je maitrise à peine qui est la notion de références. Ayant maitrisé le C avant le C++, je connaisser déjà la notion de pointeur et de ce fait je ne comprennais pas trop l'utilité de la référence. Je vais tenter d'expliquer dans cette article l'utilisation et son utilité, par rapport aux pointeurs.

## L'utilisation des références

Lors de la création de variable:
```c
	int prix_chaussure = 70;
	int& ref_prix_chaussure = prix_chaussure;
```

Alors ref_prix_chaussure devient un alias de prix_chaussure.
Les deux noms de variables désigne (référencent) la même chose.
Dans ce cas la c'est pas très utile. 

Lors de la création de fonction:
```c
	void multiply_by_two(int& n) {
		n = n * 2;
	}
	int prix_chaussure = 70;
	multiply_by_two(prix_chaussure);
	(prix_chaussure == 140) // true;
```

Ici la fonction multiply_by_two ne va pas faire une copie de la variable qu'on lui donne en paramètre mais utilise directement cette variable pour faire les opérations.
De ce fait à la fin la variable est bien modifier, ce n'est pas une copie de celle ci qui est modifier.
Le compilateur faire cette opération soit en "transformant" la référence en pointeur, soit en agissant directement à l'adresse mémoire de la variable.

Dans tout les cas cette opération permet de dire au compilateur: "ne crée pas de copie de la variable en paramètre mais agit directement dessus". Après le compilateur se débrouille pour faire cela. Soit il remplace par des pointeurs (comme on le ferait manuellement en C), soit il agit directement sur l'emplacement mémoire de la variable si il l'a connait déjà. 

Ce qui revient au même, c'est juste que dans le premier cas il fait une opération en plus (l'opération que nous deviont faire en C).
Toute les fois ou l'on écrira la variable en paramètre dans la fonction, sa sera l'adresse en mémoire de celui-ci qui sera "affecté". On modifie directement la variable et non une copie de celle ci.


## A savoir:

Il faut également savoir que la référence ne pas pas etre null et doit avoir une valeur à son initialisation. Egalement on ne peut pas changer la variable vers lequel refère une réfèrence.

## L'avantage de cette méthode:

C'est avant tout une question de syntaxe, au lieu d'avoir à ce soucier de crée un pointeur et d'envoyer l'adresse de la variable sous jacente en paramètre d'une fonction,  et de dire à la fonction: tu va recevoir "un pointeur sur int" en paramètre. On dit plutôt à la fonction: "hey mec, tu vois les variables que tu recoit en paramètre ne crée pas de copie, agit directement dessus." Du coup le programmeur n'a pas à crée de pointeur et d'envoyer l'adresse en paramètre, il donne seulement la variable et la fonction agit sur la variable (donc à l'adresse de cette variable).

En clair c'est comme si c'était un raccourcie. On délégue notre boulot à la fonction en lui donnant l'instruction à la création de celle ci (dans la signature).
La deuxième utilité, d'après ce que j'ai lu, c'est que ca permet au compilateur de faire des optimisations. Car il sait qu'une référence ne peut avoir qu'une seul variable sous jacente et ne peut etre null, contrairement à un pointeur.

Source: 

-https://openclassrooms.com/fr/courses/1421911-du-c-au-c/1422263-nouveautes-pour-les-variables

-https://stackoverflow.com/a/101406
