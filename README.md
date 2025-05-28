 Backend avec Spring Boot (Application Cardatabase)




Backend avec Spring Boot
________________________________________
1. Introduction à Spring Boot
•	Framework Java simplifiant le développement d'applications backend.
•	Convention over configuration : réduit la configuration manuelle via des paramètres par défaut.
•	Objectif : Créer des applications standalone, production-ready avec des dépendances intégrées (Tomcat, Spring Core, Spring MVC, etc.).
________________________________________
2. Fonctionnalités Clés
•	Starters (spring-boot-starter-*) : Packages prédéfinis pour ajouter des fonctionnalités (Web, Data JPA, Security).
•	Auto-configuration : Configure automatiquement les beans en fonction des dépendances présentes.
•	Actuator : Fournit des endpoints pour la surveillance (santé, métriques, logs).
•	CLI : Outil en ligne de commande pour prototyper rapidement.
________________________________________
3. Architecture MVC
•	Modèle-Vue-Contrôleur adapté aux API REST (la "Vue" est remplacée par des réponses JSON/XML).
•	Couches :
o	Controller : Gère les requêtes HTTP (@RestController, @GetMapping).
o	Service : Logique métier (@Service).
o	Repository : Accès aux données (@Repository, JpaRepository).
________________________________________
4. Développement d'API REST
•	Annotations Principales :
o	@RestController : Combine @Controller + @ResponseBody.
o	@RequestMapping, @GetMapping, @PostMapping, etc.
o	@RequestBody : Désérialise le JSON en objet Java.
o	@PathVariable / @RequestParam : Capture les variables d'URL/paramètres.
•	Réponses : Utilise ResponseEntity pour contrôler le statut HTTP, les headers, et le corps.
________________________________________
5. Gestion des Données (Spring Data JPA)
•	Entités : Classes Java annotées (@Entity, @Id, @Column).
•	Repositories :
o	Interface étendant JpaRepository<T, ID>.
o	Génération automatique de requêtes via des noms de méthodes (findByNom()).
o	Requêtes personnalisées avec @Query.
•	Transactions : @Transactional pour la gestion ACID.
________________________________________
6. Sécurité (Spring Security)
•	Authentification : Formulaire, JWT, OAuth2.
•	Autorisation : @PreAuthorize, @Secured.
•	Configuration via WebSecurityConfigurerAdapter (déprécié) ou SecurityFilterChain.
•	Protection contre les vulnérabilités (CSRF, XSS).
________________________________________
7. Gestion des Exceptions
•	@ControllerAdvice : Intercepte les exceptions globalement.
•	@ExceptionHandler : Traite des exceptions spécifiques (ex: EntityNotFoundException → 404 NOT FOUND).
•	Exceptions courantes : ResponseStatusException, MethodArgumentNotValidException.
________________________________________
8. Configuration
•	Fichiers : application.properties ou application.yml.
•	Profils : spring.profiles.active=dev|prod.
•	Variables d'environnement : Surcharger via des variables système/OS.
•	Validation : @Valid dans les contrôleurs + annotations de validation (@NotNull, @Size).
________________________________________
9. Tests
•	Tests Unitaires : JUnit 5 + Mockito.
•	Tests d'Intégration :
o	@SpringBootTest : Charge le contexte Spring.
o	@DataJpaTest (pour JPA), @WebMvcTest (pour les contrôleurs).
•	Test des API : TestRestTemplate ou MockMvc.
________________________________________
10. Déploiement
•	Fichier JAR : Exécutable via java -jar app.jar.
•	Docker : Créer une image avec un Dockerfile basé sur openjdk.
•	Cloud : Déploiement simplifié sur Heroku, AWS, Azure via des plugins.
________________________________________
11. Bonnes Pratiques
•	Code propre : Respect des principes SOLID.
•	Validation des entrées : DTOs + @Valid.
•	Journalisation : Utilisation de SLF4J/Logback.
•	Documentation d'API : Swagger/OpenAPI (springdoc-openapi).
________________________________________
12. Outils Associés
•	Spring Initializr : Génère la structure du projet.
•	Spring DevTools : Rechargement à chaud (hot reload).
•	Lombok : Réduit le code boilerplate (getters/setters).
________________________________________
Ce résumé couvre les concepts essentiels pour démarrer un projet Spring Boot. Consultez la documentation officielle pour plus de détails.

