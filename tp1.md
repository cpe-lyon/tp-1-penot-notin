# Exercice 1
Apres installation, pour se connecter en shh sur une vm local, il faut ouvrir une invite de commande (Windows ou Linux) : 
```
ssh -p 2222 tp@localhost
``` 

# Exercice 2
- which :
    > Retourne  le  chemin  des  fichiers  qui seraient exécutés dans
    l'environnement courant si ses arguments avaient été donnés comme  com‐
    mandes  dans un interpréteur de commandes strictement conforme à POSIX.
    Pour ce faire, which cherche dans la variable PATH les fichiers  exécu‐
    tables  correspondants aux noms des arguments. which ne déréférence pas
    les liens symboliques.

    Exemple :
    ```
    which cp
    /bin/cp
    ```
Il est possible de rechercher dans le man en appuyant sur ___"/"___ . Il faut ensuite entré un ___"paterne"___ qui sera chercher sur le man. Il faut ensuite appuyer sur ___"n"___  et ___"shift + n"___ pour passer parcourir les résultats.  

On quitte ensuit en appuyant sur __"q"__.  

Pour afficher la première page de la section 6 il faut taper : ```man 6 intro```. On va retrouver une description de la section. 

## Commandes de déplacements : 
```
  cd /var/log/
  cd ..
  cd ~
  cd -
```
Si on essaie de faire un `cd /root` on obient un message qui nous indique que l'on a pas les permissions. La commande `sudo cd /root` nous retounrne le message : `sudo: cd: command not found`. En effet, lorsque l'on fait cd avec un sudo cela ne fonctionne pas, la commande cd c'est pas compatible avec la commande sudo. Il est aussi possible lorsque l'on utilise une commande valide mais ne pas disposer des droits sudo avec le compte.

Pour supprimer Dossier1 et Fichier1 : 
```
cd ~
rm /Dossier1/Fichier1
rm /Dossier1
```
La dernière commande retourne une erreur, `rm: cannot remove 'Dossier1'`. Pour supprimer un fichier, il faut rajouter `-d`, ce qui donne : 
```
rm -d /Dossier1
```
Lorsque l'on fait ca sur Dossier2, on a une erreur car le dossier deux n'es pas vide. Pour régler se prolème il faut faire : 
```
rm -r Dossier2
```
Cette commande va supprimer tous ce qu'il y a dans le dossier recursivement (fichiers et dossiers)

## Commande Important

Pour afficher l'heure il faut taper : `date`.  
La commande time permet de sortir le temps d'execution de la commande passer en argument (le temps entre le lancement du processus et son arret). Exemple : 
```
time mkdir toto

real	0m0.003s
user	0m0.000s
sys	0m0.000s

time man man

real	0m4.154s
user	0m0.052s
sys	0m0.020s
```
Les fichiers avec .nomDuFichier ne s'affichent pas avec la commande ls, mais avec la commande la ils s'affichent. Le sfichiers commencant par . sont des fichiers cachés  
Avec la fonction `which ls`, on voit que ls se trouve dans `/usr/bin/ls`.  
ll et la n'existent pas, se sont des alias. Par exemple avec la commande alias permet de fair en fait `ls -alF`  
Pour afficher les fichier dans un dossier il faut faire ajouter ___"-f"___ : 
```
ls -f /bin
```
la commande `ls ..` va lister les fichiers et dossiers contenus dans le dossier parent.  
Pour afficher le chemin complet du dossier courant il faut faire : `pwd`
La commande `echo "text"` va afficher le text sur la sortie standard. On a deux possibilités si on veut les mettres dans un fichier : 
```
echo "text" > toto
echo "text" >> toto
```
Si le fichier toto n'existe pas, il sera créer dans les deux cas. Pour le premier on va remplacer le contenu, pour le second on va ajouter en fin de ligne.  
La commande file va permettre d'indiquer l'encodage du text présent dans un fichier. Si le fichier est vide cela est indiqué  
Si on créer un fichier a l'aide de ces commandes :
```
echo "Hello Toto !" > toto
ln toto titi
cat titi
    Hello Toto !
echo "la" >> toto
cat titi
    Hello Toto !
    la
rm toto
cat titi
    Hello Toto !
    la
```
Lorsque l'on modifier toto titi est modifier aussi, si on supprime toto, titi reste.
Si on remplace ln toto titi par ln -s toto titi, le comportement est le même sauf que avec un lien symbolique, titi n'es plus accessible.  
Pour afficher le contenu d'un fichier, il faut faire `cat nomduFichier`. Pour arreter un défilement il faut faire `ctrl + c`.  
La commande `head nomDuFichier` permet d'afficher le s10 preière lignes, `tail nomDuFichier` permet d'afficher les 15 dernière lignes. Pour afficher de la ligne 10 a 20 on fait `sed -n '10,20p' nomDuFichier`.  
La commande `dmesg | less` permet d'afficher les messages renvoyer par le system, et de les paginer avec less. Less fonctionne comme more mais est plus rapide, il affiche le text sans formatage par exemple.  
le fichier `/etc/passwd` contient tout les mots de passe chiffrer des users de la machine. La page du man de se fichier va afficher son contenu : `man /etc/passwd`. La commande `man passwd` permet de modifier se fichier.  
La commande qui permet d'afficher la premire colonne de se fichier est : 
```
cut -d: -f1 fichier
```
On peut trier avec sort -r dans l'ordre inverse de l'ordre alphabetique.  
Pour compter le nombre d'utilisateur il suffit de compter le nombre de ligne du retour de la commande précédente, avec `wc -l`.  
On peut chercher le nombre de ___page de description___ de man qui contiennent un mot clé avec la commande : `man -k motClef | wc -l`  
Pour la commande find, pour trouver un fichier avec un nom défini on fait : `find -name nomDuFichier`. Pour gérer les erreurs et fichiers trouvés et les renvoyés dans des fichiers définits : 
```
find -name nomDuFichier > ~/list_passwd_files.txt 2> /dev/null
``` 
locate permet de trouver un fichier avec son nom.
