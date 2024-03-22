# ENSEA_S10_TP_Notau_Temps_Reel FreeRTOS
TP_Notau_Temps_Reel_FreeRTOS
# Laloux Yann, Geslin Arthur et Lejars Valentin 3DN
# Séance 1 : 22/03/2024

<h1>1 FreeRTOS, tâches et sémaphores</h1>
Créez un projet pour la carte STM32F746G-DISCO. <br/>
Configuration sur du STM32CubeIDE :
- System Core > RCC > High Speed Clock (HSE) = Crystal/Ceramic Resonator <br/>
- System Core > SYS > Debug = Serial Wire & TIM6 <br/>
- FreeRTOS > CMSIS_V1 <br/>
Configurez la broche PI1 en sortie (c’est la LED !). 
- PI1 > GPIO Output <br/>
- "Clock Configuration". Mettez HCLK à 216MHz <br/>
-  Dans Projet Manager puis Code Generator, dans la rubrique Genereted files cocher "Generate peripheral initialization as a pair of '.c /' h ' files per peripheral" <br/>
- Le nom du projet est "TP_Noyau_Temps_Reel" -> Core -> Src -> "main.c" <br/>
- Les balises BEGIN et END (ou des balises similaires) sont des outils utiles pour organiser, naviguer, comprendre, déboguer et collaborer sur du code dans un environnement de développement comme STM32CubeIDE. <br/>

<h2>1.1) Tâche simple</h2> <br/>
- Le paramètre TOTAL_HEAP_SIZE est crucial pour garantir le bon fonctionnement de FreeRTOS en fournissant suffisamment de mémoire pour les allocations dynamiques nécessaires à l'exécution des tâches et des autres structures de données. Sa valeur doit être soigneusement sélectionnée en fonction des besoins spécifiques de votre application. <br/>
- La configuration dans le fichier FreeRTOSConfig.h permet d'adapter FreeRTOS aux besoins spécifiques de notre application, en ajustant les paramètres de performance, de taille mémoire et de fonctionnalités pour atteindre les objectifs de notre projet. Ces ajustements judicieux peuvent permettre d'optimiser l'utilisation des ressources et garantir le bon fonctionnement de votre système en temps réel. <br/>
- portTICK_PERIOD_MS est une macro cruciale dans FreeRTOS qui définit la durée d'une tique en millisecondes, facilitant ainsi la programmation temporelle dans les applications utilisant FreeRTOS. <br/>
1.2) Sémaphores pour la synchronisation <br/>
1.3) Notification <br/>
1.4) Queues <br/>
1.5) Réentrance et exclusion mutuelle <br/>

<h1>2 On joue avec le Shell</h1>

<h1>3 Debug, gestion d’erreur et statistiques</h1>



