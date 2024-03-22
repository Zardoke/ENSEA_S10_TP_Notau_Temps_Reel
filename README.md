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

