# Compte Rendu TP WebGL

BAIO David, BONNARD Guillaume, MIGUELEZ Sylvain.

## Comment faire fonctionner le projet

Avant d'ouvrir l'index dans l'explorateur, il faut ex�cuter la commande suivante sur un terminal afin d'avoir un affichage correct des textures:

    \$python3 -m http.server

Vous pouvez ensuite visualiser le projet en vous connectant au localhost.

Pour jouer, cliquer dans la zone de la piste afin de lancer la boule. Une fois toutes les quilles tomb�es, re-cliquez pour faire appara�tre la fen�tre de fin.

## Choix de la technologie

Le principe de ce TP �tait de se familiariser avec les techniques de webGL. Le projet devait contenir les fonctionnalit�s suivantes:

* Gestion de la physique
* Utilisation de mod�les 3D
* Gestion d'une cam�ra

Afin de r�aliser ce projet nous avons choisi d'utiliser le framework BabylonJS. Nous avons choisi ce framework car il g�re d�j� lui-m�me une grande partie 
des fonctionnalit�s qui devaient �tre impl�ment�es dans le projet.

## Le projet

### Pr�sentation g�n�rale

Apr�s avoir �tudi� les sp�cifications du projet, nous avons d�cid� de cr�� un petit jeu de bowling. Pour ce faire nous avons d�cid� de mod�liser la piste
par un simple plan avec une texture de piste de bowling. Les quilles sont des cylindres textur�s, stock�es sous la forme d'un tableau. On peut voir sur l'image ci-dessous
l'aspect de la zone de jeu.

![Image](./bowling.png "Magnifique image de notre projet")

Chaque texture est g�r�e s�par�ment afin de pouvoir modifier une texture en particulier assez rapidement.

### Gestion de la collision

Nous avons choisi un jeu de bowling car cela fait intervenir plusieur gestions de collision. Nous avons de la collision entre la boule et la piste, la boule et les quilles
ainsi que la boule et les barri�res sur le c�t�. Nous avons d�cid� de donner une masse � la boule 10 fois sup�rieure � la masse des quilles. Cela nous permet d'avoir un effet
plus ou moins r�aliste lorsque la boule touche les quilles. La piste, ainsi que les barri�res n'ont pas de masse mais ont un coefficient de friction afin de pouvoir ralentir
la boule lors d'un contact.

Nous avons impl�ment� un syst�me de score basique qui compte le nombre de quilles tomb�es. Un quille est consid�r�e comme tomb�e si on d�tecte une variation de la rotation de la quille
selon l'axe x ou z sup�rieure � 45 degr�s.

### Am�liorations possibles

En l'�tat, le projet est plus une vitrine de d�monstration technique qu'un v�ritable jeu.

Nous avons impl�ment� une sorte de score mais pour l'instant celui-ci ne compte que le nombre de quilles tomb�es. Nous pourrions impl�menter les v�ritables r�gles du bowling, avec
la gestion des deux manches et les coups sp�ciaux comme le strike ou le spare. Nous pourrions aussi affiner la gestion de la collision afin d'�viter que les quilles ne partent trop
vite et trop fort, ainsi qu'un syst�me de remise � z�ro des quilles.