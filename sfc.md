---
Date création : 2023-08-03
Status: Brouillon 
DigitalGarden: true
share: true
--- 
SFC est un outil Windows (fourni à l'installation du système) qui permet d'analyse la configuration du système et de détecter des erreurs. 

Quand j'ai un problème sur un poste, c'est la première commande que je lance. 
/git
Son utilisation basic est : 
```batch
sfc /scannow
```

Et si des erreurs corrigées sont présentes, un reboot du système (parfois très long), permet de gérer le problème. 

En règle générale cette instruction permet de résoudre des problèmes incompréhensible : 
- Pas d'envoi depuis outlook 
- Windows qui fige 
## Quand cela en suffit pas
Dans certains cas, Windows n'arrive pas à se réparer, mais aussi parfois la réparation dure 2 jours, et après l'utilisateur me recontacte pour son problème. 

Je lance un scan complet 
```batch
DISM /online /Cleanup-Image /StartComponentCleanup
DISM /online /Cleanup-Image /AnalyzeComponentStore
Dism /Online /Cleanup-Image /CheckHealth
Dism /Online /Cleanup-Image /RestoreHealth
sfc /scannow
```

## Cas d'erreur dans le package 
Il m'est arrivé 2 d'avoir besoin de recréer le package depuis l'installation de Windows. 
Après avoir télécharger un ISO Windows, et monter celui en tant que lecteur DVD, je lance la commande pour recréer le package Windows (lecteur f: dans mon cas)
```batch
DISM /Online /Cleanup-Image /RestoreHealth /source:WIM:f:\Sources\Install.wim:1 / LimitAccess
sfc /scannow
```

Il est aussi utile de regarder dans l'observateur d'évènement. 
