
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

<u>Implémentation</u> en C : 

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

>[!info] NB : Dans un tas min, en tout noeuds les sous-arbres g et d sont des tas-min.

On va s'interesser à deux opération

```C
void up(struct tas,int i){
//Rétablie la propriété de tas min dans l'hypothèse où t est un tas min sauf éventuellemnt t.tab[i] qui peut être inférieur à son père
	int p = pere(i);
	while (p>0 && t.tab[p]>t.tab[i]{
		swap(t,i,p);
		i=p;
		p=pere(i)
	}
}
```

