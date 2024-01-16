
1. Les patterns de création :
    
    - Singleton : permet de garantir qu'une classe n'a qu'une seule instance.
    - Fabrique (Factory) : fournit une interface pour créer des objets sans spécifier leur classe concrète.
    - Fabrique abstraite (Abstract Factory) : fournit une interface pour créer des familles d'objets liés ou dépendants sans spécifier leur classe concrète.
2. Les patterns structurels :
    
    - Adapteur (Adapter) : permet à des classes incompatibles de travailler ensemble en convertissant l'interface d'une classe en une autre interface attendue.
    - Composite : permet de traiter un groupe d'objets de la même manière qu'un objet unique.
    - Décorateur (Decorator) : permet d'ajouter des fonctionnalités supplémentaires à un objet de manière dynamique.
    - Proxy : fournit un substitut ou un représentant d'un objet pour contrôler l'accès à cet objet.
3. Les patterns comportementaux :
    
    - Observateur (Observer) : définit une dépendance entre objets de manière à ce que lorsqu'un objet change d'état, tous ses dépendants soient notifiés et mis à jour automatiquement.
    - Stratégie (Strategy) : permet de définir une famille d'algorithmes, encapsule chacun d'eux et les rend interchangeables.
    - Commande (Command) : encapsule une demande sous la forme d'un objet, permettant de paramétrer les clients avec différentes demandes, de mettre en file d'attente ou d'enregistrer des demandes, et de prendre en charge les opérations annuler/rétablir.
    - Modèle de méthode (Template Method) : définit le squelette d'un algorithme dans une méthode, en laissant les sous-classes implémenter certaines étapes spécifiques de l'algorithme.
4. Les patterns architecturaux :
    
    - Modèle-Vue-Contrôleur (MVC) : sépare la logique métier (modèle), la présentation (vue) et la gestion des événements (contrôleur).
    - Modèle-Vue-Présentation (MVP) : similaire à MVC, mais le contrôleur est remplacé par un présentateur qui gère la logique et la coordination entre la vue et le modèle.
    - Modèle-Vue-ViewModel (MVVM) : similaire à MVP, mais utilise un modèle de présentation (view model) pour faciliter la liaison de données bidirectionnelle entre la vue et le modèle.

Il existe de nombreux autres design patterns, chacun avec ses propres objectifs et cas d'utilisation. Les design patterns offrent des solutions éprouvées et des bonnes pratiques pour résoudre des problèmes récurrents de conception logicielle. Ils permettent de promouvoir la réutilisabilité, la maintenabilité et la modularité du code.