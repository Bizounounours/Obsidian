
Complexité 
- Tester si la liste est vide : O(1)
- taille de la liste O(n)
- Ajouter / supprimer un élément O(i) tel que O(1)<=O(i)<=O(n) depent de la position dans la liste 
- Concatenation 










Ce type implemente des tableux de taille fixe















fgryzmd:



taille max 


note l'elemeent pile 


typedef struct maillon{
	int elem;
	struct maillon * suivant
}maillon_t

depiler pile_t




**<mark style="background: #ABF7F7A6;">IV \ Files</mark>**

Fonctionnement de type FIFO

	First In, First Out
premier entré, premier sorti
C'est le fonctionnement de la file d'attente 

/!\ 
-Les éléments s'ajoute ou se retire un par un
-Une file s'initialise toujours par une file vide

/!\ 
-Pas de parcours d'éléments avec *For*
-Pas d'acces a l'aide la position 
-Pas d'indice de position

<mark style="background: #FFB8EBA6;">->on remplace par *while*</mark>

Exemple
f0 : 4->3->2->1

```C
typedef struct maillon{
	int elem;
	struct maillon * suiv;
}maillon_t
```

```C
typedef struct file{
	maillon_t * tete;
	maillon_t * queue;
	int nb_elem; //facultatif
}file_t 
```

On définit une fonction par chacune des quatres opérations élémentaires du type abstrait de file
On appelle ces fonction les <mark style="background: #FFF3A3A6;">PRIMITIVES</mark> du modele de file 

 ```C
 file_t* file_vide(){
	 file_t* f = malloc(sizeof(file_t))
	 f->tete = NULL;
	 f->queue = NULL;
	 f->nb_elem = 0;
 }
 
 bool est_vide(file_t* f){
	 return f->nb_elem==0;
	 //OU
	 return (f->tete==NULL) && (f->queue==NULL);
 }
 ```

```C
void enfiler(file_t* f, int val){
	maillon_t* anc_q = f->queue; //sauvegarde de l'ancienne queue 
	maillon_t* nouv_q = malloc(sizeof(maillon_t)); //reserver la place pour le nouveau maillon qui contientra la valeur à ajouter
	nouv_q->elem = val;
	nouv_q-> suivant = NULL;
	f->queue=nouv_q; //On demande de la place ne mémoire pour y ecrire 2 pointeurs (64bits Chacun)
	f->nb_elem++;
	if (anc_q==NULL){ //si la file etait précédemment vide
		f->tete = nouv_q;
	}
	else{
	anc_q->suivant=nouv_q;
	}
}
```

```C
int defiler(file_t* f){
	assert(! est_vide(f));
	maillon_t* anc_tete = f->tete;
	int res = anc_tete->elem; //Copie de la valeur a défiler
	maillon_t nouv_tete = anc_tete->suivant;
	f->nb_elem = --;
	f->tete = nouv_tete;
	if(est-vide(f)){
		f->queue = NULL;
	}
	free(anc_tete);
	return res;
}
```

<mark style="background: #ABF7F7A6;">V \ Tableaux redimensionnable</mark>










en C






















