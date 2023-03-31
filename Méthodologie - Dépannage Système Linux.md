# DÉPANNAGE SYSTÈME -- MÉTHODE :

## Idée générale :

**A - Méthodologie :**

Le Troubleshooting en admin système ne dispose pas d'une méthode concrète universelle applicable à tous les cas. L'idée générale est donc d'**appliquer la méthode scientifique** à notre situation problématique a savoir :

- **CONNAISSANCES** *sur son ou le type de système*
- **OBSERVATIONS** *des problèmes ou du comportement du système*
- **DÉDUCTION** *sur la provenance des problèmes existants*
- **ACTIONS** *à entreprendre pour tenter de régler le problème*
- **TESTS** *des solutions au problème, et revenir aux étapes précédentes pour chaque itération jusqu'à ce que le problème soit résolu*

	
	Dans notre cas, l'écosystème Linux, nous pouvons utiliser l'approche suivante : 

	Partir de la base du démarrage système vers les couches les plus "externes" (confrontés à l'utilisateur,
et au monde extérieur)

|   **BOOT**    |   **NOYAU**   |   **SYSTÈME**    |    **SERVICES APPLICATIFS**        |  **RÉSEAU**    |  **ENV.UTILISATEUR**
|   grub    |   linux    |    systemd    |  vos services (web, etc..)  |     ip     |  /etc/profile
                                                                    networking      /etc/bashrc
                                                                    Network-Manager /etc/

### 1) Grub est-il cassé ?

si oui : booter un système live sur cette même machine (usb, cd...) exécuter la commande pour réinstaller grub (Debian / Ubuntu) 

	"sudo grub-install /dev/sda"
même chose mais pour famille RedHat (doc officielle) :
	
	"https://access.redhat.com/documentation/fr-fr/red_hat_enterprise_linux/7/html/system_administrators_guide/sec-reinstalling_grub_2"
vérifier le fichier de configuration : 

	"/etc/default/grub"

### Outils utils pour la plupart des cas pour un débutant :
- SuperGrubDisk ~ 15Mo
- Rescatux ~ 650Mo
 
Ce sont deux fichiers iso à télécharger sur leur sites officiels, dans le but de créer des clés USB live (bootable) comprenant une suite d'outils pour réparer Grub et la plupart des problèmes rencontrés au démarrage


### 2) Le système démarre en mode rescue/emergency :
Étudiez les logs du noyau Linux

		"dmesg" ou "journalctl -k"
		"dmesg -T | tail"

### 3)    - Vérifier les erreurs dans les services systèmes
        "journalctl -pe err"
        "journalctl --since yesterday"
Vérifier l'état des différents composant de l'initialisation système (systemd)

        "status status systemd*"

se renseigner sur le but et le fonctionnement de chacun de ces services
Vérifier la target définie par défaut et tenter de l'atteindre

		"systemctl isolate TARGET"

Vérifier l'uptime et vérifier les 3 niveaux de charge système

        "uptime"

### 4)  - Vérifier le statut des services réseaux sur votre distribution
        "systemctl status systemd-networkd"
        "systemctl status networking.service"
        "systemctl status NetworkManager.service"

Vérifier le statut d'actuvation des interfaces, physiques comme virtuelles :

        "ip link show"

Vérifier leur configuration IP

        "ip addr show"
    
Forcez l'interface en mode adressage automatique
 
       "sudo dhclient -r"
        "sudo dhclient"

Vérifier le comportement de la pile tcp/ip

        ping 127.0.0.1

Vérifier la communication sur le réseau local

		ping @de_passerelle/votre_box

Vérifier la communication vers l'extérieur par IP

        ping 8.8.8.8

Vérifier la communication vers l'extérieur par nom

        ping www.clubic.com

rectifier via "ip", "nmcli", "nmtui"

### 5) - Vérifier l'intégrité des fichiers /etc/profile, /etc/bashrc, ainsi que les fichiers propres aux utilisateurs :
    
	".bashrc ; .profile ; .bash_history ;"
