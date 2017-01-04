##*Projet WebGL - Babylon js*

*Caroline MILLET et Maxence CHAVEROT - CPE Lyon - 5ETI*

-----
**1.Objectif**

L'Objectif de ce TP est de se familiariser avec l'API Javascript WebGL. 
WebGL permet d'afficher, de créer et de gérer de façon dynamique des environnements en 3D sur Internet. WebGL est compatible sur la plupart des navigateurs web.

Le but du projet est de créer une scène interactive 3D contenant des intéractions physiques en utilisant la technologie WebGL.

-----

**2.Réalisation de la scène intéractive 3D**

-----

*Description de la scène*

-----

Dans le cadre de ce projet, nous avons choisi de modéliser un jeu de billard intéractif. 
Les boules de billard sont initialement disposée comme dans un vrai jeu de billard. 
L'utilisateur peut cliquer sur la boule blanche afin de viser les autres boules et de les faire tomber dans les trous du billard.
La boule blanche se déplace en fonction de la position de la caméra. 
Pour viser une boule, il suffit donc de bien positionner la caméra et de cliquer ensuite sur la boule blanche afin de la lancer.

La barre espace permet de réinitialiser la position des boules de billard.

Pour réaliser cette scène, nous avons utilisé le moteur 3D temps réel Babylon.js. Ce moteur est sous forme d'une bibliothèque Javascript qui permet l'affichage d'objets 3D dans le navigateur.
La scène est créée dans la fonction createScene() dans le script javascript du ficher HTML index.html.

-----

*Creation des sphères*

-----

Les onzes sphères du billard sont créées et initialisées dans la fonction initializeSpheres().

La sphère fait partie des maillages simples disponibles dans Babylon JS.
Les sphères possèdent toutes le même diamètre et la même coordonnée y (de telle sorte à ce qu'elles soient positionnées sur la table de billard).
On leur attribue ensuite des coordonnées en x et en z afin de les positionner comme on le souhaite. 
On ajoute ensuite un matériau à nos sphères. On crée un matériau standard auquel on ajoute une texture blanche, jaune ou rouge selon la sphère considérée.

-----

*Creation de la table de billard*

-----

La création de la table de billard s'effectue dans la fonction createPoolTable().

Comme un billard est symétrique, nous créeons uniquement une barre pour la largeur et une barre pour la longueur que l'on dupliquera plus tard.
Dans un premier temps nous utilisons les mesh de type "box" disponibles dans Babylon JS.
Afin de réaliser les trous du billard, nous utilisons la méthode CSG : Constructive Solid Geometry. 
C'est à dire que nous retirons des mesh une forme de type sphère. Pour cela nous utilisons la classe CSG disponible dans le framework. 
On positionne la sphère à l'endroit ou l'on veut créer le trou, puis nous la convertissons en Mesh CSG, et enfin on utilise la méthode substract de la classe pour simuler les trous. 

Une fois que tous les trous sont réalisés, nous reconvertissons la Mesh CSG en Mesh normale avec la méthode ToMesh().
Enfin, nous dupliquons les deux barres créees avec la méthode clone().
Nous leur spécifions un matériau couleur bois afin de les rendre réalistes.

Dans un deuxième temps nous créeons le sol du billard a l'aide d'une Mesh de type Plane, auquelle nous appliquons un materiau de couleur verte pour simuler le tapis de billard.

-----

*Gestion des touches du clavier*

-----

La gestion de la touche espace s'effectue dans la fonction keyEvent().
On appelle donc notre fonction initializeSpheres() lorsque l'utilisateur appuie sur la touche espace.

Il nous reste à géré le cas où l'utilisateur clique sur la boule blanche : 
Pour cela, on utilise la fonction scene.onPointerDown = function (event, pickResult).
Dans cette fonction, lorsque l'utilisateur clique sur la sphère blanche, on calcule la direction de la caméra, puis le vecteur vitesse que l'on doit appliquer à notre sphère.
Enfin, nous appliquons une impulsion à la vitesse calculée à notre boule blanche.

-----

*Gestion de la physique*

-----

Nous commencons par activer les intéractions physiques dans notre scène en utilisant : scene.enablePhysics().

Nous ajoutons ensuite l'état physique des chacun des éléments de la scène en utilisant la fonction setPhysicsState():

Pour toutes les sphères, nous leur attribuons une masse égale à 1 et une restitution de 0.9. Plus la valeur de la restitution est grande, plus le choc de la collision est grand.
Pour que la boule finisse par s'arrêter, nous ajoutons l'attribut state.linearDamping = 0.2 afin que la vitesse de la boule diminue linéarirement. 

Pour les côtés du billard et la table de billard, nous leur attribuons une masse de 0 et une restitution de 0.9.

-----

*Lumière et caméra*

-----

Nous avons crée une caméra qui effectue une rotation autour du point de coordonnées (0,0).
On a également crée une fonction computeCameraDirection() pour caluler le vecteur directeur de l'axe de la caméra. La connaissance de ce vecteur nous permet de gérér la direction et la vitesse de l'impulsion de la sphère blanche.

Nous avons modélisé une source de lumière à l'aide d'une HemisphericLight.
var light = new BABYLON.HemisphericLight("hemi", new BABYLON.Vector3(0, 1, 0), scene);

Afin que le rendu des objets paraisse plus réaliste, nous attribuons à chacun de nos objets 3D des couleurs diffuse et spéculaire.

-----

*Affichage des instructions*

-----

On affiche les instructions dans un canvas 2D.

