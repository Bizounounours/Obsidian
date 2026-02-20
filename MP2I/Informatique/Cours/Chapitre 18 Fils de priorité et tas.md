
## I) Tas 

### 1) Définition : tas min

Un tas min est un arbre binaire complet à gauche tel que l'étiquette de tout noeud interne est inférieur ou égale à celle de ses fils 

<u>Remarque</u> : on définit de même les tas_max 

On a donc la possibilité de le rprésenter en stockant son parcours en largeur dans un tableau 


```handdrawn-ink
{
	"versionAtEmbed": "0.3.4",
	"filepath": "Ink/Drawing/2026.2.13 - 9.47am.drawing",
	"width": 480,
	"aspectRatio": 2.981366459627329
}
```

##### <u>Implémentation</u> en C : 

```C
struct tas{
	int * tab; //valeurs dans le tas
	int capacity; //nb de cases alloués
}
```

```C
int fils_gauche(int i){
	return 2*i;
}

int fils_droite(int i){
	return 2*i +1;
}

int pere(int i){
	return i/2;
}
```

```C
void swap(struct tas t, int i, int j){
int temp = t.tab[i];
t.tab[i]=t.tab[j];
t.tab[j]=temp;
}
```

## II) Opérations sur les tas min 

>[!note] NB : Dans un tas min, en tout noeuds les sous-arbres g et d sont des tas-min.

On va s'interesser à deux opération

```C
void up(struct tas t,int i){
//Rétablie la propriété de tas min dans l'hypothèse où t est un tas min sauf éventuellemnt t.tab[i] qui peut être inférieur à son père à ceci près la structure de tas min doit être respecté càd 
	int p = pere(i);
	while (p>0 && t.tab[p]>t.tab[i]){
		swap(t,i,p);
		i=p;
		p=pere(i);
	}
}
```

`p > 0` : vérifier que i n'est pas à la racine
`t.tab[p]>t.tab[i]` : on vérifie s'il faut inverser pere et fils
`i = p; p = pere(i);`  Prépartion de l'itération suivante (éventuelle)

<mark style="background: #00688F;"><u>Complexité</u></mark> : le nombre d'itérations est au plus égale à la profondeur de noeud i. donc la complexité est en $\log_2(i)$ (majoré par $O(h)$)

```C
void down(struct tas t, int i){
//Rétablit la propriété de tas min dans l'hypothèse où t est un tas min sauf éventuellement au noeud i, qui peut être supérieur à l'un de ses fils.
	int taille = t.tab[0];
	while (i<taille){
		int gauche = fils_gauche(i);
		int droit = fils_droit(i);
		int min_Index = i;
		//si le fg existe et est pmus petit que le plus petit déja trouvé
//trouvé (ici i)
		if (gauche <= taille && t.tab[gauche]<t.tab[minIndex]){
			minIndex = gauche;
		}
		// idem à droite
		if (droit <= taille && t.tab[droit] < t.tab[minIndex]){
			minIndex = droit;
		}
		// si le plus petit est à la racine : on arrête
		if (minIndex == i) return ;
		// sinon on échange i avec le plus petit.
		swap(t, i, minIndex);
		//préparation de l'itération suivante (suite éventuelle de la descente)
		i = minIndex;
	}
}
```



### 3)<u>Extraire le min</u> :

Principe :
 - le min est à prendre à la racine
 - on rétablit le tas en plaçant à la racine la dernière feuille (pour être dans un cas d'application de down)

```C
int extraire_min (struct tas t){
	int taille = t.tab[0];
	int min = t.tab[1];
	t.tab[1] = t.tab[taille];
	t.tab[0] = taille - 1;
	down(t,1);
	return min;
}
```

### 4)<u>Ajouter un élément</u> :

>[!info] Def/info
>On ajoute en dernière position ($\text{taille} + 1$) (préserve la structure d'arbre complet)
>On applique `up` (préserver la structure de tas)
>Actualiser la taille càd `t.tab[0]` (* ajouter 1)

### 5)<u>Mettre à jour un élément</u> :

>[!info] Def/info
><u>Càd</u> changer la valeur en position `i` 
>On change la valeur : 
> - si la nouvelle valeur est plus grande : on appelle `down`.
> - si la nouvelle valeur est plus petite : on appelle `up`.


#### Insertion

```C
void inserer (struct tas t, int val){
	assert(t.capacity>t.tab[0]+1);
	int taille = t.tab[0]+1;
	t.tab[0] = taille;
	t.tab[taille]=val;
	up(t,taille);
}
```

#### Màj d'un élément

```c
void maj(struct tas t, int i, int val){
	int ancien = t.tab[i];
	t.tab[i] = val;
	if(val > ancien){
		down(t,i);
	}
	else {
		up(t,i)
	}
}
```


## III) Création d'un tas à partir d'un tableau:

### 1) Par insertions successives

```C
struct tas init(int* tab, int taille){
	struct tas t;
	t.capacity =  taille + 1 
	t.tab = malloc((t.capacity)*sizeof(int));
	t.tab[0] = 0
	for(int i =0; i<taille; i++){
		inserer(t,tab[i]) /*Préconditions: que le tableau t.tab soit de taille 
		suffisnate pour aceuillir la valeur tab[i]*/ 
	}
	return t; //On renvoie une copie de la structure crée
}
```

Compléxité : 
$$
O(1)+\sum^{h}_{k=0}O(k)\underbrace{ 2^k}_{\text{nombre de noeud à la profondeur k}}
$$
### 2) Deuxieme façon

```C
struct tas init(int* tab, int taille){
	struct tas t; 
	t.capacity = taille + 1
	t.tab = malloc((t.capacity)*sizeof(int));
	t.tab[0] = taille;
	//recopie du tableau
	for(int i=0; i<taille; i++){
		t.tab[i+1]=tab[i];
	}
	//
	for(int i=taille/2;i>0;i--){
		down(t,i);
	}
	return t;
}
```



hrejgjr
ijfezlkjl
jkzjfzjekjhehpzzpam;s
skmmasls;a