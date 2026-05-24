# I)<u>Fichiers</u> :

### 1)<u>Arborescence</u> :

>[!cour] Commandes
>`pwd` -> donne le répertoire courant
>`cd` -> permet de changer de répertoire
>`mkdir` -> créer un nouveau dossier
>`ls` -> donne le contenu d'un dossier

### 2)<u>Inodes</u> :

>[!cour] Définitions
>L'inode (ou nœud d'index) est un numéro qui permet d'identifier de façon unique chaque fichier (ou répertoire).
>Le système d'exploitation gère une table des inodes dans laquelle, à chaque inode sont associés : les <font color = "red"><u>métadonnées</u></font> du fichier 
> - son type (fichier ordinaire, repertoire, lien ou autre)
> - date de dernière modification
> - propriétaire du fichier
> - droits sur le fichier
> - adresse physique de contenu sur le disque.

>[!bug] Commande
>``` Linux
>ls -l -i
>```
>`-i` : pour afficher l'inode

>[!cour]  
>Le nom du fichier n'est pas stockée dans les métadonnées mais dans le répertoire qui contient le fichier.
>Un répertoire est un fichier, qui contient une liste de couples $(nom,inode)$.
>
>On peut ainsi associer plusieurs noms à un même fichier (inode).

>[!bug] Commande
>La commande <font color = "red">ln</font> (pour "link") permet de créer un lien phyqsique entre deux "fichiers"

>[!example] Par exemple
>`$ ln A/fichier1.txt fichier2.txt`
>
>`fichier1.txt` : nouveau nom
>`fichier2.txt` : nom sous lequel le fichier est déjà connu
>
>On dispose de deux noms (ici à deux emplacements différents <font color =  "green">(répertoire A et répertoire courant)</font>) qui renvoient au même ficher sur le disque (même inode).
><font color = "cyan">On peut modifier le ficher en utilisant indiférenement l'un ou l'autre nom</font>, en revanche, le ficher ne sera supprimé définitivement que lorsque tous les liens  physiques aurait été supprimés.
>
>On peut aussi créer des <font color = "red"><u>liens symboliques</u></font> qui sont de simples raccourcis 
>`$ ln -s A C`
>`C` est un raccourcis pour le chemin `A`

# II)<u>Flux standard</u> :

>[!cour] 
>Un <font color = "red"><u>flux de données</u></font> est une suite de données qu'il faut manipuler.
>Typiquement, on distingue, lors de l'exécution d'un <font color = "red"><u>processus</u></font> (un processus est un instance d'exécution d'un certain programme), 3 flux de données :
> - entrée standard : communication de l'extérieur vers le processus (<u>ex</u>: saisie au clavier)
> - sortie standard : communication du processus vers l'extérieur (<u>ex</u>: le terminal)
> - sortie erreur standard : communication du processus vers l'extérieur mais pour les erreurs.

>[!example] exemples de terminal
> `ls` renvoie sa sortie sur la sortie standard
> `ls` avec un argument erroné renvoie sa sortie sur la sortie erreur standard
> 
> On peut rediriger les 3 flux :
> $$ \begin{cases}
 \text{> pour rediriger la sortie standard} \\
 \text{2> pour rediriger la sortie erreur standard} \\
< \text{pour rediriger l'entrée}
\end{cases} \text{   /// suivi du chemin valide vers un fichier}$$

>[!important] Remarque 
>`>` `2>` écrasent le fichier s'il existe, le créer sinon
>Utiliser `>>` `2>>` pour ajouter à la fin du fichier sans écraser.
>On peut aussi transférer la sortie d'une commande à l'entrée d'une autre : opérateur `|` ("pipe")

>[!implementation] Exemple en C
>`printf` affiche sur la sortie standard par défaut.
>- spécification de format 
>> `%d` : entiers 
>>`%c` : caractères
>>`%s` : chaînes
>>`%f` : flottants
>>`%p` : pointeur

>[!warning] Le flux de sortie s'accumule dans le $buffer$ (mémoire tampon) qui n'est vidé qu'en certaines occasions : 
> - lorsqu'il y a un retour à la ligne
> - lorsque le "cache" (le buffer) est plein
> - lorsqu'il y a une lecture à faire sur l'entrée standard
> 
><font color = "cyan">L'objectif étant de gagner du temps, car l'accès à la sortie (console ou fichier) prend du temps </font>

>[!cour]
>Pour rediriger la sortie, on peut utiliser `fprintf(FILE *stream, const char* for mat, ...)`
>`fprintf` : printf vers `*`
> - Le premier argument désigne le flux à utiliser
> - les arguments sont les mêmes que pour `printf`
> 
>□ pou la lecture sur l'entrée standard :
>$$scanf(\underbrace{\text{const char* format}}_{\text{chaîne avec spécificateurs}},\underbrace{\text{...................................................................}}_{\text{adresse où écrire les valeurs coresspondant aux spécificateurs}})$$

>[!example] 
>``` C
>char c;
>scanf(" %c",&c);
>```
>l'espace au début de scanf aura pour effet d'ignorer les espaces ou retour à la ligne qui précèderont le caractère
>
>Si on utilise le spécificateur `%s` la lecture s'arrête au $1^{er}$ rerour à la ligne et `'\O'` est ajouté 

>[!warning] 
>Il faut qu'il y ait suffisamment de place à l'adresse spécifique pour écrire les données.
>>[!example] 
>>`char s[50]` pour lire une chaîne d'au plus 50 carectères

>[!cour] 
>Il existe aussi `fsanf` pour lire depuis un fichier

>[!cour]
>□ <u>En OCaml</u> :
>`printf`, `print_float`,`print_string`,`print_newline` pour écrire sur la sortie standard
>
>Lecture sur l'entrée standard :
>`read_int`, `read_float`, `read_line`[^1]

# III)<u>Fichier texte</u> :

>[!cour]
>Pour lire ou écrire dans un ficher texte, on doit interagir avec le système d'exploitation :
> - on demande l'accès au fichier, en lecture ou en écriture (ou en ajout) : on obtient un descripteur de ficher, avec toutes les informations utiles pour gérer l'accès au fichier;
> - on écrit ou on lit dans le ficher $(2)$
> - lorsque les opérations sont terminées, on demande la fermeture de l'accès au fichier (important pour que les données ne soient corrompues et pour libérer la ressource pour les autres utilisateurs).

>[!important] Remarque 
>ces opérations implique en $(2)$ une gestion des flux de données pour l'OS

>[!implementation] En C
> Pour obtenir l'accès à un fichier
> $\underbrace{\text{FILE *}}_{\text{pointeur structure de descripetur de ficher}} \text{fopen(}\underbrace{\text{const char * pathname}}_{\text{chemin vers le ficher (chaîne)}}, \underbrace{\text{ const char * mode}}_{\text{mode d'accès "w" ou "r" ou "a"}});$
> 
>>[!warning] 
>>La fonction `fopen` renvoie `NULL` si on ne dispose pas des bons droits sur le fichier (à vérifier donc)
>><font color = "red"><u>Il faudra teste aux concours</u></font>
>

>[!cour] Utilisation
>``` C
>int main (){
>	FILE * f = fopen(....);
>	....
>}
>```
>pour lire dans un fichier :
>`fscanf(f, "%d %d",&a,&b)`
>>`"%d %d"` : pour lire une ligne dans un fichier dont chaque ligne contient deux entrées séparés par un espace
>
>pour fermer l'accès au fichier :
>`fclose (FILE * stream)`

>[!tip] Rappel
>lecture de paramètre sur l'entrée au moment de l'exécution `./myprog ~ ~` 
>```C
>int maint(int argc, char* argv[]){...}
>```
>`argc` prendra pour valeur le nomnbre d'arguments sur la ligne de commande (nom du programme inclus).
>`argv` tableau de chaîne de caractères qui contient `argc` cellule une paramètre (en position 0 : le nom du programme).


[^1]: lit jusqu'au premier retour à la ligne.
---
#Informatique #cours