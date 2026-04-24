# WeARM v3.5RC - MANUEL DE RÉFÉRENCE & ARCHITECTURE

## 1. Introduction Technique
WeARM est un contrôleur de flux binaire dynamique et évolutif, ainsi qu'un environnement de prototypage haute performance pour l'assembleur bas niveau (ARM64 et x86_64).
Conçu pour les entreprises, les industries de haute technologie et le secteur de l'IoT, WeARM automatise la complexité des chaînes d'outils de compilation croisée. Il permet une transition fluide de la conception algorithmique en assembleur vers les environnements de production industriels.

---

## 2. Modèle de Licence
WeARM est distribué selon plusieurs paliers afin de s'adapter aux besoins des utilisateurs :
- **Licence Community** : Version gratuite destinée à l'apprentissage, aux étudiants et aux développeurs indépendants. Elle inclut les fonctionnalités essentielles du contrôleur de flux et du VFS.
- **Licences Professionnelles** : Versions étendues pour l'industrie incluant des moteurs de performance avancés et des outils d'analyse critiques.

---

## 3. Infrastructure de Calcul AETHER™
*Note : Technologie disponible exclusivement dans les versions Pro et supérieures.*

Le Core de WeARM est propulsé par AETHER, une infrastructure de calcul propriétaire conçue pour l'exécution massivement parallèle et la suppression des goulots d'étranglement mémoires traditionnels.

- **Souveraineté Mémoire (O(1))** : Contrairement aux gestions de tas (Heap) standards, AETHER utilise un moteur d'allocation déterministe. Chaque objet `we::Managed` bénéficie d'un accès instantané à la ressource, garantissant une fluidité constante même sous une charge de calcul extrême.
- **Déterminisme Temporel** : Le cycle de vie complet d'une session de calcul (Initialisation, Allocation de 100 objets Managed, Traitement et Destruction) est stabilisé à une moyenne de 11,7 microsecondes. Cette précision garantit une réactivité prédictible, indispensable pour l'analyse chirurgicale des flux d'instructions ARM64 et x86_64.
- **Optimisation de la Barrière Silicium** : AETHER maximise la localité spatiale en alignant dynamiquement les structures de données sur l'architecture interne du processeur. Le moteur réduit drastiquement les cycles d'attente (Wait States) en optimisant les interactions avec les caches de données et les unités de gestion mémoire (MMU) du CPU.

---

## 4. Architecture Découplée & Plugins de Précision
L'intelligence de WeARM ne repose pas sur un bloc monolithique, mais sur une architecture modulaire où les composants critiques sont externalisés et substituables.
- **Moteurs d'Analyse Distribués** : Le moteur de désassemblage (basé sur Capstone), le Highlighting et les suggestions d'instructions opèrent sous forme de plugins autonomes.
- **SDK & Évolutivité (v3.6RC)** : Cette architecture permet aux industries d'intégrer leurs propres moteurs. Le plugin 'core.wearm.engine.capstone' sera disponible sous licence MIT pour servir de modèle de substitution.
- **Moteur de Scripting LUA** : Intégration native du loader 'com.wearm.core.loader.lua'. Il permet l'extension de fonctionnalités via scripts LUA, offrant une alternative agile au développement C/C++.

---

## 5. Le Trampoline : Surveillance & Diagnostic
L’exécution est encapsulée dans une couche propriétaire (Trampoline). Elle garantit une sécurité maximale et un débogage chirurgical.
- **Analyseur de Conformité ABI** : Surveillance active des conventions d'appel. Toute violation des registres non-volatils déclenche une alerte immédiate.
- **Introspection Multimédia** : Affichage temps réel des registres SSE (x86) et NEON (ARM), essentiel pour l'optimisation de haute performance.
- **Réconciliation de Crash** : Le moteur calcule l'offset statique en cas d'erreur fatale et pointe la ligne source fautive directement dans l'éditeur.

---

## 6. Architecture VFS & Gestion des Sources
WeARM repose sur une couche d'abstraction propriétaire : le système de fichiers virtuel (VFS). Cette technologie garantit l'intégrité totale de vos actifs numériques.
- **Importation Sécurisée** : WeARM ne travaille jamais sur vos fichiers originaux. Lors de l'importation, le VFS crée une copie exacte dans un dossier projet dédié.
- **Étanchéité (Sandbox)** : Vous pouvez modifier, tester et crash-tester votre code sans jamais altérer vos sources de référence. Le dossier caché `Work/` redirige automatiquement les opérations de fichier relatives vers cette zone sécurisée.
- **Structure du Projet** :
    - `src/` : Dossier racine pour vos fichiers sources (.s, .asm). Virtualisé et persistant.
    - `headers/` : Centralise les fichiers d'en-tête (.h, .inc) pour la résolution automatique des dépendances.
    - `build/` : Zone de sortie volatile vidée à chaque début de build (.o, .exe, .dll, .a, .dylib).
    - `Work/` : (Caché) Couche d'exécution interne sandboxée.

---

## 7. Noyau d'Introspection Binaire & Recherche
WeARM déconstruit le code pour identifier les structures machine réelles avec une précision absolue.
- **Parsing Haute Fidélité** : Analyse native des formats PE, COFF et ELF. Il cartographie les segments directement depuis le binaire assemblé. Cette introspection s'appuie sur nos propres moteurs de parsing entièrement autonomes : WeARM ne dépend d'aucune API système et reste insensible aux mises à jour ou modifications des bibliothèques de l'OS.
- **Scoring Intelligence** : Détection automatique du point d’entrée garantissant un linking correct sans besoin de symboles explicites de la part de l'utilisateur.
- **Innovation Windows** : Outrepasse les limites natives en résolvant les liaisons complexes et l'extraction des symboles sans usage de fichiers .def ou de directives `__declspec`.
- **Recherche Universelle** : Recherche active après exécution utilisant l'extraction des symboles du projet complet. Détection des conflits (Duplicate Labels) et Quick-Jump vers l'instruction.

---

## 8. Pilotage Multi-Toolchain & Extensions
Couche d'abstraction intelligente entre l'utilisateur et les outils de compilation (Toolchains).
- **Agnosticisme des Toolchains** : Drivers intégrés pour NASM, FASM, GNU AS et CLANG. Le passage d'un moteur d'assemblage à un autre s'effectue sans aucune modification des sources originales ni reconfiguration des scripts de build. WeARM assure la cohérence des paramètres d'entrée/sortie quel que soit l'outil piloté.
- **Injection d'Environnement** : WeARM manipule dynamiquement les variables d'environnement système pour garantir que les outils externes "voient" le VFS sans configuration manuelle.
- **Driver de Liaison Hybride** : Sélection automatique entre linkers bas niveau (ld, lld) et drivers complexes (Clang) pour l'automatisation des SDK (UCRT, libSystem).
- **Extensions Réseau** : L'inclusion de modules comme 'network.http' démontre la capacité d'extension du Core pour la communication et la télémétrie.

---

## 9. Cycle de Développement & Types de Projets
- **PROJET : Fonction Isolée (PROJ_ISO / Mode PIC)** : Validation d'une routine de calcul. Vérification stricte de l'ABI et exécution sans crash. Génère du code indépendant de la position prêt pour l'injection dynamique.
- **PROJET : Application Exécutable (PROJ_EXE)** : Finalisation du logiciel pour une exécution directe par l'OS. Résolution des dépendances et configuration du point d'entrée.
- **PROJET : IoT & Embarqué (PROJ_BARE)** : Développement de micro-kernels et firmwares. Mode sans bibliothèque standard (-nostdlib) pour un contrôle matériel total.

---

## 10. Variables de Substitution Dynamiques
Balises pour piloter vos outils personnalisés :
- `$SRCPATH` : Chemin absolu vers le fichier source (.s).
- `$OUTPATH` : Destination pour l'objet généré (.o).
- `$INCDIR` : Chemin vers le dossier miroir des en-têtes (.h / .inc).
- `$OUT` : Chemin complet du binaire final (EXE ou DLL).
- `$OBJS` : Liste consolidée de tous les fichiers objets du projet (.o).
- `$LIBS` : Liste des chemins vers les bibliothèques externes configurées.

---

## 11. Téléchargements & Distribution (Licence Community)
- **macOS** : [Télécharger WeARM.dmg](https://upd.wearm.dev/get/mac)
- **Windows** : [Télécharger WeARM_Setup.exe](https://upd.wearm.dev/get/windows)

© 2026 WeARM Core™ – All rights reserved. Proprietary Technology.
