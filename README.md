# MANUEL DE RÉFÉRENCE WeARM v3.5RC

## 1. Introduction Technique
WeARM est un contrôleur de flux binaire dynamique et un environnement de prototypage haute performance pour l'assembleur bas niveau (ARM64 et x86_64). Le logiciel automatise la complexité des chaînes d'outils de compilation croisée pour permettre une transition fluide vers les environnements de production industriels.

---

## 2. Modèle de Licence
WeARM est distribué selon plusieurs paliers afin de s'adapter aux besoins des utilisateurs :
* **Licence Community** : Version gratuite destinée à l'apprentissage, aux étudiants et aux développeurs indépendants. Elle inclut les fonctionnalités essentielles du contrôleur de flux et du VFS.
* **Licences Professionnelles** : Versions étendues pour l'industrie incluant des moteurs de performance avancés et des outils d'analyse critiques.

---

## 3. Moteur AETHER™ : Performance Atomique
*Note : Technologie disponible exclusivement dans les versions Pro et supérieures.*

Le moteur AETHER redéfinit la réactivité du développement bas niveau :
* **Gestion Mémoire "Lock-Free"** : Isolation par thread (TLS) via Slab Arena, éliminant 100% des verrous système (Mutex).
* **Latence de Cycle < 12µs** : Cycle complet (Initialisation, Allocation, Traitement et Destruction) exécuté en moyenne en 11,7 microsecondes.
* **Localité Spatiale Optimisée** : Rétention forcée des données dans le cache processeur pour éviter les accès à la RAM lente.

---

## 4. Architecture Découplée & Plugins de Précision
L'intelligence de WeARM repose sur une architecture modulaire où les composants critiques sont externalisés :
* **Moteurs d'Analyse Distribués** : Le désassemblage (Capstone), le Highlighting et les suggestions d'instructions opèrent sous forme de plugins autonomes.
* **SDK & Évolutivité (v3.6RC)** : Architecture permettant l'intégration de moteurs tiers. Le plugin 'com.wearm.engine.capstone' sera disponible sous licence MIT comme modèle.
* **Moteur de Scripting LUA** : Intégration native du loader 'com.wearm.core.loader.lua' pour l'extension de fonctionnalités via scripts.

---

## 5. Le Trampoline : Surveillance & Diagnostic
L’exécution est encapsulée dans une couche propriétaire garantissant un débogage chirurgical :
* **Analyseur de Conformité ABI** : Surveillance active des conventions d'appel et alertes immédiates en cas de violation des registres non-volatils.
* **Introspection Multimédia** : Affichage temps réel des registres SSE (x86) et NEON (ARM).
* **Réconciliation de Crash** : Calcul de l'offset statique en cas d'erreur fatale avec pointage direct de la ligne source dans l'éditeur.

---

## 6. Architecture VFS (Virtual File System)
* **Importation Sécurisée** : Travail exclusif sur des copies virtuelles sans altérer les sources de référence.
* **Exécution Isolée (Sandbox)** : Redirection automatique des opérations vers la zone sécurisée Work/.
* **Structure de Projet** : `src/` (sources), `headers/` (dépendances), `build/` (objets et binaires), `Work/` (sandbox).

---

## 7. Noyau d'Introspection Binaire
WeARM déconstruit le code pour identifier les structures machine réelles :
* **Parsing Haute Fidélité** : Analyse native des formats PE, COFF et ELF.
* **Scoring Intelligence** : Détection automatique du point d’entrée pour un linking correct sans symboles explicites.
* **Innovation Windows** : Résolution des liaisons complexes sans usage de fichiers .def ou directives __declspec.

---

## 8. Pilotage Multi-Toolchain & Extensions
Couche d'abstraction entre l'utilisateur et les outils de compilation :
* **Agnosticisme des Outils** : Drivers pour NASM, FASM, GNU AS et CLANG sans reconfiguration des sources.
* **Injection d'Environnement** : Manipulation dynamique des variables pour la visibilité immédiate du VFS.
* **Liaison Hybride** : Sélection automatique entre linkers bas niveau (ld, lld) et drivers complexes (Clang).

---

## 9. Téléchargements et Distribution
Versions officielles de la licence Community :
* macOS : [Télécharger WeARM.dmg](https://upd.wearm.dev/get/mac)
* Windows : [Télécharger WeARM_Setup.exe](https://upd.wearm.dev/get/windows)

---

## 10. Variables de Substitution
* **$SRCPATH** : Chemin absolu vers le fichier source (.s).
* **$OUTPATH** : Destination pour l'objet généré (.o).
* **$INCDIR** : Dossier miroir des en-têtes.
* **$OUT** : Chemin complet du binaire final.
* **$OBJS** : Liste consolidée des fichiers objets.

---

## 11. Licence
Ce dépôt est utilisé pour la distribution des binaires officiels. Le code source de WeARM est propriétaire. Consultez le fichier LICENSE.txt pour le contrat EULA.

© 2026 WeARM Core™ – Technologie Propriétaire. Tous droits réservés.# MANUEL DE RÉFÉRENCE WeARM v3.5RC

## 1. Introduction Technique
WeARM est un contrôleur de flux binaire dynamique et un environnement de prototypage haute performance pour l'assembleur bas niveau (ARM64 et x86_64). Le logiciel automatise la complexité des chaînes d'outils de compilation croisée pour permettre une transition fluide vers les environnements de production industriels.

---

## 2. Modèle de Licence
WeARM est distribué selon plusieurs paliers afin de s'adapter aux besoins des utilisateurs :
* **Licence Community** : Version gratuite destinée à l'apprentissage, aux étudiants et aux développeurs indépendants. Elle inclut les fonctionnalités essentielles du contrôleur de flux et du VFS.
* **Licences Professionnelles** : Versions étendues pour l'industrie incluant des moteurs de performance avancés et des outils d'analyse critiques.

---

## 3. Moteur AETHER™ : Performance Atomique
*Note : Technologie disponible exclusivement dans les versions Pro et supérieures.*

Le moteur AETHER redéfinit la réactivité du développement bas niveau :
* **Gestion Mémoire "Lock-Free"** : Isolation par thread (TLS) via Slab Arena, éliminant 100% des verrous système (Mutex).
* **Latence de Cycle < 12µs** : Cycle complet (Initialisation, Allocation, Traitement et Destruction) exécuté en moyenne en 11,7 microsecondes.
* **Localité Spatiale Optimisée** : Rétention forcée des données dans le cache processeur pour éviter les accès à la RAM lente.

---

## 4. Architecture Découplée & Plugins de Précision
L'intelligence de WeARM repose sur une architecture modulaire où les composants critiques sont externalisés :
* **Moteurs d'Analyse Distribués** : Le désassemblage (Capstone), le Highlighting et les suggestions d'instructions opèrent sous forme de plugins autonomes.
* **SDK & Évolutivité (v3.6RC)** : Architecture permettant l'intégration de moteurs tiers. Le plugin 'com.wearm.engine.capstone' sera disponible sous licence MIT comme modèle.
* **Moteur de Scripting LUA** : Intégration native du loader 'com.wearm.core.loader.lua' pour l'extension de fonctionnalités via scripts.

---

## 5. Le Trampoline : Surveillance & Diagnostic
L’exécution est encapsulée dans une couche propriétaire garantissant un débogage chirurgical :
* **Analyseur de Conformité ABI** : Surveillance active des conventions d'appel et alertes immédiates en cas de violation des registres non-volatils.
* **Introspection Multimédia** : Affichage temps réel des registres SSE (x86) et NEON (ARM).
* **Réconciliation de Crash** : Calcul de l'offset statique en cas d'erreur fatale avec pointage direct de la ligne source dans l'éditeur.

---

## 6. Architecture VFS (Virtual File System)
* **Importation Sécurisée** : Travail exclusif sur des copies virtuelles sans altérer les sources de référence.
* **Exécution Isolée (Sandbox)** : Redirection automatique des opérations vers la zone sécurisée Work/.
* **Structure de Projet** : `src/` (sources), `headers/` (dépendances), `build/` (objets et binaires), `Work/` (sandbox).

---

## 7. Noyau d'Introspection Binaire
WeARM déconstruit le code pour identifier les structures machine réelles :
* **Parsing Haute Fidélité** : Analyse native des formats PE, COFF et ELF.
* **Scoring Intelligence** : Détection automatique du point d’entrée pour un linking correct sans symboles explicites.
* **Innovation Windows** : Résolution des liaisons complexes sans usage de fichiers .def ou directives __declspec.

---

## 8. Pilotage Multi-Toolchain & Extensions
Couche d'abstraction entre l'utilisateur et les outils de compilation :
* **Agnosticisme des Outils** : Drivers pour NASM, FASM, GNU AS et CLANG sans reconfiguration des sources.
* **Injection d'Environnement** : Manipulation dynamique des variables pour la visibilité immédiate du VFS.
* **Liaison Hybride** : Sélection automatique entre linkers bas niveau (ld, lld) et drivers complexes (Clang).

---

## 9. Téléchargements et Distribution
Versions officielles de la licence Community :
* macOS : [Télécharger WeARM.dmg](https://upd.wearm.dev/get/mac)
* Windows : [Télécharger WeARM_Setup.exe](https://upd.wearm.dev/get/windows)

---

## 10. Variables de Substitution
* **$SRCPATH** : Chemin absolu vers le fichier source (.s).
* **$OUTPATH** : Destination pour l'objet généré (.o).
* **$INCDIR** : Dossier miroir des en-têtes.
* **$OUT** : Chemin complet du binaire final.
* **$OBJS** : Liste consolidée des fichiers objets.

---

## 11. Licence
Ce dépôt est utilisé pour la distribution des binaires officiels. Le code source de WeARM est propriétaire. Consultez le fichier LICENSE.txt pour le contrat EULA.

© 2026 WeARM Core™ – Technologie Propriétaire. Tous droits réservés.
