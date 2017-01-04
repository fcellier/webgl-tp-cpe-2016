<p></p>
<h1>COMPTE RENDU PROJET WEB GL</h1>
<p></p>
<h2>	1 . Fonctionnement</h2>
<p></p>
<p>L objectif  de  ce  projet  était  de  modéliser  une  boule  qui  se  déplace  dans  un  labyrinthe.  </p>
<p>Le  déplacement  de  la boule se fait à l aide des touches directionnelles. </p>
<p>Il est possible de changer l angle de la caméra pour voir où se déplacer dans le labyrinthe. </p>
<p>Pour ce faire, il suffit de cliquer à l aide de la souris.</p>
<p></p>
<h2>	2 . Explication</h2>
<p></p>
<h3>CREATION DE LA BOULE</h3>
<p></p>
<p>Notre  boule  est  crée  simplement  à  partir  d'un  simple  sphère  sur  laquelle  nous </p>
<p>avons  ajouté  une texture et une illumination.</p>
<p></p>
<h3>CREATION DU LABYRINTHE</h3>
<p></p>
<p>Apres différents essais infructueux qui auraient permis d'importer directer un labyrinthe en format .obj ou format .babylon, </p>
<p>nous avons décidé de créer notre propre labyrinthe à l aide de plusieurs boxes.</p>
<p>Ainsi, la gestion des collisions se fera au cas par cas selon les boxes rencontrées et l'angle de la caméra.</p>
<p>sous lequel est vu le labyrinthe.</p>
<p></p>
<h3>GESTION DES DEPLACEMENTS DE LA BOULES</h3>
<p></p>
<p>Nos  déplacements  se  font  selon  les  flèches  haut,  bas,  droite,  gauche.  Le  deplacement (translation)</p>
<p>et  l'effet  de  roulement  (rotation)  se  font  selon  la  composante  du  temps.  Cette composante  </p>
<p>est  essentiel  afin  de  prendre  en  considération  le  temps  que  la  touche  est  enfoncée.  </p>
<p>Si on  omet  cette  dernière,  notre  boule  tournera  qu'une  seule  fois  puis  se  déplacera  uniquement  </p>
<p>par rotation.Pour éviter l'effet de "patinage" nous faisons varier le temps entre 30 et 40.</p>
<p></p>
<h3>GESTION DE LA CAMERA</h3>
<p></p>
<p>Notre caméra est une follow caméra que nous avons attaché à l'objet sphère, </p>
<p>c'est à dire la boule. Cela permet à l'utilisateur de suivre la boule en même temps que cette dernière se déplace. </p> 
<p>Nous nous sommes rapidement heurter  à un problème : vouloir regarder autour de notre boule.</p> 
<p>Une solution est de switcher entre deux camera : la free lorsqu'on se déplace avec la souris et la follow lorsqu'on se déplace. </p>
<p>Toutefois, cela nécessite de activer/désactiver les deux caméras.  Nous  avons  décidé  finalement  de  </p>
<p>réaliser  une  rotation  de  90  °  lorsque  l'on  clique  sur  la  souris  pour permettre  au  joueur  de  </p>
<p>revenir  sur  ses  pas  et  ainsi  de  mieux  coller  avec  l'idée  de  notre  jeux  :  chercher  une sortie, </p>
<p>se perdre et remonter ses pas.</p>
<p></p>
<h3>GESTION DES COLLISIONS</h3>
<p></p>
<p>Pour la gestion des collisions, nous enregistrons au fur et a mesure la derniere touche appuyee par l utilisateur. Ceci nous permettra de </p>
<p>determiner le cote du mur ou il y a eu collision. Tant qu aucune collision entre la sphere et les murs n a ete enregistre, on peut</p>
<p>faire tous les deplacements. Par contre, si une collision est detectee, on regarde la derniere touche appuyee par lÕutilisateur. </p>
<p>Exemple : Si il y a eu collision sur un mur et que la derniere touche appuyee est la gauche alors on a touche le mur sur la droite donc la</p>
<p>sphere peut faire tous les deplacements sauf celui d aller a gauche. Et on reitere pour chaque touche.</p>
<p></p>
<h2>	3 . INTERETS ET BESOINS ADRESSES</h2>
<p></p>
<h3>INTERET DE LA ROTATION</h3>
<p></p>
<p>Lorsque  nous  avons  géré  les  déplacements  de  la  boule,  nous  avons  vu  que  cette  dernière  </p>
<p>ne  subit qu'une  simple  translation.  Par  soucis  de  réalisme,  nous  avons  également  ajouté  </p>
<p>une  rotation  selon  la  bonne coordonnée dans le même temps.</p>
<p></p>
<h3>CHOIX DES COLLISIONS</h3>
<p></p>
<p>Il existe différentes approches pour réaliser la collisions :  </p>
<p>	-Point d'intersection  </p>
<p>	-Box de collisions</p>
<p></p>
<p>Nous avons choisi la box de collisions car les murs de notre labyrinthe sont des boxs. Par ailleurs, nous avons pense a deux methodes pour bien gerer nos collisions.</p>
<p>Soit :</p>
<p>	- enregistrer la derniere direction de la sphere afin de determiner sur quelle face du mur il y a eu collision.</p>
<p>	- realiser un rebond lors d une collision.</p>
<p>La derniere solution n a pas ete retenu car il aurait fallu faire bon nombre de calculs, dont l epaisseur du mur et recuperer la position du centre de la sphere. </p>
