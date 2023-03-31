# TROUBLESHOOTING DE RÉSEAU/SYSTÈME

## 1. Généralités

- Éliminer un ou plusieurs problèmes par un processus de recherche
	- Réfléchi
	- Intelligent
	- Logique

1) Identifie le(s) problèmes(s)
2) Rechercher la ou les causes probables (*doit ensuite être documenté*)
3) On tente de les résoudre

**La documentation doit être initié dès la conception du réseau **

### Pour faire un BON troubleshooting efficace :

- Établir une documentation
- Maitriser/connaître son architecture 
	- Topologie du réseau
	- Les Applicatifs
	- La configuration-

- Avoir la main sur la configuration et savoir l'effectuer
- Utiliser la bonne approche

## 2. Troubleshooting Structuré

- Définir le problème
- Collecter un maximum d'information !
- Analyse les données collectées _(il faut bien connaître l'aspect théorique des protocoles)_
	- Éliminer des variables
- Émettre des hypothèses
- Tester les hypothèses

### A) L'approche TOP-DOWN du Modèle OSI :

	7 Application	- 	HTTP,HTTPS, etc...
	6 Presentation	- 	Système d'exploitation
	5 Session	-	protocole Connecté/Déconnecté
	4 Transport	- 	Pare-feu - TCP/UDP
	3 Réseau	-	Routeur, Switch Manageable - IP
	2 Liaison	-	Switch - Ethernet, ARP
	1 Physique 	-	Carte Réseau + Câbles - Binaire  
 
### B) L'approche BOTTOM-UP du Modèle OSI _(exactement l'inverse)_

#### Exemple concret ####

##### Couche 1 *(Matériel)* : 
- Est-ce que le switch/routeur est alimenté électriquement ?
- Est ce que le cable entre le switch et le routeur est toujours branché ?
- Est ce que le cable relié à ma carte réseau est-il toujours branché ?
- Est-ce que le port n'a pas été désactivé ?
- Est ce que je l'ai branché sur la bonne carte réseau (si j'en ai plusieurs ?)
- Est-ce que le driver de ma carte réseau est bien opérationnel ?

		ping 127.0.0.1

##### Couche 2 *(Liaison)*:
- Est-ce que je suis bien sur un switch manageable ?
- Est-ce que je ping une autre machine raccordée à ce même réseau *(son IP, bien que couche 2)*?
- Est-ce que je ping ma passerelle depuis un PC ou un switch manageable (niveau 3)?

##### Couche 3 *(Réseau)*: 
   - Est-ce que j'ai une adresse IP ? Et dans ce cas est elle cohérente avec mon réseau ?
   - Est-ce que je ping une IP externe à mon réseau ? 

			ping 8.8.8.8 #permet de ping le serveur DNS de Google

   - Est-ce que je passe par une mauvaise IP (ex : un proxy qui n'existe pas/plus ?)
- Est-ce que je ping un nom de site web externe 
			
			ping www.google.fr

- Est-ce que j'ai la bonne adresse qui pointe vers mon serveur DNS ?

##### Couche 4 *(Transport)*:
            
- Est-ce que mon pare-feu ne bloque pas des protocoles de transport *(TCP/UDP)*
- Est-ce que les ports logiciels les plus utilisés ne sont pas fermés/bloqués ?

### C) Les autres approches 

L'approche **"DIVIDE and CONQUER"** : 

- on démarre au milieu du modèle OSI

	_Exemple : si la couche 3 fonctionne, alors la couche 1 et 2 sont aussi fonctionnelles !_

L'approche **"FOLLOW THE PATH"** : 

- On part depuis l'appareil qui a un problème et ce jusqu'à la cible

	_Exemple : traceroute_

L'approche **"SPOT THE DIFFERENCES"** : 

- définir ce qui a changé depuis la dernière fois ou le problème n'était pas présent.
- Documenter tous les changements
- De garder un historique des changements
- Comparer deux équipements identiques, avec deux configurations différentes.

L'approche : **"MOVE THE PROBLEME"** : 

- Déplacer l'équipement dans le réseau et voir si le problème se déplace avec lui !

-----------------

## 3. Maintenance

### A) ITIL - IT Infrastructure Library ###

**Référence en terme de bonnes pratiques à mettre en place dans un service informatique** !

- Le service IT doit répondre au mieux aux attentes
- Proposer de façon permanente une qualité de service correcte aux employés
- Améliorer en continu le service IT (veille technologique, anticipation des problèmes)
- Réduction des coûts
- Améliorer la disponibilité du service IT

Tout cela **rends le service IT plus complexe.**


#### Vocabulaire ####

- **Baseline** : mesure de fonctionnement normal d'un service, d'une appli, d'un réseau, d'un équipement..
a comparer avec une baseline future ou précédente.
- **Workaround** : solution de contournement temporaire en attendant que le problème soit définitivement
résolu.
- **Know Error Database** : liste d'erreurs connues, et comment les résoudre.
- **Asset** : Tout ce qui permet de travailler, de générer de la valeur *(serveurs, BDD...)*

#### FCAPS - Fault Configuration Accounting Performance Security ###

- **Fault Management** : Détection et résolution de problèmes, prévention des nouveaux incidents, conserver les solutions trouvées

- **Configuration Management** : Sauvegarde de configurations et de données relatives aux configurations _(la doc)_, rédaction de
procédure, programmation des sauvegardes et remises en place

- **Accounting Management** : Collecte de statistiques sur l'utilisation des services informatiques _(par utilisateurs, par appareils, par réseaux..)_

- **Performance Management** : Maximisation et maintien des performances _(Monitoring/Supervision)_

- **Security Management :** Maintien de la sécurité _(intrusion, perte de données, piratage, contrôle des permissions, authentification, etc...)_

#### CLSA - Cisco Lifecycle Services Approach #### 
 *(ne concerne que le matériel réseau Cisco)*

- **Prepare** : définir les besoins
- **Plan** : définition des assets pour répondre au besoin
- **Design Implement** : Elaboration d'une solution répondant aux besoins
- **Operate** : maintenir le réseau au jour le jour (opérationnel)
- **Optimisation** : amélioration de la solution.

### B) Plusieurs Méthodes ###

**I) DOCUMENTATION !**

- En même temps que l'implémentation
- A chaque changement de configuration
- En étant le plus détaille possible

	On peut y retrouver :

	- Des schémas du réseau		_(avec plan de câblage)_
	- Détail de ce qui a été mis en place _(et comment)_
	- Des explications sur le fonctionnement
	- Les configurations avec des explications
	- Des guides de modification
	- Une liste des premières choses à vérifier en cas de problèmes
	- La liste des mots de passes stocké de manière sûre _(chiffrée)_

**II) CONNAISSANCE DU RÉSEAU**

- Apprendre à connaître un réseau 
- Chercher ou établir la documentation de ce réseau

**III) SAUVEGARDE**

- Sauvegarde de la configuration des équipements
- Copie des firmwares d'origine des équipements
- Copie des firmwares mis à jour des équipements
- Conservation des anciennes sauvegarde
	- Politique de sauvegarde: _Quoi ? Quand ? Comment ? Quel interval de temps ?_
- Procédure de sauvegarde simple et compréhensible

**IV) COHÉRENCE**

- Très difficile à cause de l'évolution au fur et à mesure du réseau
	- minimiser le nombre de constructeurs différents
	- conventions et nomenclature
	- plan d'adressage "signifiant"

**V) MONITORING**

- Mettre en place des alertes en cas de problème
- Mettre en place une consultation des équipements à partir d'une interface

	- Charge des liens réseau (saturation des tuyaux)
	- Charge CPU
	- Charge RAM
	- Occupation dique
	- Température des équipements / composants
	- Trafic WEB
	- Nombre de connexions VPN actives...

Ce monitoring va nous permettre de mettre en place une Baseline

**VI) AVOIR DU SPARE**

- Avoir du stock
- Si problème de coûts, avoir un équipement de secours.
- Conserver les anciens équipements obsolètes _(dans une certaine mesure)_

**VII) PROTECTION PHYSIQUE DES ÉQUIPEMENTS :**

- Placer en lieu sûr _(sécurité)_
- Avec un contrôle d'accès matériel et logiciel 
- Placer en lieu safe _(pas d'inondation, temperature trop élevées ou trop faible, perturbation electromagnétiques, etc..)_
- Protéger contre les surtensions _(onduleurs, double alimentation, etc..)_ / double alimentation



