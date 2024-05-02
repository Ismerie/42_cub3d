# 42_cub3d
42_cub3d est un projet de l'école 42 dans lequel nous devons créer une représentation graphique 3D d'un labyrinthe en utilisant une vue à la première personne. Nous devons implémenter le raycasting dans le style du célèbre jeu [Wolfenstein 3D game](http://users.atw.hu/wolf3d/).  
Ce projet a été réalisé avec [@ThibautCharpentier](https://github.com/ThibautCharpentier)

## 📋 Règles

### 🗺️Carte
Le programme lit un fichier, la carte du jeu, qui lui sera passé en paramètre.  
Vous pouvez créer n'importe quelle carte mais elle doit respecter certaines règles :
 * L'extension du fichier doit être `.cub`
 * Les textures pour chaque orientations doivent être précisés **(NO, SO, WE, EA, F, C)**
 * La couleur en RVB (0, 255) doit etre précisé pour le sol **(F)** et le plafond **(C)**
 * Tous les bords de la carte doivent être entouré de mur **(1)**
 * Il doit y avoir 1 points cardinal dans la carte qui est la position et l'orientation du joueur au début **(N, S, W, E)**
 * Il peut y avoir des espaces vide ' ' dans la carte
 * Caractères autorisés :

| Caractère  | Objet  | Précision                                                                                 |
| ---------- | ------ | ----------------------------------------------------------------------------------------- |
| 1          | Mur    | Case infranchissable par le joueur                                                        |
| 0          | Vide   | Case sur laquelle peut se déplacer le joueur                                              |
| 2          | Porte  | Case qui peut être ouverte et traversée par le joueur (seulement pour la partie ✨bonus) |
| N          | Nord   | Position de départ et orientation cardinale **Nord** du joueur                            |
| S          | Sud    | Position de départ et orientation cardinale **Sud** du joueur                             |
| W          | Ouest  | Position de départ et orientation cardinale **Oues**t du joueur                           |
| E          | Est    | Position de départ et orientation cardinale **Est** du joueur                             |

Il y a des exemples de cartes dans le dossier ***map***

### ⌨️ Contrôles
* Les touches **W**, **A**, **S**, **D** (qwerty) ou **Z**, **Q**, **S**, **D** (azerty) servent à déplacer le point de vue du joueur
* Les touches fléchées gauche ⬅️ et droite ➡️ font pivoter le point de vue dans le labyrinthe
* La touche **ESC** ferme la fenêtre et quitte le programme

### ✨Bonus
* Des portes **(2)** qui peuvent être ouvertes
* Mini-carte qui s'affiche en haut à droite sur l'écran
* Faire pivoter le point de vue avec la souris

<img src="https://github.com/Ismerie/42_cub3d/blob/main/gif/preview_cub3d2.gif" width="480" />  <img src="https://github.com/Ismerie/42_cub3d/blob/main/gif/preview_cub3d.gif" width="480" />

## 🛠️ Usage
Avant d'exécuter le projet, vous devez configurer votre MinilibX (c'est notre bibliothèque graphique). Vous trouverez ici tout ce dont vous avez besoin pour faire fonctionner la bibliothèque selon votre OS <https://harm-smits.github.io/42docs/libs/minilibx/getting_started.html#installation>.

Si vous utilisez ***libmlx***, assurez-vous que MinilibX fonctionne en exécutant un test. Utilisez make ```libmlx``` puis exécutez le le test avec :
```
./libmlx/test/run_tests.sh
```

Si le test fonctionne, faites maintenant attention aux lignes suivantes dans le Makefifle :
```
INCLUDE_HOME = -Ilibft -I/usr/include -Ilibmlx
LES_LIBS_HOME = -Llibft -lft -Llibmlx -lmlx -L/usr/lib -lXext -lX11 -lm -lz

INCLUDE_42 = -Ilibft -Ilibmlx_mac
LES_LIBS_42 = -Llibft -lft -Llibmlx_mac -lmlx -framework OpenGL -framework AppKit
```
Vous devez choisir la bonne configuration en fonction de la structure de votre système et de votre OS. Je vous recommande de suivre le lien que je vous ai fourni ci-dessus. Si vous utilisez ***libmlx***, le droit ```-I/usr/*/include``` et ```-L/usr/*/lib``` doit correspondre à la première ligne ```INC=/usr/*/include``` du ```libmlx/Makefile.gen``` fichier.  
Sinon si vous utilisez **libmlx_mac**, vous devez modifier le paramètre LIBMLX avec cette ligne ```LIBMLX = libmlx_mac```.

Si tout semble correct, utilisez la commande ```make``` pour compiler le projet puis exécutez le programme avec :
```
./cub3d map/map.cub
```

Pour exécuter la partie bonus, utilisez la commande ```make bonus``` et exécutez le programme bonus avec :
```
./cub3d_bonus Map/map_bonus.ber
```
Si vous avez un clavier **QWERTY**, vous pouvez modifier les touches dans ```srcs/cub3d.h``` et dans ```srcs/cub3d_bonus.h```  
Vous pouvez également modifier les paramètres **MOVESPEED** ou **ROTSPEED** si votre jeu est trop lent ou trop rapide.
