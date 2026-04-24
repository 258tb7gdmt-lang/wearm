# MANUEL DE RÉFÉRENCE WeARM v3.5RC

## 1. Introduction Technique
WeARM est un contrôleur de flux binaire dynamique et un environnement de prototypage haute performance pour l'assembleur bas niveau (ARM64 et x86_64). Le logiciel automatise la complexité des chaînes d'outils de compilation croisée pour permettre une transition fluide vers les environnements de production industriels.

---

## 2. Moteur AETHER™ : Performance Atomique
*Note : Technologie disponible exclusivement dans les versions Pro et supérieures.*

Le moteur AETHER redéfinit la réactivité du développement bas niveau par les caractéristiques suivantes :
* **Gestion Mémoire "Lock-Free"** : Utilisation d'une isolation par thread (TLS). Chaque unité de calcul dispose de son propre segment mémoire (Slab Arena), éliminant les verrous système (Mutex).
* **Latence de Cycle Inférieure à 12µs** : Cycle complet (Initialisation, Allocation de 100 objets Managed, Traitement et Destruction) exécuté en moyenne en 11,7 microsecondes.
* **Localité Spatiale Optimisée** : Rétention forcée des données dans le cache processeur pour éviter les accès à la RAM lente durant l'analyse critique.

---

## 3. Architecture VFS (Virtual File System)
WeARM repose sur une couche d'abstraction propriétaire garantissant l'intégrité des actifs numériques.
* **Importation Sécurisée** : Travail exclusif sur des copies virtuelles sans altérer les sources de référence.
* **Exécution Isolée (Sandbox)** : Redirection automatique des opérations de fichier (Écriture, Chargement de DLL) vers la zone sécurisée Work/.
* **Structure de Projet** :
    * **src/** : Dossier racine pour les fichiers sources (.s, .asm).
    * **headers/** : Centralisation des dépendances (.h, .inc) pour résolution automatique.
    * **build/** : Zone de sortie volatile (fichiers .o et binaires finaux).
    * **Work/** : Couche d'exécution interne sandboxée.

---

## 4. Téléchargements et Distribution
Les liens suivants pointent vers les dernières versions signées :
* macOS : [Télécharger WeARM.dmg](https://upd.wearm.dev/get/mac)
* Windows : [Télécharger WeARM_Setup.exe](https://upd.wearm.dev/get/windows)

---

## 5. Cycle de Développement
* **PROJ_ISO** : Développement de routines isolées (Mode PIC) pour validation ABI et injection dynamique.
* **PROJ_EXE** : Finalisation d'applications exécutables avec configuration du point d'entrée.
* **PROJ_BARE** : Développement IoT et Embarqué sans bibliothèque standard (-nostdlib).

---

## 6. Variables de Substitution
Pilotage des outils personnalisés via les balises système :
* **$SRCPATH** : Chemin absolu vers le fichier source (.s).
* **$OUTPATH** : Destination pour l'objet généré (.o).
* **$INCDIR** : Chemin vers le dossier miroir des en-têtes (.h / .inc).
* **$OUT** : Chemin complet du binaire final (EXE ou DLL).
* **$OBJS** : Liste consolidée de tous les fichiers objets du projet (.o).

---

## 7. Licence
Ce dépôt est utilisé pour la distribution des binaires officiels. Le code source de WeARM est propriétaire et protégé par le droit d'auteur.
Consultez le fichier LICENSE.txt pour les conditions du contrat de licence utilisateur final (EULA).

© 2026 WeARM Core™ – Technologie Propriétaire. Tous droits réservés.
