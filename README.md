# ENSEA_S10_TP_Notau_Temps_Reel FreeRTOS
TP_Notau_Temps_Reel_FreeRTOS
# Laloux Yann, Geslin Arthur et Lejars Valentin
Premiers pas
Créez un projet pour la carte STM32F746G-DISCO.
Configuration sur du STM32CubeIDE :
- System Core > RCC > High Speed Clock (HSE) = Crystal/Ceramic Resonator
- System Core > SYS > Debug = Serial Wire
Configurez la broche PI1 en sortie (c’est la LED !).
- PI1 > GPIO Output
- "Clock Configuration". Mettez HCLK à 216MHz
-  Dans Projet Manager puis Code Generator, dans la rubrique Genereted files cocher "Generate peripheral initialization as a pair of '.c /' h ' files per peripheral"
- 
0.1 Premiers pas
1) Le nom du projet est "TP_Noyau_Temps_Reel" -> Core -> Src -> "main.c"
2) Les balises BEGIN et END (ou des balises similaires) sont des outils utiles pour organiser, naviguer, comprendre, déboguer et collaborer sur du code dans un environnement de développement comme STM32CubeIDE.

1) FreeRTOS, tâches et sémaphores
1.1) Tâche simple
Le paramètre TOTAL_HEAP_SIZE est crucial pour garantir le bon fonctionnement de FreeRTOS en fournissant suffisamment de mémoire pour les allocations dynamiques nécessaires à l'exécution des tâches et des autres structures de données. Sa valeur doit être soigneusement sélectionnée en fonction des besoins spécifiques de votre application.
1.2) Sémaphores pour la synchronisation
1.3) Notification
1.4) Queues
1.5) Réentrance et exclusion mutuelle

2 On joue avec le Shell

3 Debug, gestion d’erreur et statistiques



