 Backend avec Spring Boot (Application Cardatabase)
1. Introduction à Spring Boot
Framework Java utilisé pour développer Cardatabase, simplifiant la création de microservices.

Convention over configuration : Configuration minimale pour le démarrage rapide du projet.

Dépendances clés : spring-boot-starter-web, spring-boot-starter-data-jpa, spring-boot-starter-security.

2. Architecture MVC de Cardatabase
Controller (CarController, UserController) : Gestion des endpoints API (/api/cars, /api/users).

Service (CarService, UserDetailsServiceImpl) : Logique métier (filtrage de véhicules, gestion utilisateurs).

Repository (CarRepository, UserRepository) : Accès aux données via Spring Data JPA.

3. Fonctionnalités Implémentées
API REST :

Opérations CRUD pour les véhicules (ajout/suppression/modification).

Recherche de véhicules par marque, modèle, année.

Authentification JWT (endpoint /login).

Sécurité :

Spring Security avec JWT (filtres d'authentification).

Rôles utilisateur (USER, ADMIN).

Base de données :

Modèle de données : Entités Car, User, Owner.

Relations JPA (OneToMany, ManyToMany).

4. Gestion des Données (Spring Data JPA)
Entités :

java
@Entity
public class Car {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String brand, model;
    @ManyToOne
    private Owner owner;
}
Repositories :

java
public interface CarRepository extends JpaRepository<Car, Long> {
    List<Car> findByBrand(String brand);
    @Query("SELECT c FROM Car c WHERE c.year >= :year")
    List<Car> findByYearGreaterThan(@Param("year") int year);
}
Transactions : @Transactional sur les méthodes de service.

5. Sécurité (Spring Security)
Configuration :

java
@Bean
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
    http
        .csrf().disable()
        .authorizeRequests()
        .requestMatchers("/api/login").permitAll()
        .requestMatchers("/api/cars/**").authenticated()
        .and()
        .addFilterBefore(jwtAuthFilter, UsernamePasswordAuthenticationFilter.class);
    return http.build();
}
JWT : Génération de tokens via JwtUtil, validation par filtre personnalisé.

6. Gestion des Erreurs
Handler Global :

java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(EntityNotFoundException.class)
    public ResponseEntity<?> handleNotFound(EntityNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }
}
Validation : DTOs avec @Valid et annotations (@NotBlank, @Size).

7. Configuration Cardatabase
Profils :

application-dev.properties : H2 en mémoire.

application-prod.properties : PostgreSQL.

Variables d'environnement :

DATABASE_URL, JWT_SECRET injectées via .env.

8. Tests
Tests Unitaires :

CarServiceTest avec Mockito.

Tests d'API :

CarControllerTest avec @WebMvcTest + MockMvc.

Tests d'intégration PostgreSQL avec @DataJpaTest.

9. Déploiement
Docker :

Dockerfile
FROM openjdk:17
COPY target/cardatabase.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
CI/CD : Pipeline GitHub Actions pour build/test/déploiement sur AWS.

10. Bonnes Pratiques Appliquées
DTOs : Utilisation de CarDTO pour découpler entités et API.

Documentation : Swagger UI accessible via /swagger-ui.html.

Logging : Journalisation structurée avec SLF4J.

11. Outils Utilisés
Dépendances :

Lombok : Réduction du code boilerplate.

Springdoc OpenAPI : Documentation automatique des endpoints.

H2/PostgreSQL : Bases de données.

DevTools : Rechargement à chaud pendant le développement.

Ce résumé décrit l'implémentation concrète de Spring Boot dans Cardatabase. Pour explorer le code :
src/main/java/com/cardatabase/
Documentation Spring Boot | Code source
