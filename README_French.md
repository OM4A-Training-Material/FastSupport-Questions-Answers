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

**Q : Existe-t-il des exigences spécifiques au système d’exploitation pour exécuter InfraFair ?**  
R : Non. InfraFair peut être exécuté sur toute machine disposant de Python (version supérieure à 3.8). La seule exigence est donc d’avoir Python installé.

**Q : Comment installer InfraFair ?**  
R : Le moyen le plus simple d’installer InfraFair, après s’être assuré que Python est installé, est d’utiliser la commande pip suivante dans l’invite de commande : `pip install InfraFair`.

**Q : Comment exécuter InfraFair ?**  
R : Pour exécuter InfraFair, vous pouvez soit localiser le code principal sur votre machine via la commande : `pip show InfraFair`, soit appeler la fonction principale `InfraFair_run()` dans votre script Python.  
Dans ce dernier cas, vous devez importer la fonction à l’aide de cette ligne de code :  
`from InfraFair.InfraFair import InfraFair_run`.  
Dans les deux cas, InfraFair doit être installé avec la commande pip : `pip install InfraFair`.

**Q : Quel type de données d’entrée InfraFair nécessite-t-il ?**  
R : InfraFair nécessite une carte des flux dans tous les actifs du réseau ainsi que les injections et retraits de tous les nœuds du réseau. Ces informations peuvent être obtenues à partir d’une résolution de l’optimisation du réseau (par exemple, avec OpenTEPES). InfraFair requiert également des données sur les actifs modélisés, comme le coût de chaque actif à répartir.  
La liste complète des données d’entrée est disponible ici : [https://infrafair.readthedocs.io/en/latest/7_Input_Data.html](https://infrafair.readthedocs.io/en/latest/7_Input_Data.html).

**Q : Quels types d’actifs peuvent être modélisés avec InfraFair ?**  
R : Tout actif par lequel l’énergie circule et qui connecte deux bus peut être modélisé. Cela inclut les lignes électriques, les transformateurs à deux ou trois enroulements, les condensateurs et réactances shunt, les transformateurs déphaseurs, et les disjoncteurs. Pour les transformateurs à trois enroulements, il faut les modéliser comme trois lignes connectées à un nœud virtuel.

**Q : InfraFair exige-t-il un format spécifique pour les données d’entrée ?**  
R : Oui. InfraFair attend les données dans deux fichiers Excel (.xlsx). Le premier contient les données réseau, le second des variables d’entrée nécessaires au modèle. Les noms de colonnes doivent respecter les conventions du code.  
Un exemple de modèle est disponible ici : [https://github.com/IITEnergySystemModels/InfraFair/blob/main/Examples/EU_ex](https://github.com/IITEnergySystemModels/InfraFair/blob/main/Examples/EU_ex).

**Q : Sur quels réseaux InfraFair peut-il être appliqué ?**  
R : Tous les réseaux d’énergie où l’énergie se déplace d’un point à un autre. Cela inclut l’électricité, le gaz, la chaleur, et potentiellement l’hydrogène. Il faut fournir les flux dans les lignes ou canalisations, ainsi que les injections/sources et retraits/puits pour chaque point du réseau.

**Q : Quelles technologies de production sont acceptées par InfraFair ?**  
R : Toutes. InfraFair est indépendant de la technologie de production. Il lui suffit de connaître la quantité d’électricité produite à chaque nœud.

**Q : Combien de temps faut-il pour exécuter InfraFair et obtenir les résultats ?**  
R : Cela dépend de nombreux facteurs : puissance de la machine, taille du réseau, nombre de snapshots, résultats à exporter.  
Des exemples sont présentés dans l’article de référence : [https://doi.org/10.1016/j.softx.2025.102069](https://doi.org/10.1016/j.softx.2025.102069).

**Q : Que se passe-t-il si les données d’entrée sont incomplètes ?**  
R : La gestion des données incomplètes n’est pas prise en charge. Toutes les données obligatoires doivent être fournies intégralement pour exécuter InfraFair.

**Q : Quelle technologie est utilisée pour le regroupement des données ?**  
R : Le regroupement est simple, sans complexité technique. Tous les agents (résultat horizontal) ou actifs (résultat vertical) appartenant à un même groupe (par ex. pays) sont simplement additionnés.

**Q : Quelle communauté d’utilisateurs peut utiliser InfraFair ?**  
R : InfraFair est un outil d’aide à la décision destiné principalement aux régulateurs de l’énergie. Il peut aussi être utilisé par les chercheurs, les décideurs politiques, et la communauté élargie des modélisateurs et parties prenantes du secteur.

**Q : Comment lire le tableau de sortie "SO joint overall network usage cost per SO.xlsx" ?**  
R : Les lignes représentent les actifs réseau de chaque opérateur, les colonnes les utilisateurs du réseau. Chaque cellule indique combien les utilisateurs (colonne) doivent payer pour utiliser les actifs de l’opérateur (ligne). La diagonale indique ce que les utilisateurs doivent à leur propre opérateur.

**Q : InfraFair permet-il de faire une répartition des coûts ?**  
R : Oui. InfraFair répartit les coûts des actifs réseau (au niveau national ou régional) en fonction de l’utilisation attendue par les utilisateurs.

**Q : Le traitement des données dans InfraFair implique-t-il une normalisation ?**  
R : Non. Aucune normalisation n’est incluse. Elle peut être faite après, à des fins de comparaison. Ce n’est pas nécessaire pour l’allocation des coûts.

**Q : Quelle est l’étendue des données acceptées par InfraFair ?**  
R : InfraFair ne limite pas la taille des données, mais les fichiers Excel ont une limite : 16 384 colonnes et 1 048 576 lignes.

**Q : InfraFair applique-t-il un regroupement/clustering des données ?**  
R : Non. Si un regroupement est souhaité, il doit être effectué en amont. Le modèle accepte des snapshots représentatifs avec des pondérations appropriées.

**Q : Comment InfraFair gère-t-il les données d’amplitudes très différentes ?**  
R : Pas de normalisation. Les unités doivent être cohérentes (par ex. tout en MW). InfraFair ne vérifie pas la cohérence des unités : une ligne en MW et une autre en kW n’est pas acceptable.

**Q : Quel solveur est requis ?**  
R : Aucun. InfraFair n’est pas un solveur d’optimisation. Il utilise simplement la bibliothèque NumPy de Python pour faire les calculs.

**Q : InfraFair nécessite-t-il des caractéristiques spécifiques du système ?**  
R : Non. Il fonctionne sur tout système avec Python ≥ 3.8. Il peut fonctionner avec une version plus ancienne, mais l’installation doit alors se faire manuellement. Il fonctionne sous Windows, Linux et Mac.

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
