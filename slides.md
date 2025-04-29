---
marp: true
paginate: true
transition: push
footer: "© 2025 Bertrand Florat – CC BY-SA 4.0"
style: |
  section {
    width: 1280px;
    height: 720px;
    font-size: 28px;
  }
  @page {
    size: 1280px 720px;
    margin: 0;
  }
  section .admonition {
    border-left: 4px solid #999;
    padding: 0.75em 1em;
    margin: 1.5em 0;
    border-radius: 4px;
    background-color: #f9f9f9;
    font-size: 0.80em;
  }
  section .admonition.tip {
    border-color: #2ecc71;
    background: #f0fff0;    
  }
  section .admonition.warning {
    border-color: #e67e22;
    background: #fffaf0;
  }
  section .admonition.info {
    border-color: #3498db;
    background: #f0f8ff;
  }
  section.small {
    font-size: 1.6em;
  }  
  section.smaller {
    font-size: 1.4em;
  }
---

<!--
backgroundImage: url('./images/cover.png')
backgroundSize: cover
color: white
-->

# Introduction au DevSecOps

## Université de Nantes, MIAGE, M2

Ce document est sous licence [Creative Commons Attribution - Partage dans les Mêmes Conditions 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/deed.fr) (CC BY-SA 4.0)

---
<!--
backgroundImage: none
color: #555555
-->
# 🤝 Contribuer à ce support

Pousser une Pull Request [ici](https://github.com/bflorat/cours-devsecops.github.io/pulls), ce support est _as code_ (sources en Markdown).

<div class="admonition tip">
  💡 <strong>Note :</strong> Toutes les contributions sur le fond comme sur la forme sont appréciées.

</div>

---

# 🧭 Séance 1 – Panorama des architectures modernes & fondations du DevSecOps (1h20)

* 1 - Rappel sur les typologies d'architectures modernes
* 2 - Rappel sur les ENF
* 3 - Contexte des Organisations Traditionnelles
* 4 - DevOps : culture, principes et objectifs
* 5 - Bonnes pratiques DevOps (architecture et livraison)
* 6 - Le DevSecOps

---

# 1.1 Rappel sur les typologies d'architectures modernes

---

<!-- _class: small -->

### Le monolithe (années 1990 - ) 
![bg left:40% 100%](./images/typologie-monolithe-03.svg)

* Applications Web (Server Side Rendering)
* Unité de déploiement unique: Toute l'application est déployée comme un seul bloc
* Base de code commune: Tous les modules partagent le même codebase
* Couplage fort: Les composants sont étroitement liés et interdépendants
* En général, découpage en couches au sein d'un seul tiers

---

## Le monolithe : avantages / inconvénients 

<!-- _class: small -->

* ✅ **Web**: très simple à déployer
* ✅ Architecture **simple**
* ✅ **Technologies homogènes**: Utilisation généralement d'un seul langage/framework
* 🤔 **Vendor Locking** selon les technologies retenues mais va dans le bon sens (ex: JEE)
* 🤔 **Scalabilité** verticale ET horizontale possible mais globale et limitée pour les BDD
* ⚠️ **Difficile à maintenir** (couplage fort, code complexe)
* ⚠️ **Lourd à démarrer / déployer**
* ⚠️ Difficile à tester
* ⚠️ Collaboration difficile (conflits de merge...)
* ⚠️ **Stack technologique** : presque impossible à migrer (il faut tout réécrire)

---

## Le n-tiers (années 2000 - ) 

<!-- _class: smaller -->

![bg left:40% 100%](./images/typologie-n-tiers-04.svg)

* Applications Web (Server Side Rendering)
* Proche du monolithe mais unité de déploiement par tiers (en général, un tiers présentation / un tiers service / un tiers BDD)
---
<!-- _class: smaller -->

## Le n-tiers : avantages / inconvénients 

* ✅ **Architecture simple**
* ✅ **Scalabilité:** Verticale ET horizontale (mais limitée sur les BDD). 
* ✅ **Scalabilité individuelle** de chaque tiers (ex: 2 serveurs de présentation, 3 serveur de service)
* ✅ **Découplage** présentation / services
* ✅ **RH** : Possible d'avoir deux équipes : une frontend et une backend
* 🤔 **Testabilité** : Plus simple à tester (ex: bouchonnage du tiers services)
* 🤔 **Vendor Locking** : Selon les technologies retenues mais va dans le bon sens (ex: JEE)
* 🤔 **Maintenance** quelque fois difficile à maintenir (couplage fort, code complexe dans chaque tiers)
* 🤔 **Déploiement**: Peut être lourd à démarrer / déployer
* ⚠️ **Stack technologique** : presque impossible à migrer (il faut tout réécrire)
* ⚠️ **Pas de réutilisation** des services par d'autres applications

---


## Le micro-services (années 2010 - ) 

<!-- _class: small -->

![bg left:40% 100%](./images/typologie-n-tiers-04.svg)


* Découpage par services
* Organisation autour des capacités métier
* Produits plutôt que projets
* Points de terminaison intelligents et tuyaux simples
* Gouvernance et gestion des données décentralisées
* Automatisation de l'infrastructure
* Conception pour tolérer les défaillances
* Conception évolutive
 
---
<div class="admonition tip">
  💡 <strong>Note :</strong> L'architecture microservice a été précédée du <strong>SOA</strong> (Service-Oriented Architecture) dans les années 2000. 
  
  * Le SOA est une architecture similaire mais s'appuie en général sur un Enterprise Service Bus (ESB) centralisé En microservices et non des appels directs (même on trouve en microservices de plus en plus d'API Gateway). 

  * En SOA, les WebServices se basaient sur le standard SOAP (et non REST, GraphQL ou gRPC).
  
  * Les WebServices étaient principalement développés en Java (Java Enterprise Edition = JEE) et non multi-languages (polyglotte).

  * Le SOA était principalement représenté par des solutions propriétaires complexes et coûteuses.

</div>

---
<!-- _class: smaller -->

## Le micro-services : avantages / inconvénients 

* ✅ **Déploiement indépendant** de chaque service : maj plus fréquentes et ciblées
* ✅ **Scalabilité verticale et horizontale granulaire**
* ✅ **Autonomie/parallélisation des équipes** : chaque équipe peut développer et déployer ses services
* ✅ **Facilité d'évolution** : les services peuvent être remplacés, réécrits ou supprimés 
* ✅ **Réutilisation des services** entre applications
* ✅ **DEV plus simple** : petits périmètres, plus faciles à comprendre et à tester
* ✅ **Peu de vendor locking** : technologies Open Source et standard principalement
* 🤔 **Code polyglotte** : **avantage RH** mais aussi un **risque sur la maintenabilité**
* 🤔 **Surcoût en infrastructure** : orchestrateurs, API Gateway, monitoring, observabilité...
* 🤔 **Tests d'intégration** plus simples mais **tests système** plus complexes
* ⚠️ **Architecture complexe** : code plus simple mais intégration plus complexe et nécessite des mécanismes robustes et une gestion des erreurs (rejeux...)
* ⚠️ **[Surdimensionné](https://martinfowler.com/bliki/MicroservicePrerequisites.html)** pour certaines organisations (nécessite DevOps, CI/CD, observabilité, résilience…)
* ⚠️ **Consistance des données plus difficile** : chaque service gère sa propre base → cohérence eventualisée

---


## Le serverless (années 2015 - ) 

<!-- _class: small -->
![bg left:40% 100%](./images/typologie-serverless-06.svg)


[Traits principaux](https://www.thoughtworks.com/insights/blog/traits-serverless-architecture/) (source: Thoughtworks) :
serverless :
* Faible Barrière à l'entrée
* Sans hôtes (que l'on gère)
* Sans états
* Élasticité
* Distribué
* Orienté événements


---
<!-- _class: smaller -->

## Le serverless : avantages / inconvénients 

* ✅ **Plus de scalabilité à gérer, élasticité automatique**, mais **latence à froid**.  
* ✅ **Plus d'infrastructure à gérer** et nécessitant des compétences élevées, avec **HA native**.  
* ✅ **Autonomie / parallélisation des équipes** : chaque équipe peut développer, tester et déployer son propre service. 
* ⚠️ **Vendor-locking** très élevé (forte dépendance aux GAFAM)  
* 🤔 **Coût raisonné** en théorie (paiement à l'utilisation) mais impose une surveillance importantes pour éviter les surcoûts  
* 🤔 Développement en théorie rapide et simple, mais **débogage complexe** et **risque sur la cohérence globale**  
* ⚠️ **Surface d'attaque** plus large, surtout si on multiplie les fournisseurs  
* ⚠️ **Architecture complexe** : code plus simple mais intégration plus complexe, nécessitant des mécanismes robustes et une gestion des erreurs (rejeux...).  
* ⚠️ **Consistance des données plus difficile** : chaque service gère sa propre base → cohérence eventualisée

---

<div class="admonition tip">
  💡 <strong>Note :</strong> Les architectures microservices et serverless représentent **l'état de l'art** au milieu des années 2020.

  * Le serverless est <strong>peu adapté</strong> aux environnements <strong>souverains</strong> (administrations) ou <strong>sensibles</strong>

  * On le rencontre plus fréquemment dans les <strong>structures agiles</strong> (startups, PME) ou celles disposant de <strong>moins d’exigences techniques internes</strong>

  * Le serverless et les microservices sont souvent <strong>utilisés de façon complémentaire</strong>. Ils ne s'opposent pas.

  * À titre personnel, je recommanderais pour les applications de gestion de taille moyenne à importante de **limiter le serverless aux fonctions périphériques** (envoi d’emails, traitement de fichiers, BI...)
</div>

---

Plus de détail : 

[Cours de M1, thème « typologies d'architectures »](https://public.florat.net/cours_miage/support-CoursArchiSolution.pdf) 

---
# 1.2 Rappel sur les ENF

<!-- _class: small -->

### 🛠️ ENF d'exploitabilité

- **Robustesse** : Capacité du système à fonctionner correctement malgré des erreurs
- **Résilience** : Aptitude à se remettre automatiquement d'une panne ou d’un incident
- **Observabilité** : Possibilité de diagnostiquer l’état du système via logs, métriques et traces

---

### 🚀 ENF de performances

- **Scalabilité** : Capacité à maintenir les performances en augmentant les ressources
- **Rapidité**: Aptitude d’un système à présenter un temps de réponse (TR) acceptable pour un niveau charge donné
- **Élasticité** : Aptitude d’un système à provisionner /dé-provisionner automatiquement des ressources en fonction de la charge afin de conserver des temps de réponses acceptables tout en optimisant le coût

---

### 🔐 ENF de sécurité

- **Disponibilité** : Le système est accessible et fonctionnel quand nécessaire
- **Confidentialité** : Les données sont protégées contre les accès non autorisés
- **Intégrité** : Les données ne sont ni altérées ni corrompues

---

<div class="admonition tip">
  💡 <strong>Note :</strong> Voir au besoin <a href='https://public.florat.net/cours_miage/support-CoursArchiSolution.pdf'>le cours de M1</a> sur les Exigences Non Fonctionnelles (ENF).
</div>


---

## 1.3 Contexte des Organisations Traditionnelles

![bg left:40% 100%](./images/dev-et-ops.png)

- **Structure Organisationnelle** : Hiérarchique et cloisonnée par rôles :
  - **Devs** : Développement de nouvelles fonctionnalités 
  - **Ops** : Gestion de l'infrastructure et des déploiements 

**Processus** : Souvent rigides et basés sur des cycles longs

---

## Équipes de Développement (Devs)

- **Objectif Principal** : Livrer rapidement de nouvelles fonctionnalités
- **Priorités** :
  - **Innovation** : Introduire de nouvelles fonctionnalités et améliorations
  - **Réactivité** : Adapter rapidement le produit en fonction des retours utilisateurs
  - **Cycle de Développement Court** : Utiliser des méthodologies agiles
- **Défis** :
  - Risque d'introduire des bugs ou des instabilités
  

---

## Équipes d'Opérations (Ops)

- **Objectif Principal** : Assurer la stabilité et la sécurité des systèmes
- **Priorités** :
  - **Fiabilité** : Garantir que les applications fonctionnent sans interruption
  - **Sécurité** : Protéger les systèmes contre les menaces
  - **Maintenance Préventive** : Effectuer des mises à jour pour éviter les pannes
- **Défis** :
  - Gérer les changements fréquents tout en maintenant la stabilité
  

---

## Défis de la Collaboration Devs-Ops

- **Silos Organisationnels** : Communication limitée entre équipes
- **Processus Lents** : Déploiements longs et complexes (Time To Market = **TTM allongé**)
- **Résistance au Changement** : Culture d'entreprise parfois réticente à l'innovation
- **Impact sur l'Innovation** : Difficulté à répondre rapidement aux besoins du marché

---

# 1.4 DevOps : culture, principes et objectifs

![bg left:40% 100%](./images/devops.png)

Livrer des logiciels **plus rapidement**, **plus fréquemment** et **plus fiablement**.

<div class="admonition tip">
  💡 Le DevOps est un <strong>ensemble de pratique agiles appliquées à l'intégration</strong> et non à la gestion de projet (comme Scrum) ou au code (comme XP)
</div>

---

## Convergence avec DevOps

- **DevOps** : Aligner les objectifs des Devs et des Ops.
- **Avantages** :
  - **Amélioration de la Communication** : Réduction des silos.
  - **Déploiements Plus Rapides et Sécurisés** : Automatisation avec CI/CD
  - **Culture de Collaboration** : Responsabilité partagée pour la qualité et la stabilité


---

## les piliers du succès

![](./images/piliers.png)

---

## Passer de cette organisation :  

![](./images/avant-devops.png)

---

## A cette organisation (two pizza teams) : 

![width:500px](./images/two-pizza-teams.png)

* **Équipes petites** (5 à 8 personnes max), **autonomes**, **multi-compétences**
* **Responsables** à la fois du code et **de l’exploitation**
* **Communication fluide** entre Dev et Ops

---
## Le cycle d'amélioration continue DevOps

![bg left:40% 100%](./images/cycle-devops.png)

---

## Étapes clés du cycle DevOps

<!-- _class: small -->

📝 Plan : prioriser les besoins (fonctionnels et non fonctionnels)

💻 Code : Écrire le code source et les tests unitaires — souvent collaboratif (Git, MR…)

🧱 Build : Compiler, empaqueter l’application et générer des artefacts (binaries, containers…)

✅ Test : Exécuter des tests automatisés (unitaires, d’intégration, de sécurité…)

🚀 Release : Préparer la MEP, valider le déploiement dans des environnements de test

📦 Deploy : Déployer automatiquement dans l’environnement de production (CD, canary…)

⚙️ Operate : Bon fonctionnement du service (patchs, ajouter ressources, modifier configuration) 

📊 Monitor : Observer performances, superviser, collecter métriques, détecter anomalies

---

## Comment mieux collaborer ?

<!-- _class: smaller -->

🌐 **Penser système, pas équipe isolée**
- Communication multi-équipes via messagerie instantanée de préférence

💬 **Feedback**
- Source d’information commune (ex: daily)

🚀 **Innovation et amélioration continue**
- Ateliers

🤝 **Partager les responsabilités**

🔄 **Casser les carcans**
- Les devs exploitent (**You build it, you run it** » Amazon)
- Les ops codent (IaC : Infrastructure as Code)

---

## Qu’est-ce qu’on entend par automatisation ?

🔄 **CI : Intégration Continue**
✅ Tests automatisés (TU, TI, E2E, spécifications exécutables...)
📦 Livraison continue
🏗️ **Infrastructure as Code (IaC)**: Provisioning des serveurs et composants
🌟 **GitOps** : Si ce n’est pas dans Git, ça n’existe pas
🚀 **CD (Livraison Continue voire Déploiement Continu)**

---

## 🔗 Relations entre DevOps et Cloud-native

<!-- _class: small -->

> DevOps et Cloud-native sont **étroitement liés et complémentaires**

🔧 DevOps = **Méthode et culture**

☁️ Cloud-native = Architecture des **applications à déployer sur un cloud**
- **Microservices**, conteneurs, orchestration (ex. Kubernetes)
- **Scalabilité**, tolérance aux pannes, portabilité
- **Infrastructure dynamique** et éphémère


DevOps **est un prérequis naturel** au cloud-native : impossible d’exploiter des architectures distribuées modernes **sans automatisation et collaboration**

Cloud-native **amplifie les bénéfices de DevOps** : scalabilité automatique, testabilité, déploiement continu, observabilité native

---

## 🐾 Pets vs 🐄 Cattle : deux visions de l'infrastructure

Cette métaphore illustre le **changement de culture** entre l’infrastructure traditionnelle (manuelle) et l’infrastructure cloud-native (automatisée, jetable, scalable).

---
<!-- _class: smaller -->

| **Pets (animaux de compagnie)**   | **Cattle (bétail)**                        |
|-----------------------------------|---------------------------------------------|
| Nommés individuellement (ex: `svr_bdd`) | Identiques et numérotés (ex: `node-001`, `node-002`) |
| On les soigne, on les répare      | On les remplace automatiquement (permet de repartir d'une situation connue rapidement)            |
| Configuration manuelle            | Créés par script / IaC                      |
| Chers à maintenir                 | Jetables, scalables, automatisés            |
| Tendance "on-premise"             | Tendance cloud / conteneurs / DevOps        |


<div class="admonition info">
  ℹ️ L’approche <strong>"Cattle"</strong> favorise la <strong>scalabilité, la résilience et l’automatisation</strong>, au cœur des pratiques <strong>cloud-native et DevOps</strong>.
</div>

---

## En résumé: un mix de changements architecturaux, organisationnels et humains

![width:600px](./images/shift-pratiques.png)

---
<!-- _class: small -->

**🧠 Quiz !** Niveau DevOps de la pratique (de 0 à 5) :
- 1 : Les ops fournissent aux devs un **dashboard Zabbix** mais seuls les Ops reçoivent les alertes par mail
- 2 : Un **canal de messagerie instantanée** a été mis en place pour remonter les problèmes de PROD  mais la plupart du temps les Ops ne signalent que les indisponibilités programmées
- 3 : Chaque équipe produit dispose d'un.e **DevOps dédié** qui automatise tous les aspects du  cycle de vie (build déploiement, alerting...) et dispose des droit de PROD sur le provider Cloud
- 4 : Les modules sont **conteneurisés en Docker** mais lancés manuellement (pas d'orchestrateur)
- 5 : L’équipe de Dev rédige un **document d’installation manuelle en Word** et l’envoie aux Ops par mail lorsque la version du produit est publiée
---


## 🔒 1.5 Bonnes pratiques DevOps (architecture et livraison)


---

### ⚙️ Indépendance de la Configuration

**Principe :**  
Ne jamais embarquer de **configuration plate-forme dépendante** dans les paquets applicatifs.

#### Pourquoi ?

- ❌ Risque de couplage fort avec l'environnement
- ❌ Difficulté à déployer sur plusieurs cibles (dev, prod, cloud, etc.)
- ❌ Impossibilité de reproduire des déploiements de manière fiable
- ❌ Gaspillage d'espace disque pour stocker les livrables

---

#### ⚙️ Bonne pratique

- ✅ Séparer **binaire applicatif** et **configuration d'environnement**
- ✅ Utiliser des mécanismes externes (fichiers de configuration, **variables d'environnement**, systèmes de configuration)
- ✅ Favoriser des déploiements **portables** et **prévisibles**

---

### 🤖 Automatiser (presque) tout

**Principe :**  
Automatiser le **déploiement**, le **rollback**, le **provisionnement**, etc.

#### Object

- ✅ Gagner en **fiabilité** et en **rapidité**
- ✅ Réduire les erreurs humaines
- ✅ Faciliter les répétitions et les rollbacks

---

#### ⚠️ Attention à l'overkill

- Pas besoin d'automatiser **absolument tout** !
- ✅ Autoriser quelques actions manuelles **quand le coût d'automatisation est supérieur au gain attendu**

---

## 🔀 Organisation en branches recommandée

- Approche Trunk-Based Development (**TBD**) + **FF** (Feature Flags)
- **Une seule branche** (ex : `main`)  
- Branches temporaires pour les **Merge Requests (topics)**  uniquement (durée de vie de quelques heures à quelques jours)
- Feature-Flags pour activer/désactiver facilement les nouvelles fonctionnalités.
- Objectif : simplifier l'intégration, **réduire les conflits** et écarts
- Configurer le **Fast-Forward only** (impose les rebases) pour faciliter la lecture de l'historique. 

---

### 🐤 Canary Testing

**Définition :**  
Déploiement progressif d'une nouvelle version logicielle à une fraction restreinte des utilisateurs (les « canaries ») pour détecter rapidement les anomalies.

## Objectifs

- ✅ Détecter précocement les anomalies en prod
- ✅ Minimiser les risques lors des déploiements
- ✅ Réagir rapidement grâce à un monitoring renforcé

---

#### Fonctionnement

1. Déploiement à un groupe restreint (les FF peuvent servir de filtre)
2. Surveillance des métriques clés (erreurs, latence, UX)
3. Extension progressive ou rollback selon les résultats

#### Avantages

- 📌 Limite l’impact d’un incident
- 📌 Feedback rapide et fiable
- 📌 Améliore la confiance et réduit le stress des équipes

---

### 🌑 Dark Deployment

**Définition :**  
Déploiement d'une nouvelle version en production **sans l'exposer** aux utilisateurs finaux.

#### Objectifs

- ✅ Tester l'infrastructure et les performances
- ✅ Identifier les problèmes cachés avant activation
- ✅ Préparer un basculement rapide (feature toggle)

---

#### Fonctionnement

1. Déploiement en "ombre" en parallèle de l'ancien système
2. Surveillance du comportement en production
3. Activation ultérieure via un switch contrôlé (ex: feature flag)

#### Avantages

- 📌 Réduit les risques avant l'exposition
- 📌 Permet des tests réalistes en conditions réelles
- 📌 Améliore la qualité des mises en production

---

### 🔵🟢 Blue-Green Deployment

**Définition :**  
Technique de déploiement où **deux environnements identiques** (Blue et Green) sont utilisés pour minimiser les interruptions.

#### Fonctionnement

1. **Blue** : environnement en production actuel
2. **Green** : nouvelle version déployée en parallèle
3. Test sur Green → bascule du trafic → mise à jour terminée !

---

#### Objectifs

- ✅ Déployer sans downtime
- ✅ Pouvoir revenir rapidement à l'ancienne version en cas de problème
- ✅ Sécuriser les mises en production

#### Avantages

- 📌 Bascule instantanée
- 📌 Rollback facile et rapide
- 📌 Amélioration de la fiabilité et de l'expérience utilisateur

<div class="admonition warning">
  ⚠️ Challenges au niveau des évolutions des modèles de données et de leur compatibilité...
</div>


---

### 🕶️ Shadow Traffic (ou Double Commande)
<!-- _class: smaller -->

**Définition :**  
Technique où **le trafic utilisateur est dupliqué** vers une nouvelle version sans impacter la réponse envoyée.

![bg right width:500px](images/double-commande.svg)


#### Objectifs

- ✅ Valider le comportement de la nouvelle version
- ✅ Comparer les résultats avec l'ancienne version
- ✅ Détecter les écarts sans risque pour les utilisateurs

---

#### Fonctionnement

1. Le trafic réel est envoyé aux deux versions
2. Seule la réponse de la version officielle est utilisée
3. Les réponses sont comparées en interne

#### Avantages

- 📌 Permet de vérifier l'intégration (configuration, tuning...)
- 📌 Tests réalistes en conditions de production
- 📌 Aucune perturbation pour les utilisateurs
- 📌 Détection précoce d'erreurs ou de régressions fonctionnelles

---

## 🚀 GitOps

**Définition :**  
Approche où **Git est la source unique de vérité** pour décrire l'état désiré d'un système, souvent pour du déploiement cloud/Kubernetes.

> **Si ce n’est pas dans Git, ÇA N'EXISTE PAS !**

### Fonctionnement

- Les configurations (infra, apps) sont **stockées dans Git**
- Les modifications sont faites par **pull | merge requests** (PR/MR)

---

### 🚀 GitOps - Avantages

- ✅ Déploiements traçables et auditables
- ✅ Rollbacks facilités
- ✅ Déploiements reproductibles et fiables
- ✅ Séparation claire entre développement et opérations

---

## 🔧 Convention over Configuration (ou 'on rails')

<!-- _class: small -->

**Principe :**  
Privilégier des **standards explicites** et les valeurs par défaut plutôt que laisser de nombreuses options manuelles.

Exemples : 
* Maven qui "opinionalise" la structure des sources
* Comptes de service en dur déductibles par convention (ex: `cs-monapi` pour l'API `monapi`)

#### 🔧 Objectifs

- ✅ Simplifier les décisions techniques
- ✅ Gagner en **productivité** et en **prévisibilité**
- ✅ Réduire les erreurs et les écarts de pratique


---

### ❌ Quelques anti-patterns d'intégration à éviter

#### 🧍‍♂️ Interventions humaines non maîtrisées

- Déploiements manuels, procédures non automatisées  
- Dépendance à des **workflows informels ou oraux**  
- Risques d’erreurs, de non-reproductibilité et de ralentissement

#### ⚠️ Intégration continue défaillante

- **Builds lancés à la main**, sans trigger automatique  
- **Tests trop longs** (> 10 mins) ou instables → développeurs les contournent  
- **Perte de confiance** dans les pipelines CI/CD  
- **Temps de feedback trop élevé** → ralentit la boucle de développement

---

#### 🌀 Chaos dans la gestion de version

- Trop de **branches parallèles** → complexité, conflits, dérives  
- **Absence de tags** -> difficile de retrouver la version qui a été livrée
- **Branches actives longtemps sans rebase** = dette technique

---

#### ↔️ Impédance DEV-PROD

<!-- _class: small -->

![bg left:33% fit](images/works-on-my-machine.png)

- Des **binaries différents** selon les environnements (ex : dev, staging, prod)  
- **Spécificité de l'environnement de DEV** 
  - (ex: développement sous Windows, déploiement sous Linux)
- Génération locale, configuration manuelle, "ça marche chez moi/ **Works on my machine**"  


---

## 1.6 🔒 Le DevSecOps

DevSecOps intègre **la sécurité** dès le début du cycle DevOps, au lieu de l'ajouter à la fin.

C'est l'**évolution naturelle du DevOps** et l'**état de l'art actuel**.

---

### 🔒 Fondamentaux du DevSecOps

<!-- _class: small -->

#### ✅ 1. Intégration de la sécurité dès le départ (Secure By Design)
> La sécurité n’est plus un "étape finale", elle est intégrée dès la conception et le développement.

#### ✅ 2. Culture collaborative Dev + Sec + Ops  
> Les développeurs, les équipes sécurité et les opérations travaillent ensemble, en continu.

#### ✅ 3. Automatisation des contrôles de sécurité  
> Scans de vulnérabilités, tests statiques, politiques de sécurité automatisées dans les pipelines CI/CD.


---


#### ✅ 4. "Shift Left"  
> Détecter les failles **le plus tôt possible**, dès l’écriture du code, pour éviter des corrections tardives coûteuses.

#### ✅ 5. Observabilité et réponse aux incidents  
> Surveillance continue, journaux centralisés, alertes, détection d’anomalies et réponse rapide aux menaces.

#### ✅ 6. Politique de moindre privilège et de séparation des responsabilités  
> Chaque composant n’a que les droits nécessaires à son fonctionnement. Isolation stricte des rôles.

---
<!-- _class: small -->

#### ✅ 7. Sensibilisation à la sécurité dans les équipes  
> Formation continue, bonnes pratiques, revues de code avec une vision sécurité.

#### ✅ 8. Conformité automatisée  
> Intégration de contrôles de conformité (RGPD, ISO, etc.) dans les pipelines et les audits.

---

### 🔄 DevOps vs 🔐 DevSecOps

|               | **DevOps**                            | **DevSecOps**                             |
|---------------|----------------------------------------|-------------------------------------------|
| 🎯 Objectif    | Livrer plus vite et plus souvent       | Livrer vite **et** en toute sécurité       |
| 🧩 Focus       | Automatisation, CI/CD, collaboration   | Sécurité intégrée dans tout le cycle       |
| 🛠️ Pratiques   | CI/CD, Monitoring, IaC, observabilité  | + Scans, tests de sécurité, politique zero-trust |
| 👥 Acteurs     | Dev + Ops                              | Dev + Sec + Ops                            |
| 🕒 Sécurité    | Souvent en fin de cycle                | Intégrée dès le début (Shift Left)         |

---

### ❓ Lequel choisir ?

- ✅ **DevSecOps est une évolution naturelle du DevOps**  
- 🔐 Choisissez **DevSecOps dès que des données sensibles, un contexte réglementaire ou une exposition web** sont en jeu.
- 🛠️ Pour des projets internes simples, DevOps peut suffire (au départ)... mais sécuriser dès le début reste toujours préférable.

<div class="admonition info">
  ℹ️ Aujourd'hui, dans un contexte de plus en plus dangereux (attaques, DDOS, rançongiciels, hameçonnage...),  l'<strong>approche DevSecOps est à privilégier</strong> dans la plupart des cas.
</div>

---

### 🔐 Principes de Secure by Design : sécurité = critère d’architecture comme la performance

<!-- _class: small -->

- **Moindre privilège** : chaque composant ne dispose que des droits strictement nécessaires
- **Séparation des responsabilités** : les fonctions critiques sont isolées pour limiter les impacts
- **Surface d’attaque minimale** : réduction des points d’entrée exposés
- **Défense en profondeur** : plusieurs couches de sécurité superposées
- **Comportement sûr par défaut** : tout ce qui n’est pas explicitement autorisé est refusé
- **Validation stricte des entrées** : toutes donnée externe est considérée comme non fiables
- **Auditabilité** : les actions critiques sont traçables et exploitables en cas d’incident


---

### 🛡️ Défense en profondeur (Defense in Depth)

> Principe fondamental de la sécurité : **multiplier les couches de protection**  
> pour réduire le risque d’intrusion ou de compromission, même en cas de faille.


<div class="admonition info">
  💡 Certaines normes et meilleures pratiques recommandent la <b>diversité technologique</b> (dans la mesure du raisonnable) pour éviter les monocultures technologiques
  <p><p>
  Exemple: utiliser des firewalls de vendeurs différents
</div>

---

#### 🧱 Couches typiques de défense

1. **Contrôles physiques** : data centers sécurisés, badges, portiques, caméras...
2. **Réseau** : firewalls, segmentation, VPN, sécurité des flux (TLS)
3. **Infrastructure** : durcissement des OS, patchs de sécurité, monitoring système
4. **Accès et identités** : authentification forte, RBAC, MFA
5. **Applications** : validation des entrées, protections contre les injections
6. **Données** : chiffrement, gestion des secrets, contrôle d’accès aux bases
7. **Surveillance et réponse** : journaux, alertes, Intrusion Detection System (IDS), Intrusion Prevention System (IPS), plans d’intervention

---


### 🚨 Etude de cas : rôle du DevSecOps dans le cadre d'une CVE majeure ?

**[Log4shell (CVE-2021-44228)](https://nvd.nist.gov/vuln/detail/CVE-2021-44228)** :

**Impact** : Exécution de code à distance (RCE) sur les serveurs vulnérables

**Score CVSS** : 10.0 / 10 (critique)

**Composant affecté** : Log4j 2 (versions < 2.15.0)

**Vecteur** : Chaînes de log contenant des expressions ${jndi:ldap://...} injectées depuis des requêtes utilisateur

**Exploitabilité** : Très simple — aucun accès authentifié requis

---


# 🛠️ Séance 2 – Écosystème technologique : IaC, CI/CD & sécurité (1h20)

* 1 - L'outillage et l'infrastructure DevOps / Cloud Native...
* 2 - Rappel sur les conteneurs
* 3 - Kubernetes : le système nerveux du cloud
* 4 - L'Infrastructure as Code (IaC)
* 5 - La CI / CD

---

## 💡 2.1 L'outillage et l'infrastructure DevOps / Cloud Native...


Voir le [Landscape CNCF ](https://landscape.cncf.io/) (Cloud Native Computing Foundation)

* Un écosystème foisonnant...
* ... en évolution rapide et constante

![](./images/landscape-cncf.png)

---
## 📦 2.2 Rappel sur les conteneurs

> Un **conteneur** est un environnement léger, isolé et portable,  
> permettant d’exécuter une application avec toutes ses dépendances.

### ✅ Caractéristiques

- **Partage le noyau** de l’hôte (contrairement à une VM)
- **Étanche** (processus isolés)
- **Démarrage rapide**, faible empreinte mémoire
- **Image immuable** = mêmes résultats sur tous les environnements
- Facile à versionner, tester, déployer

---
### Containeurs et VMs

![](./images/conteneurs.png)

<div class="admonition info">
  ℹ️ Ne pas opposer VM et conteneurs :

* VM : premier découpage pour grosses machines 
* Les conteneurs tournent très souvent dans des VMs...
* Mais pas toujours (**bare metal**)
</div>

---
### 🖼️ Les images de conteneurs

> Une **image de conteneur** est un **snapshot exécutable** contenant tout le nécessaire pour lancer une application.

#### ✅ Norme de référence : **OCI (Open Container Initiative)**

- Standard ouvert pour les **formats d’image** et les **runtimes**
- Assure la **portabilité** entre outils : Docker, Podman, containerd, etc.

---

### 🧅 Notion d’"onions" (couches)

- Une image est construite **par couches successives**
- Chaque instruction (RUN, COPY…) ajoute une **nouvelle couche**
- Les couches sont **en cache** et **partagées** entre images
- On peut **reconstruire partiellement** l’image si une couche change
- Consolidées sous la forme d'une archive (`.tar.gz`) 
- **Publiées (push) dans un registre d'image** (ex: Artifactory, GitLab Container Registry, GitHub Container Registry, ...)  pour pouvoir être récupérées (pull)

---

### 🐳 Exemple de Dockerfile (Node.js)

```dockerfile
# Image de base officielle
FROM node:18-slim

# Répertoire de travail
WORKDIR /app

# Dépendances
COPY package*.json ./
RUN npm install

# Code source
COPY . .

# Port exposé
EXPOSE 3000

# Commande de démarrage
CMD ["npm", "start"]
```

---

### 🧱 Exemples d’outils de construction et execution des conteneurs

- **Docker** : création et exécution de conteneurs
- **Podman** : alternative sans daemon
- **Containerd / CRI-O** : autres moteurs d’exécution de haut niveau (gèrent le cycle de vie, le pull, l’exécution des conteneurs)
- **Kaniko**/**Buildah** : construction d’images OCI en userspace (hors containeur)
- **runc** (par défaut, écrit en Go) / **crun** (écrit en C) / **youki** (en Rust) : moteurs d’exécution bas niveau

---

## ☸️ 2.3 Kubernetes : le système nerveux du cloud

![bg left](./images/k8s.png)

> “**Kubernetes (K8s)** is an open-source system for automating deployment, scaling, and management of containerized applications.”  
> — [kubernetes.io](https://kubernetes.io)

---

### ✨ Kubernetes : un projet open source majeur

- **Amorcé par Google en 2014**
- Inspiré de **Borg** (orchestrateur interne de Google)
- **Donné à la CNCF** en 2015
- Principaux contributeurs : Google, Red Hat, VMware, Microsoft, Amazon

#### 📊 Chiffres clés

- **2ᵉ projet open source** le plus actif (après Linux)
- **1500+ contributeurs actifs**
- **70k+ stars** sur GitHub
- **4000+ entreprises utilisatrices** 


---

# Pourquoi Kubernetes ?

- 💪 Orchestration des conteneurs à grande échelle
- 🌐 Portabilité cloud (AWS, Azure, GCP, on-premise)
- 🛠️ Communauté et écosystème très riches


---

### 🧱 Une infrastructure **managée au-dessus** de l’infrastructure

- 🧊 Conteneurs = **unités de calcul** (compute)  
- 🗄️ Volumes = **stockage persistant**  
- 🌐 Services/Ingress/Network Policies = **réseau intelligent et sécurisé**

➡️ Kubernetes orchestre **tout automatiquement**

---

### 🚀 Développement & exploitation cloud-native

- Déploiement **déclaratif** (YAML, GitOps)  
- **Scalabilité automatique** selon la charge  
- **Résilience intégrée** : redémarrage, réplication  
- **Observabilité native** (logs, métriques, events)

---

### 🌩️ Kubernetes = moteur des apps cloud-native

- Déploiement continu, microservices, tolérance aux pannes  
- Utilisé par : Google, Spotify, BlaBlaCar, OVH, etc.  
- Standard de fait pour les plateformes modernes (AKS, EKS, GKE...)

---

### 🧩 Architecture de K8S

![width:700px](images/kubernetes-cluster-architecture.svg)

Source: https://kubernetes.io/docs/concepts/architecture/

---

### 📦 Exemple de déploiement Kubernetes

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: webapp
  template:
    metadata:
      labels:
        app: webapp
    spec:
      containers:
        - name: nginx
          image: nginx:1.25
          ports:
            - containerPort: 80
```

---

### 🛠️ K9S, un navigateur Kubernetes

![width:700px](./images/k9s.png)

<div class="admonition info">
  ℹ️ Outil presque indispensable et permettant d'accélerer grandement la gestion d'un cluster K8S
</div>
---

## 🏗️ 2.4 L'Infrastructure as Code (IaC)

> L’Infrastructure as Code permet de **définir l’infrastructure (serveurs, réseaux, bases, etc.) via du code**, versionnable et automatisable.

---

### ✅ Objectifs

- Déployer des environnements **de façon reproductible**
- **Versionner** l’infrastructure (comme du code)
- **Automatiser** la création, modification et suppression de ressources
- Réduire les **erreurs manuelles** et les écarts entre environnements

---

## 🧭 La notion d’état désiré

> En Infrastructure as Code, on décrit **l’état final attendu** de l’infrastructure,  
> et non les étapes pour y parvenir

- L’**état désiré** représente ce que **l’infrastructure doit être** :  
  types de ressources, configurations, relations
- L’outil IaC (ex : Terraform) se charge de **comparer l’état réel** à l’état désiré  
  et applique les **changements nécessaires**

---

### 🛠️ Exemples

- "Je veux **2 serveurs** EC2 avec 8 Go de RAM"
- "Je veux un **load balancer** devant mes pods Kubernetes"
- "Je veux une **base PostgreSQL** avec sauvegarde quotidienne"

---

### 🔁 Avantages

- **Automatisation** des changements
- **Détection des dérives** entre ce qui est déployé et ce qui est attendu
- **Idempotence** : rejouer le code n’a pas d’effet s’il n’y a rien à changer

---

### 🧠 En résumé

> Les outils IaC ne spécifient pas *comment faire*, mais *ce que l’on veut obtenir* 

<div class="admonition info">
  ℹ️ Tous les outils d'IaC, quelle que soit leur niveau d'abstraction (voir plus loin) utilisent ce concept mais à des niveaux différents.

  * Dans un déploiement **Kubernetes**, ce sera par exemple « je désire au moins **cinq instances** (pods) de mon application »
  * Dans un **playbook Ansible**, ce sera : « Je veux que le fichier /etc/xyz.conf existe" ou "le **service SystemD ABC** est démarré »
</div>


---

## 🛠️ Exemples d'outils IaC orientés provisionnement

<!-- _class: smaller -->

| Outil               | Éditeur / Origine         | Description principale                                 |
|---------------------|---------------------------|--------------------------------------------------------|
| **Terraform**       | HashiCorp                 | Provisionnement multi-cloud déclaratif en HCL         |
| **Pulumi**          | Pulumi Corp.              | IaC en langages classiques (Python, TS, Go…)          |
| **CloudFormation**  | Amazon Web Services (AWS) | Déploiement d’infra AWS en JSON/YAML                  |
| **ARM / Bicep**     | Microsoft (Azure)         | Provisionnement pour Azure (ARM = JSON, Bicep = DSL)  |
| **Deployment Manager** | Google Cloud         | IaC pour GCP avec YAML/Jinja                          |
| **Crossplane**      | Upbound                   | Provisionnement Kubernetes via CRDs                   |


---


 ## 📝 Exemple de fichier Terraform (HCL)

```hcl
provider "aws" {
  region = "eu-west-3"  # Paris
}

resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"  # Amazon Linux 2
  instance_type = "t2.micro"

  tags = {
    Name = "MonServeurWeb"
  }
}
```

---


## 🛠️ Outils IaC orientés Gestion de Configuration

<!-- _class: small -->


| Outil         | Mode                | Particularités                              |
|---------------|---------------------|----------------------------------------------|
| **Ansible**   | Agentless (push)    | Simple, basé sur SSH, YAML déclaratif        |
| **Puppet**    | Agent + serveur     | DSL propre, très utilisé en entreprise       |
| **Chef**      | Agent + serveur     | Basé sur Ruby, flexible mais complexe        |
| **SaltStack** | Push + Pull hybride | Rapide, orienté événements                   |


<div class="admonition info">
  ℹ️ Ces outils permettent de <strong>configurer et maintenir l’état des serveurs</strong>, une fois provisionnés par des outils d'IaC de provisionnement comme Terraform ou Pulumi.
</div>

<div class="admonition info">
  💡 Une <strong>approche conteneurs</strong> (voir plus loin) reste <strong>préférable</strong> si supportée.
</div>


---

## ⚙️ Exemple de fichier Ansible (YAML)

```yaml
- name: S'assurer que nginx est démarré
  hosts: webservers
  become: true

  tasks:
    - name: Démarrer et activer nginx
      ansible.builtin.service:
        name: nginx
        state: started
        enabled: true
```

---

## 🛠️ Exemple de configuration Pulumi (Typescript)


```js
import * as pulumi from "@pulumi/pulumi";
import * as aws from "@pulumi/aws";

// Create an S3 bucket
const bucket = new aws.s3.Bucket("my-bucket", {
    acl: "private",
    tags: {
        Environment: "Dev",
        Name: "MyPulumiBucket",
    },
});

// Export the bucket name
export const bucketName = bucket.id;
```

---

## 🐳 Outils IaC orientés conteneur

<!-- _class: smaller -->

| Outil         | Rôle principal                              | Particularités                              |
|---------------|----------------------------------------------|----------------------------------------------|
| **Dockerfile**| Décrit l’image du conteneur                  | Définition du build, base de tout conteneur  |
| **Docker Compose** | Décrit des stacks multi-conteneurs en local | Idéal pour le dev, moins adapté à la prod    |
| **Helm**      | Gestion de packages Kubernetes (charts)      | Templating puissant, logique de versionnage  |
| **Kustomize** | Overlays et variantes d’objets Kubernetes    | Natif K8s, sans langage de templating        |
| **CDK8s**     | IaC Kubernetes via des langages de programmation | Basé sur JS/TS/Python, alternative à YAML (jeune)  |

<div class="admonition info">
  ℹ️ Ces outils permettent de <strong>configurer et maintenir l’état des serveurs</strong>, une fois provisionnés par des outils d'IaC de provisionnement comme Terraform ou Pulumi.
</div>

<div class="admonition info">
  💡 Nous préconisons plutôt Kustomize pour les applications internes de l'organisation et Helm pour les applications externe (déjà packagées en Helm).
</div>

---


## 🧩 Exemple de fichier Kustomize

```yaml
# production/kustomization.yaml

resources:
  - deployment.yaml
  - service.yaml

commonLabels:
  app: demo-app

patches:
  - target:
      kind: Deployment
      name: mon-app
    patch: |
      - op: replace
        path: /spec/replicas
        value: 3
```

---
## 🔐 2.4 Notions de déploiement sécurisé

> Un déploiement sécurisé repose sur plusieurs **couches complémentaires** de protection.

---

### 🧾 Gestion des secrets

- Ne jamais stocker de secrets (jetons, clés...) en clair dans le code source.
- Utiliser des outils dédiés : **Vault**, **Sealed Secrets**, **AWS Secrets Manager**.
- Injecter les secrets via des variables d’environnement ou des volumes sécurisés.

---

### 🌐 Réseaux et isolation

- Séparer les flux réseau : **externe / interne / administration**.
- Appliquer des politiques de réseau (ex. : **NetworkPolicy**, **Security Groups**).
- Réduire la surface d’exposition des services (ex. : ingress, firewall, proxy).

---

### 👤 Contrôle d'accès basé sur les rôles (RBAC)

- Appliquer le principe du **moindre privilège**.
- Définir les rôles avec précision : développeur, opérateur, administrateur, observateur...
- Implémenter le RBAC au niveau de **Kubernetes**, du **cloud**, des **pipelines CI/CD** et des **registries**.

---

### 👤 Exemple de RBAC dans Kubernetes

```yaml
# Role : lecture des Pods dans un namespace
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: mon-namespace
  name: lecture-pods
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["get", "list", "watch"]

# RoleBinding : association du rôle à un utilisateur
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: liaison-lecture-pods
  namespace: mon-namespace
subjects:
  - kind: User
    name: alice
    apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: lecture-pods
  apiGroup: rbac.authorization.k8s.io
```

---

### 🔄 2.5 La CI / CD

> La CI/CD automatise la **construction, les tests et le déploiement** des applications,  
> afin de **livrer plus vite**, **plus souvent**, et **avec plus de fiabilité**.

![bg right:40% 100%](./images/CI_CD_Modern.svg)

---

#### ⚙️ CI – Intégration Continue (*Continuous Integration*)

- **Construit** les livrables finaux selon les technologies et languages et via diverses opérations : **Compilation**, **Transpilation**, **Minification**, **Bundling**, **Optimisation**, **Obfuscation**, **Linkage**, **Packaging** (zip, image OCI, war, deb, msi, jar,..), etc.
- Automatiser les **tests à chaque modification du code**
- Peut intégrer des tests de performance
- ... et des **tests de sécurité**
- Détecter rapidement les régressions (**feedback rapide**)
- Analyse la qualité du code (Qualimétrie) : **inspection continue**
- Favoriser les **petites livraisons fréquentes**
- Exemples d’outils : GitLab CI, Jenkins, GitHub Actions, CircleCI, Drone

---

## 🛠️ GitLab CI/CD en bref

🚀 **GitLab CI/CD** = système d’intégration et de déploiement continu intégré à GitLab

- 📦 Exécute des **pipelines** dès qu’un commit/push/MR est effectué  
- 📜 Décrit les étapes dans un fichier `.gitlab-ci.yml` à la racine du dépot  
- 🧱 Utilise des **jobs** parallélisables, organisés en **stages** (build, test, deploy...) en série
- ⚙️ Les scripts exécutés par les jobs sont simplement des commandes bash (simple et puissant)

🧑‍💻 Fonctionne avec des **runners** auto-hébergés ou cloud. En général, les **jobs** sont exécutés sous la forme de **conteneurs** (beaucoup plus reproductible).

---

## 📋 Exemple de pipeline GitLab CI simple

<!-- _class: small -->

```yaml
stages:
  - build
  - test
  - deploy

build-job:
  stage: build
  script:
    - echo "Compilation..."
    - make

test-job:
  stage: test
  script:
    - echo "Tests unitaires"
    - make test

deploy-job:
  stage: deploy
  script:
    - echo "Déploiement en staging"
    - ./deploy.sh
  only:
    - main
```


---

### Un pipeline Gitlab-CI simple avec CD en test

![width:700px](./images/GitLab-Pipeline-simple.png)


---

### Un pipeline Drone-CI simple avec CD en PROD

![width:700px](./images/drone-ci.png)

---

### Un pipeline plus complexe avec parallélisation et pipeline downstream

![width:700px](./images/GitLab-Pipeline.png)

[Source](https://about.gitlab.com/blog/guide-to-ci-cd-pipelines/) : gitlab.com


---

## ⚙️ Jenkins : le vétéran de la CI/CD

- 🧑‍🔧 Jenkins est un outil open-source d’intégration continue (CI)  
- 🧱 Très modulaire, basé sur des **plugins** (plus de 1800 !)  
- ⚙️ Pipelines décrits par un DSL (Domain Specific Language) basé sur Groovy
  * DSL déclaratif (plus simple, structuré) → `pipeline { ... }`
  * DSL scripté (plus flexible, moins lisible) → `node { ... }`
- 🌍 Déploiement sur serveur (local ou cloud), UI web 
- 🛠️ Configuration possible par UI **ou via code (Jenkinsfile)**

<div class="admonition info">
  💡 A moins d'être sur une CI-CD historique, préférer Gitlab-CI ou d'autres CI plus modernes pour éviter le plugin-hell (plugins instables et incompatibles) bien qu'il soit possible de coder des jobs en bash...
</div>

---

## 📝 Exemple de Jenkinsfile simple (Déclaratif)

```groovy
pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Compilation du projet...'
        sh 'make'
      }
    }
    stage('Tests') {
      steps {
        echo 'Lancement des tests...'
        sh 'make test'
      }
    }
    stage('Déploiement') {
      when {
        branch 'main'
      }
      steps {
        echo 'Déploiement en production...'
        sh './deploy.sh'
      }
    }
  }
}
```

---
### 📋 La qualimétrie, exemple avec SonarQube

<!-- _class: small -->

![width:700px](./images/qualimetrie.png)

<div class="admonition tip">
  💡 Utilisez le <b>plugin Sonarlint</b> sur votre IDE pour améliorer votre code avant même d'être commité.
</div>

---

### 🚀 CD – Déploiement Continu (*Continuous Delivery / Deployment*)

- **Continuous Delivery** : le code est toujours prêt à être déployé (déploiement manuel)
- **Continuous Deployment** : le code validé est déployé automatiquement (en environnement de test voire en production)

---

## 🛡️ Ajout de sécurité dans les pipelines CI/CD

> L’intégration de la sécurité dans la chaîne CI/CD est un pilier de l’approche **DevSecOps**  
> Elle permet de détecter les failles **tôt**, **automatiquement**, et **de manière répétable**.

---
<!-- _class: small -->

## 🔍 Analyse de code et dépendances

### ✅ SAST (Static Application Security Testing)

- Analyse du **code source** avant l’exécution
- Détecte les failles connues (ex : injections, erreurs de logique)
- Exemple : SonarQube, Semgrep

### ✅ DAST (Dynamic Application Security Testing)

- Analyse l’application en **exécution**, sans connaître le code
- Exemples : OWASP ZAP, Burp Suite

### ✅ SCA (Software Component Analysis)

- Vérifient les CVEs dans les dépendances
- Exemples : **OWASP Dependency Check**, **npm audit**, **Trivy**, **Grype**, **Artifactory XRay**

---

## 🔏 Intégrité des artefacts : signature & attestation

### ✅ Signatures de build

- Assurent que les images / artefacts **proviennent bien de votre pipeline**
- Permettent la **vérification en production** avant déploiement

### 🔐 Outils courants

- **cosign** : signature et vérification d’images conteneurs
- **Sigstore** : chaîne complète pour signer, publier et vérifier les artefacts

> 🎯 Ajoute de la **traçabilité** et de la **confiance** à la chaîne logicielle

---

## 📦 Sécuriser les artefacts : SBOM & provenance

### 🧾 SBOM (Software Bill of Materials)

- Liste exhaustive des composants d’une image ou d’un build
- Permet de retrouver facilement les dépendances, leurs versions et leurs licences **en production** (alors que le SCA ne s'applique que lors du build)
- Requis par certaines normes (ex : NIS2, ISO 27001, DORA, ...)

### 📜 Provenance

- Informations sur **qui a construit quoi, quand, et avec quoi**
- Permet l’**auditabilité** complète du build

> Outils : **Syft**, **Cosign attestations**, **CycloneDX**, **in-toto**

---

## 📋 Exercice 

Comment intégrer une analyse SCA d'un logiciel JavaScript dans un pipeline ?

---

# 📈 Séance 3 – Marché du travail, métiers du DevSecOps, rôle de l'encadrant (1h20)

* 1 - Les principaux métiers de l'intégration
* 2 - De nouvelles exigences transverses
* 3 - La formation continue
* 4 - Sécurité, culture d’équipe, et responsabilité technique
* 5 - Ressources pour approfondir

---

## 3.1 Les principaux métiers de l'intégration

### 🧩 Intégrateur applicatif
### 🖥️ Intégrateur d’exploitation / SysOps
### 🧠 Site Reliability Engineer (SRE)
### 🔄 Métier : Ingénieur DevOps

---

### 🧩 Métier : Intégrateur applicatif

> 🎯 **Objectif principal** : Assurer que les dépendances sont compatibles, à jour et sûres

#### 🛠️ Activités principales

- Assemble les applications avec leurs dépendances :  
  **Maven, npm, Gradle, PyPI**, etc.
- Gère les conflits de version et maintient la **cohérence globale**
- Met en œuvre l’analyse de sécurité des composants (SCA)
- Maintient une **documentation claire et traçable**

📚 Compétences clés : outils de build, dépendances, sécurité logicielle, veille technologique

---

### 🖥️ Métier : Intégrateur d’exploitation / SysOps

> 🎯 **Objectif principal** : Assurer le bon fonctionnement quotidien des systèmes informatiques

#### 🛠️ Activités principales

- Surveille et gère les systèmes, services et applications
- Résout les incidents et problèmes techniques au quotidien
- Met en œuvre les **mises à jour** et **correctifs**
- Exécute des opérations manuelles ou planifiées d’**Infrastructure as Code (IaC)**
- Gère les **sauvegardes** et les **restaurations**
- Collabore avec les équipes DEV pour planifier les déploiements
- Maintient la **documentation opérationnelle**

----

### 🧠 Métier : Site Reliability Engineer (SRE)

> 🎯 **Objectif principal** : Améliorer la **fiabilité** des systèmes et applications grâce à des pratiques d’**ingénierie logicielle**

#### 🛠️ Activités principales

- Développe des outils de **supervision**, **alerting** et **automatisation**
- Fiabilise le SI via l’**Infrastructure as Code (IaC)**
- Configure les environnements pour assurer **robustesse** et **résilience**
- Conduit des **tests de résilience** (ex. : **chaos engineering**)
- Optimise les performances, réalise des **benchmarks**
- Propose aux équipes DevOps les **bonnes pratiques IaC** (et les documente)
- Rédige les **post-mortems** après incidents

---

### 🔄 Métier : Ingénieur DevOps/DevSecOps
<!-- _class: small -->

> 🎯 **Objectif principal** :  Favoriser la collaboration entre les équipes **développement** et **exploitation** (SysOps, SRE…),  
pour **accélérer et fiabiliser** le cycle de développement et de déploiement logiciel

#### 🛠️ Activités principales

- Automatise les processus de **développement**, **tests** et **déploiement** (CI/CD)
- Écrit et maintient l’**Infrastructure as Code** (Terraform, Kubernetes, Ansible…)
- Aide les DEV à appliquer les bonnes pratiques infra et sécurité (souvent issues du SRE)
  **cloud-native**, **haute disponibilité**, **rejeux**, **résilience**
- Met en place des démarches d’**amélioration continue**
- Participe à la **documentation technique et process**
- Intègre la **sécurité dans la CI/CD** (SAST, DAST, ...)
---

## 🧩 Comparatif des rôles liés à l'intégration et à l'exploitation

| Rôle                         | Objectif principal                                  | Proximité Devs | Posture     |
|------------------------------|------------------------------------------------------|---------------|-------------|
| **Intégrateur applicatif**   | Assurer la compatibilité et la sécurité des dépendances | +++           | Proactif    |
| **SysOps** | Garantir le fonctionnement quotidien des systèmes     | +             | Réactif     |
| **DevOps** / **DevSecOps**   | Fluidifier et sécuriser le cycle Dev / Ops           | ++            | Proactif ++ |
| **SRE**                      | Améliorer la fiabilité via l’ingénierie logicielle   | +             | Proactif +++|


---

### 🧠 En résumé

- L’**intégrateur applicatif** agit **en amont**, sur la qualité des dépendances
- Le **SysOps** assure **la continuité de service** au quotidien
- Le **DevOps**/**DevSecOps** crée **les ponts et les automatismes** entre DEV et OPS
- Le **SRE** agit en **ingénieur de la fiabilité**, avec des outils et une culture de production avancée

---

## 🚀 Des métiers en pleine croissance

🔒 **Non délocalisables**

  * 🤖 Développeurs parfois remplacés par l’IA, des progiciels ou du SaaS
  * ☁️ Sysadmins souvent remplacés par des solutions cloud 
  
  mais: 


🛠️ **SysOps / DevOps / SRE** : essentiels à la fiabilité

🔁 **Multi-rôles recherchés**  → Développement, automatisation, infra, observabilité

---

## 3.2 🌍 Nouvelles exigences transverses

> Les organisations modernes doivent intégrer de nouvelles préoccupations  
> **dès la conception et dans tous les métiers du cycle de vie logiciel**.

En tant que futur encadrant, vous serez également responsable :

- De la **qualité de l'observabilité** et de sa **conformité réglementaire**  
- Des **arbitrages** entre **sécurité**, **performance** et **vie privée**  
- De l’**impact environnemental** des pratiques techniques (**écoconception**)

🎯 L’objectif est de concevoir des systèmes à la fois **robustes**, **responsables** et **durables**.

---

### 🔐 DevSecOps – Sécurité intégrée

- Intégration de la **cybersécurité dans les pipelines** CI/CD
- Analyse statique (SAST), dépendances (SCA), signature des artefacts
- Principe : **"Security as Code"**

---

### 💰 FinOps – Optimisation des coûts cloud

- Suivi et **pilotage des dépenses cloud** par les équipes techniques
- Budgétisation, alertes, accountability, optimisation multi-cloud
- Collaboration Dev + Finances + Ops

---
### 🧭 Éthique de l’observabilité
<!-- _class: small -->

> “**Ce que l’on mesure et stocke doit être justifié, maîtrisé et proportionné.**”

- Les **logs** contiennent souvent des **données personnelles** (IP, identifiants, comportements)
- Le **RGPD** impose une **justification claire**, une **durée de conservation limitée**, et un **usage proportionné**
- L’**observabilité** doit soutenir le **bon fonctionnement** du système, **sans surveillance excessive**

- **Journaliser uniquement** ce qui est **utile** à la supervision ou à l’analyse post-mortem  
- **Éviter** les logs contenant des **données sensibles** ou **nominatives**  
- Mettre en place des **politiques de rétention** et de **rotation des journaux**  
- **Restreindre l’accès** aux journaux et **auditer** leur consultation

---

### 🌱 GreenOps – Réduction de l’empreinte environnementale

- Réduction de la **consommation énergétique des services IT**
- Optimisation des ressources (CPU, stockage, cloud idle, etc.)
- Sensibilisation à la **sobriété numérique**

Le rôle de l’encadrant inclut également une **responsabilité environnementale** :

- **Réduire** les volumes de **logs**, **métriques** et **traces** à l’essentiel  
- **Limiter la durée de conservation** des données de monitoring  
- **Éviter la redondance fonctionnelle** entre outils  
- **Favoriser des solutions sobres** en énergie et en ressources

---

## 🎓 3.3 La Formation continue

<div class="admonition <warning">
  ⚠️ Dans le monde du DevSecOps, les technologies évoluent encore plus vite que dans le domaine du code. Des formations régulières sont indispensables. Prévoir <i>a minima</i> des <b>MOOCs</b> réguliers.
</div>

### Certifications clés dans le cloud, le DevOps et la sécurité

> De nombreuses certifications permettent de **valoriser ses compétences techniques**  
> et de se spécialiser selon son profil : Cloud, Infrastructure, Sécurité ou DevSecOps.

---

### ☁️ Cloud & Infrastructure

- **AWS Certified Solutions Architect / DevOps Engineer**
- **CKA** (Certified Kubernetes Administrator)
    - Pour administrer et gérer des clusters Kubernetes en production
- **CKAD** (Certified Kubernetes Application Developer)
    - Pour concevoir et déployer des applications sur Kubernetes
- **Terraform Associate** (HashiCorp Certified)

---

### 🔐 Sécurité

- Formations de l'**ANSSI** comme la formation **ESSI** "Expert en Sécurité des systèmes d'information" ouverte aux organisations vitales pour la nation.
- **CISSP** (Certified Information Systems Security Professional) – niveau expert
- **CEH** (Certified Ethical Hacker) – sécurité offensive

### 🛡️ DevSecOps

- **DevSecOps Foundation** (DevOps Institute)
- **Practical DevSecOps** – plus technique, orienté pipelines CI/CD

---

### 🔍 S’auto-évaluer sur la sécurité

#### ✅ Forces possibles :
- Connaissance des failles classiques (OWASP top 10...)  
- Capacité à auditer du code ou des configurations  
- Sensibilisation aux enjeux RGPD, traçabilité, logs

#### ⚠️ Lacunes fréquentes :
- Sécurité réseau ou infrastructure (TLS, firewalls, cloud IAM)  
- CI/CD sécurisé, gestion des secrets  
- Modélisation des menaces, tests d’intrusion, audit


---

## 🛡️ 3.4 Sécurité, culture d’équipe, et responsabilité technique

Aujourd’hui, un encadrant technique ne peut plus ignorer la **sécurité**  

Elle se construit dans la **culture d’équipe** et les **choix technologiques**  

Les menaces évoluent, les erreurs humaines sont fréquentes  

Il faut un leadership technique conscient et engagé

🧭 **Objectif** : poser les bases d’un rôle d'encadrant responsable, garant de la sécurité par défaut

---

## 🧭 Gouvernance de la sécurité dans l’équipe

- Clarifier les responsabilités : **qui fait quoi en sécurité ?**  
- Mettre en place des **rituels sécurité** : revue de code, threat modeling, revue des exceptions CVE, ...  
- **Anticiper les risques humains** : erreurs, négligence, turnover  
- Être le garant des **bonnes pratiques** (pas le pompier)

---

## 🧑‍🤝‍🧑 Rôles dans l’équipe

-  **Développeurs** : appliquent les bonnes pratiques de codage sécurisé  
-  **DevOps / SRE** : gèrent la sécurité infra, secrets, CI/CD  
-  **Encadrant / Tech Lead** : impulse la direction, arbitre les choix  
-  **Product Owner** : comprend les enjeux sécurité liés au métier

---

## 🛠️ Choix technologiques orientés sécurité

-  Frameworks avec protections intégrées (CSRF, XSS, injections...)  
-  Authentification et chiffrement dès la conception  
-  Traçabilité : surveillance, logs, audit trail  
-  Choix d’outils maintenus, documentés, et **audités**

---

## 🧠 Culture sécurité by design

-  Sécurité = qualité → **intégrée dès le départ** (« Shift to the Left »)  
-  **User stories** incluant sécurité (ex : rôles, gestion des données sensibles)  
-  Vérifications automatiques SAST/DAST/SCA dans **CI/CD** 
-  **Formation continue** : Capture The Flag (CTF) internes, katas sécurité (cas d'école à corriger), retours d’incidents; ...

---

## 🧑‍💼 Sécurité au quotidien

-  Exemples de **rituels** :  
   *  Atelier **“Sécurité du mois”** (présentation d'un problème de PROD par exemple)
   *  Focus sécurité en **rétrospective** 
   *  **Mini audits en peer review**
-  Montrer l’exemple : **ne jamais merger un code douteux**, même sous pression

---

## 🧭 Posture de l’encadrant responsable

-  Cultiver un climat de confiance : “on peut parler de faille sans crainte”, **blameless**.
-  Rendre la sécurité **visible** : KPIs, alertes, dashboards  
-  Défendre les chantiers sécurité/dette technique face aux priorités business  
-  Valoriser les efforts invisibles autour de la sécurité

---

## 💸 Intérêt économique des tests et de la CI/CD

### 📈 Le coût d’un bug augmente **exponentiellement** avec le temps

- Plus un défaut est détecté **tard**, plus il coûte cher à corriger :
  - 25€ en phase de dev
  - 2500€ ou + en production
- Les boucles longues favorisent l’accumulation de dette technique invisible

---

### 🔁 Règle d’or : la **rétroaction rapide**

🕐 **"10 minutes max"** : temps idéal pour un retour complet dans un pipeline

🔧 Objectif :
- Identifier les erreurs **immédiatement après le commit**
- Corriger à chaud → développeur encore “dans le flow”
- Réduire les context switches, les bugs en prod, et la frustration

🚀 Une CI/CD bien conçue = investissement qui **diminue les coûts cachés**

---

💰 Coût d'un bug avec la phase du projet

![width:700px](./images/couts.png)


---

## 📚 3.5 Ressources pour approfondir

- [OWASP.org](https://owasp.org) : Top 10, Cheat Sheets, outils de test  
- [DevSecOps.org](https://www.devsecops.org) : principes, pratiques, retours terrain  
- [CNCF Security TAG](https://github.com/cncf/tag-security) : bonnes pratiques cloud native  
- [HackTricks](https://book.hacktricks.xyz/) : encyclopédie sécurité offensive/défensive  
- [Cybrary, Root Me, TryHackMe...] : entraînement pratique (CTF, labs)
