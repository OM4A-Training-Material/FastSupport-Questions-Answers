# ❓ Questions & Réponses par Modèle

---

## 🧮 GENeSYS-MOD

**Q : Comment installer GENeSYS-MOD et ai-je besoin d'une licence ?**  
R : Pour l'installation, suivez le [Guide d'installation](https://genesysmod.readthedocs.io). Aucune licence n'est requise pour exécuter le modèle – tout est open-source. Si votre institution dispose d’un accès à un solveur commercial (ex. Gurobi), vous pouvez l’utiliser.

**Q : Comment remplir les jeux de données Excel – où puis-je trouver les modèles et conventions de nommage ?**  
R : Les modèles et conventions sont disponibles dans le Guide des Données d'Entrée et le Guide des Données Horaires dans [ce dépôt](https://github.com/OM4A-Training-Material).

**Q : Quelles options de configuration sont disponibles et comment influencent-elles le comportement du modèle ?**  
R : Le Guide d'Exécution explique toutes les options. Accédez-le [ici](https://docs.google.com/document/d/1LI9mHE5MGleJ4G8OTMvSU3DDtScnruNpQI6xX-WcEyQ/edit?usp=sharing). Une copie sera bientôt disponible sur ReadTheDocs.

**Q : Quels solveurs sont supportés (Gurobi, CPLEX, HiGHS, Ipopt), et comment les configurer ?**  
R : Tous sauf CPLEX peuvent être utilisés. Indiquez le solveur dans le fichier de lancement – vous pouvez le modifier à tout moment.

---

## ⚡ openTEPES

**Q : Comment l’installer ?**  
R :

- openTEPES fonctionne sous Windows et Ubuntu.
- Guides d'installation disponibles :
  - [ReadTheDocs](https://opentepes.readthedocs.io/en/latest/Download.html)
  - [PDF Installation Manual](https://pascua.iit.comillas.edu/aramos/openTEPES_installation.pdf)
- Solveurs recommandés :
  - **Gurobi** (licence académique gratuite)
  - **HiGHS** (open-source)
  - **GAMS/CPLEX** (si licence disponible)

**Q : Quel type de PC est nécessaire ?**  
R :

- Cela dépend de l’étude de cas :
  - Périodes, niveaux de charge
  - Complexité du réseau
  - Stochasticité
  - Variables binaires
- Règle empirique : 1 Go RAM par million de lignes d’optimisation.
- Exemple : les études fournies tournent sur un portable avec 16 Go RAM.

**Q : Que faire juste après l’installation ?**  
R :

- Essayez les 7 études de cas fournies.
- Vérifiez la mémoire système si un cas ne fonctionne pas.

**Q : Problèmes fréquents ?**  
R :

- Tous les éléments définis doivent apparaître dans les fichiers de dictionnaires.
- Minimum 2 nœuds et 1 ligne de transmission.
- Minimum 1 générateur.
- Toutes les demandes doivent être reliées à des nœuds.

**Q : Comment simplifier les données pour des tests ?**  
R :

- Supprimez les durées après 168h dans `oT_Data_Duration`.
- Utilisez des pas de temps de 2–3h.
- Scénarios avec 0.0 probabilité, périodes à 0.0 poids.
- Laissez vide la colonne node ou définissez une année de début postérieure à l’étude.
- Cellules vides = 0.0. Pour PV la nuit, entrez 0.000001.
- Colonnes inutiles peuvent être omises dans les fichiers CSV.

**Q : Comment analyser les sorties ?**  
R :

- Vérifiez l’optimalité du solveur.
- Si non optimal, relâchez les contraintes strictes.
- Vérifiez les fichiers de bilan.
- Explorez les résultats par zone si les résultats globaux sont incohérents.

---

## 🧰 InfraFair

**Q : Exigences système ?**  
R : Aucune. Fonctionne avec toute machine ayant Python ≥ 3.8.

**Q : Comment installer InfraFair ?**  
R : Une fois Python installé :  
`pip install InfraFair`

**Q : Comment exécuter InfraFair ?**  
R : Deux options :

- Recherchez l’installation avec : `pip show InfraFair`
- Ou utilisez dans un script :

```python
from InfraFair.InfraFair import InfraFair_run
InfraFair_run()
```

**Q : Quelles données d'entrée sont requises ?**  
R :

- Carte de flux, injections/retraits
- Données spécifiques par actif
- Liste complète : [Documentation](https://infrafair.readthedocs.io/en/latest/7_Input_Data.html)

**Q : Quels actifs sont modélisables ?**  
R :

- Lignes, transformateurs, condensateurs shunt, shifters, disjoncteurs
- Les transfo 3-enroulements doivent être modélisés avec 3 lignes et nœud virtuel

**Q : Format spécifique ?**  
R : Oui. Deux fichiers `.xlsx` avec noms de colonnes définis.  
Modèle : [Exemple GitHub](https://github.com/IIT-EnergySystemModels/InfraFair/blob/main/Examples/EU_ex)

**Q : Sur quels réseaux s’applique InfraFair ?**  
R : Tous : électricité, gaz, chaleur, hydrogène.  
Flux et sources/puits nécessaires par nœud.

---

## 🚗 EV-PV

**Q : Comment installer EVPV ?**  
R : Suivez le [guide d'installation](https://evpv-simulator.readthedocs.io/en/latest/user_guide/installation.html). Une fois Python installé, utilisez `pip`.

**Q : Premiers pas ?**  
R :

- Lire la documentation sur [ReadTheDocs](https://evpv-simulator.readthedocs.io), tutoriels YouTube, plateforme OM4A  
- Lancer l’exemple Addis Ababa Simple

**Q : Comment exécuter EVPV ?**  
R : Deux options :  
1. Mode basique : ligne de commande  
2. Mode avancé : comme module Python  
Voir [ReadTheDocs](https://evpv-simulator.readthedocs.io) pour plus de détails.

**Q : Quelles données d’entrée ?**  
R :

- Fichier de config
- Fichier GeoJSON de la région
- Fichier TIFF population résidentielle
- Deux fichiers CSV : lieux de travail et POI

**Q : Temps d'exécution ?**  
R : Varie selon :

- Nombre de zones de trafic
- Utilisation d’OpenRouteService
- Nombre de VE
- Nombre de jours simulés

Référence : Addis Ababa < 3 min sur un portable standard.

**Q : Détails de la méthodologie ?**  
R : Voir [ReadTheDocs](https://evpv-simulator.readthedocs.io) et [article](https://arxiv.org/pdf/2503.03671).

**Q : Plusieurs types de systèmes PV par localisation ?**  
R : Non. Un seul type par simulation.

**Q : Résolution spatiale maximale ?**  
R :

- Pas de limite stricte
- Plus haute résolution = plus long
- Le modèle gravitaire peut mal fonctionner à très fine résolution
- Les données doivent être disponibles à la résolution voulue

**Q : Visualisations supplémentaires prévues ?**  
R : Non. Mais :

- Les sorties peuvent être visualisées avec Excel ou autres outils  
- Les résultats spatiaux sont déjà en HTML interactif  
- L’intégration future avec l’outil SIG OM4A est prévue
