##Installer Gladys

Gladys est conçue pour tourner aussi bien sur Linux, Mac ou Windows.

#### Image Raspbian

Une version de Gladys spécialement packagée sur Raspberry Pi ( une image Raspbian toute prête ) sera bientôt disponible ! En attendant, vous pouvez installer Gladys manuellement comme indiqué dans le prochain paragraphe.

#### Installation manuelle

Pour installer Gladys, il suffit de suivre les instructions sur le [GitHub du projet Gladys](https://github.com/GladysProject/Gladys).

## Programme développeur

#### Les scripts

N'importe qui peut créer un script Gladys, et le partager avec la communauté. Pour créer un script Gladys, c'est très simple: 

* Connectez-vous à Gladys, et rendez-vous à l'onglet "Scripts" du dashboard.
* Cliquez sur le menu déroulant, et sélectionner un script à éditer. ( Il y a par défaut le script "alarm.js", vous pouvez vous en inspirer pour créer d'autres scripts ). Sinon, vous pouvez cliquer sur "Nouveau script" pour créer un script.
* Ecrivez **ce que vous voulez** du moment que c'est du JavaScript dans le champs. Vous pouvez utilisez toutes les fonctions de l'API Gladys bien entendu.
* Cliquez sur "Exécuter le script" pour tester votre script. En cas d'erreur, une box apparaîtra et vous dira le message d'erreur retourné par votre script.

**API Gladys :** Pour connaître toutes les fonctions Gladys disponible, rendez vous dans le dossier `api/services`. Tous les fichiers contiennent des fonctions qui sont accessible depuis un script. Pour utiliser une fonction, appelez la fonction : `nom_du_fichier.nom_de_la_fonction()`. Par exemple, pour le fichier `api/services/SpeakService.js`, si je veux appeler la fonction `say()`, je fais de la sorte : 

```
SpeakService.say("Bonjour monsieur");
```

**Question :** Si un script plante complètement, Gladys plante aussi, c'est pas terrible tout ça non ? Est-il prévu d'isoler les scripts du coeur ?     
**Réponse :**  Tout à fait, c'est prévu ! ( dans une prochaine release ) Le problème est que Node.js est single thread, tout tourne dans le même process, du coup si un script crash, tout crash. ( même si là le script est dans une sandbox et n'a accès qu'à certaines variables mais pas à tout Gladys ). Il y a néanmoins une solution, c'est de créer un processus fils qui s'exécutera à côté de Gladys sans gêner le thread principal.
Le souci, c'est que qui dit processus fils, dit qu'il n'a pas accès aux fonctions du coeur principal de Gladys, c'est donc assez limité. Pour palier à ça, il faut créer des sortes de mini-instances de Gladys pour chaque script. C'est prévu et en cours, mais pas pour cette version, vu qu'il faut faire ça proprement pour ne pas utiliser trop de ressources car ça revient à lancer Gladys plusieurs fois, et niveau RAM ça consommera beaucoup plus qu'actuellement. Mais c'est prévu!


#### Les modules

En fait un module Gladys n'est ni plus ni moins qu'un Hooks de sails.js ( [Plus d'informations sur les Hooks](https://github.com/balderdashy/sails-docs/blob/master/concepts/extending-sails/Hooks/userhooks.md) ).

Pour vous montrer un example de Hooks, j'ai développé un "ExampleHooks" placé dans le répertoire `api/hooks`. 

Au démarrage de Gladys, ce module effectue plein d'actions :

* Les fichiers dans le dossier "assets" sont copiés dans le répertoire "assets" de l'application mère, pour pouvoir être accessible depuis l'extérieur.
* Les Models sont ajoutés aux modèles de Gladys ( pour pouvoir créer des nouvelles tables dans la base de données )
* Les controllers sont ajoutés aux controllers de Gladys
* Les services sont ajoutés aux services de Gladys et deviennent disponible partout ( même dans les scripts Gladys)
* Les fichiers de config, les policies sont injectés eux aussi à Gladys
* Les widgets de l'écran d'accueil définis dans le fichier `example/lib/parametres.js` sont injectés dans la base de donnée dans la table "DashboardBox" pour être disponible rapidement quand on charge la page d'accueil.

Imaginons que vous vouliez créer un module pour gérer vos lampes connectées, et ainsi rendre Gladys compatible avec votre modèle d'ampoule ! Je vous conseille de procéder ainsi ( c'est un exemple d'implémentation complète de lampes connectées, mais il est possible de créer des modules beaucoup plus simple ) :

* Dupliquez le dossier `api/hooks/example` pour partir d'une base de module qui fonctionne.
* Modifiez le fichier `votre_module/lib/defaults.js`, ainsi que le fichier `votre_module/lib/parametres.js` avec les différentes informations sur votre module.
* Créez un Model sails dans `votre_module/models` pour créer une table pour stocker vos périphériques.
* Créez dans un controller une API REST qui va gérer les interactions avec le client ( ajout/suppression d'un périphérique, allumage/extinction d'une lampe ).
* Créez dans le dossier `assets` un client JS ( une application Angular, ou JQuery, ou pur JS selon vos préférences ) qui va aller demander à l'API les différents périphériques controllable, les injecter dans le widget sur la page d'accueil, et gérer les cliques boutons pour allumer/éteindre les lampes. 
* Modifiez le code HTML du Widget de l'écran d'accueil en touchant au fichier `votre_module/views/box.ejs`.

Pour faire vos tests, vous pouvez directement mettre du code dans le fichier `index.js`, il sera exécuté au chargement de Gladys.
Cependant si vous voulez attendre que Gladys soit bien chargée pour avoir accès à toutes les fonctions de Gladys, placez-vous dans la fonction qui attend l'event "sailsReady" dans le fichier `index.js` :

```
sails.config.Event.on('sailsReady', function(){
     // Est exécuté quand Gladys a fini de charger 
}); 
```

Une documentation plus précise arrivera bientôt !

#### Le Gladys Store

Le Gladys Store est en cours de reconstruction pour cette nouvelle version de Gladys!