# ENSEA_S10_TP_Noyau_Temps_Reel FreeRTOS
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
<h2>1.2) Sémaphores pour la synchronisation</h2> <br/>
</h2>1.3) Notification</h2> <br/>
</h2>1.4) Queues</h2> <br/>
</h2>1.5) Réentrance et exclusion mutuelle</h2> <br/>
- On remarque que la taches 1 est intérrompu par la tâche 2. On a dans un 1er temps changé la valeur de TASK1_DELAY1 pour qu'il est le même delais que TASK1_DELAY2
- On a utiliser le semphore mutex pour "verrouillé" afficher notre message dans son entièreté avec la liaison UART et "déverrouillé" le mutex.

<h1>2 On joue avec le Shell</h1><br/>

</h2>1.3) </h2> <br/>
- le shell interprète les commandes entrées par l'utilisateur, analyse les arguments et appelle les fonctions correspondantes avec ces arguments. Dans le shell en tapant le caractère une chaine de caractère commençant par le caractère "a", la méthode "fonction" est lancé et affiche les caractères. Lorsque le shell appelle cette fonction, elle est exécutée. Dans ce cas, la fonction fonction envoie un message via UART en utilisant les fonctions de transmission du shell. Après l'exécution de la fonction, le contrôle est renvoyé au shell, qui attend une nouvelle entrée de l'utilisateur.

![alt text](https://github.com/Zardoke/ENSEA_S10_TP_Noyau_Temps_Reel/assets/144770542/7a67b71f-9816-48ea-8be1-16b39cc28ccb)

</h2>1.4) </h2> <br/>
Le problème dans cette implémentation est que la fonction fonction utilise la structure h_shell_t pour accéder aux fonctions de transmission du shell (transmit). Cependant, la structure h_shell_t n'est pas passée en tant que paramètre à la fonction fonction. Cela peut conduire à des erreurs ou un comportement indéterminé, car la fonction ne dispose pas d'un accès direct à la structure.

![alt text](https://github.com/Zardoke/ENSEA_S10_TP_Noyau_Temps_Reel/assets/144770542/75ac1fb6-70da-4322-9620-6b08c2f0cd70)

</h2>1.5) </h2> <br/>
Pour résoudre ce problème, la structure h_shell_t doit être passée en tant que paramètre à la fonction fonction. Cela permettra à la fonction d'accéder correctement aux fonctions de transmission du shell. Voici comment la fonction fonction peut être modifiée pour recevoir la structure h_shell_t en tant que paramètre :
Avec notre modification, la fonction addition retourne toujours une valeur, même si elle rencontre une erreur.
</h2>2) </h2> <br/>
Le non-respect des priorités peut entraîner des problèmes pouvant faire planter le programme.

Le non respect des priorités des tâches dans un système d'exploitation temps réel comme FreeRTOS,  peut entraîner des problèmes de performances et de comportement. Par exemple, si une tâche critique avec une priorité élevée est bloquée par une tâche non critique avec une priorité plus basse, cela peut entraîner des retards dans le traitement des tâches critiques.

<img width="194" alt="Capture" src="https://github.com/Zardoke/ENSEA_S10_TP_Noyau_Temps_Reel/assets/144770542/e35fc2f0-c6ff-48e9-9eba-00fc7663a0d7"><br/>

La fonction task_blink_led est créée comme une tâche FreeRTOS. Cette fonction est responsable du clignotement de la LED.
Dans la boucle infinie de cette fonction (for (;;)) :
La LED est basculée (allumée ou éteinte) à l'aide de HAL_GPIO_TogglePin(LED_GPIO_Port, LED_Pin). Cette fonction bascule simplement l'état de la broche de la LED entre allumé et éteint à chaque itération de la boucle.
Ensuite, la tâche est mise en pause pendant une période de temps spécifiée à l'aide de vTaskDelay(period / portTICK_PERIOD_MS). Cela permet de contrôler la fréquence de clignotement de la LED en ajustant la valeur de period.
Lorsque la fonction led est appelée depuis le shell avec une période spécifiée, elle met à jour la variable globale period avec la période spécifiée. Si la période est définie à 0, la tâche de clignotement de la LED est suspendue, ce qui a pour effet d'éteindre la LED.

<h1>3 Debug, gestion d’erreur et statistiques</h1>
<h2>3.1 Gestion du tas</h2> <br/>
</h2>1) </h2> <br/>
La zone réservée à l'allocation dynamique est généralement appelée le "tas" ou la "zone de heap".
</h2>2) </h2> <br/>
Le tas est géré par FreeRTOS, pas par la HAL (Hardware Abstraction Layer). FreeRTOS alloue et gère dynamiquement la mémoire nécessaire pour les tâches, les files d'attente, les sémaphores, etc. Cela inclut l'allocation dynamique de mémoire pour les structures de données utilisées par le système d'exploitation. La HAL, en revanche, fournit des interfaces logicielles pour accéder au matériel spécifique du microcontrôleur, mais elle n'est pas responsable de la gestion de la mémoire dynamique utilisée par FreeRTOS.




