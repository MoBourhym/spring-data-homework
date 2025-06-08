# Rapport  : TP ORM JPA Hibernate avec Spring Data

Ce rapport global regroupe les trois parties du TP sur l'ORM (Object-Relational Mapping) avec JPA, Hibernate, et Spring Data dans le cadre du développement d'applications Java avec Spring Boot. Chaque partie correspond à un projet distinct, illustrant des concepts clés et des fonctionnalités spécifiques de gestion de données. Ce rapport fournit une vue d'ensemble des architectures, technologies, entités, relations, et concepts utilisés dans chaque projet, tout en mettant en avant les notions fondamentales de JPA, Hibernate, et Spring Data.

## 📁 Homework Structure

- [Part 1 – Project Patient](https://github.com/MoBourhym/ORM-JPA-Hibernate-Spring-Data)
- [Part 2 – Project Hospital](https://github.com/MoBourhym/ORM-JPA-Hibernate-Spring-Data-Part-2)
- [Part 3 – Project Roles](https://github.com/MoBourhym/ORM-JPA-Hibernate-Spring-Data-Part-3)


## Table des Matières
1. Introduction
2. Vue d'Ensemble des Projets
3. Architecture Globale
4. Technologies Utilisées
5. Concepts Clés et Notions
6. Partie 1 : Gestion des Patients
7. Partie 2 : Système de Gestion Hospitalière
8. Partie 3 : Gestion des Utilisateurs et Rôles
9. Comparaison des Projets
10. Conclusion
11. Annexes

## 1. Introduction
L'objectif de ce TP est de maîtriser les concepts d'ORM à travers JPA et Hibernate, en utilisant Spring Data pour simplifier l'accès aux données dans des applications Spring Boot. Les trois projets abordent des cas d'utilisation différents :
- **Partie 1** : Gestion des patients avec des opérations CRUD simples.
- **Partie 2** : Système hospitalier avec relations complexes entre patients, médecins, rendez-vous, et consultations.
- **Partie 3** : Gestion des utilisateurs et rôles avec une relation Many-to-Many.

Chaque projet met en œuvre des concepts fondamentaux d'ORM, des relations entre entités, des repositories Spring Data, et des services métier, tout en explorant des bases de données relationnelles (H2 pour les tests, MySQL pour la production).

## 2. Vue d'Ensemble des Projets

| **Partie** | **Description** | **Entités Principales** | **Relations** | **Base de Données** |
|------------|-----------------|-------------------------|---------------|---------------------|
| Partie 1   | Gestion des patients avec CRUD | Patient | Aucune | H2, MySQL |
| Partie 2   | Système hospitalier | Patient, Médecin, RendezVous, Consultation, StatusRDV | One-to-Many, Many-to-One, One-to-One | H2, MySQL |
| Partie 3   | Gestion des utilisateurs et rôles | User, Role | Many-to-Many | H2 |

Chaque projet progresse en complexité, passant d'opérations CRUD simples (Partie 1) à des relations complexes (Partie 2) et une gestion avancée des relations bidirectionnelles (Partie 3).

## 3. Architecture Globale
Les trois projets adoptent une **architecture en couches** typique des applications Spring Boot :

```
┌─────────────────────────┐
│   Contrôleur (REST)     │  (API REST, Partie 2 uniquement)
├─────────────────────────┤
│   Service               │  (Logique métier)
├─────────────────────────┤
│   Repository            │  (Accès aux données via Spring Data JPA)
├─────────────────────────┤
│   Entité                │  (Objets JPA mappés aux tables)
├─────────────────────────┤
│   Base de Données       │  (H2 pour tests, MySQL pour production)
└─────────────────────────┘
```

- **Contrôleur** : Gère les requêtes HTTP (présent dans Partie 2 pour les endpoints REST).
- **Service** : Contient la logique métier et coordonne les interactions avec les repositories.
- **Repository** : Fournit une abstraction pour les opérations CRUD et les requêtes personnalisées.
- **Entité** : Représente les tables de la base de données via des classes Java annotées.
- **Base de Données** : H2 pour les tests en mémoire, migré vers MySQL pour la persistance en production.

## 4. Technologies Utilisées
Les technologies communes aux trois projets sont :

| **Technologie** | **Version** | **Description** |
|-----------------|-------------|-----------------|
| Spring Boot | 3.2.4 - 3.4.4 | Framework principal pour le développement rapide d'applications Java. |
| Spring Data JPA | 3.4.4 | Abstraction pour simplifier l'accès aux données avec JPA. |
| Hibernate | 6.4.4 - 6.6.11 | Implémentation JPA pour l'ORM. |
| H2 Database | 2.3.232 | Base de données en mémoire pour les tests. |
| MySQL | 8.0 | Base de données relationnelle pour la production (Partie 1 et 2). |
| Lombok | 1.18.38 | Réduction du code boilerplate (getters, setters, constructeurs). |
| Maven | 3.6+ | Gestionnaire de dépendances. |
| Java | 17 | Langage de programmation. |

## 5. Concepts Clés et Notions

### 5.1 ORM (Object-Relational Mapping)
- **Définition** : Technique pour mapper des objets Java aux tables relationnelles d'une base de données.
- **Avantages** : Simplifie les interactions avec la base de données en évitant l'écriture manuelle de requêtes SQL.
- **Utilisation** : Les entités JPA (`@Entity`) représentent les tables, et les annotations définissent les mappings.

### 5.2 JPA (Java Persistence API)
- **Rôle** : Spécification standard pour l'ORM, définissant des interfaces pour la gestion des entités.
- **Annotations clés** :
  - `@Entity` : Marque une classe comme entité persistante.
  - `@Table` : Spécifie le nom de la table associée.
  - `@Id` : Définit la clé primaire.
  - `@Column` : Configure les colonnes (nom, contraintes).
  - `@GeneratedValue` : Définit la stratégie de génération des clés primaires (e.g., `IDENTITY`).

### 5.3 Hibernate
- **Rôle** : Implémentation de JPA, utilisée par Spring Boot pour gérer les interactions avec la base de données.
- **Fonctionnalités** :
  - Génération automatique du schéma (`spring.jpa.hibernate.ddl-auto`).
  - Exécution des requêtes SQL sous-jacentes.
  - Gestion des transactions et des relations.

### 5.4 Spring Data JPA
- **Rôle** : Simplifie l'accès aux données en fournissant des repositories avec des méthodes CRUD automatiques.
- **Fonctionnalités** :
  - **JpaRepository** : Interface de base pour les opérations CRUD (`save`, `findAll`, `findById`, `delete`).
  - **Query Methods** : Génération automatique de requêtes à partir des noms de méthodes (e.g., `findByMaladeTrue`).
  - **@Query** : Requêtes JPQL ou SQL personnalisées.
  - **Derived Queries** : Requêtes basées sur les conventions de nommage.

### 5.5 Relations JPA
- **Types** :
  - **One-to-Many** : Un patient peut avoir plusieurs rendez-vous (Partie 2).
  - **Many-to-One** : Plusieurs rendez-vous sont associés à un médecin (Partie 2).
  - **One-to-One** : Un rendez-vous a une consultation unique (Partie 2).
  - **Many-to-Many** : Un utilisateur peut avoir plusieurs rôles, et un rôle peut être attribué à plusieurs utilisateurs (Partie 3).
- **Annotations** :
  - `@OneToMany`, `@ManyToOne`, `@OneToOne`, `@ManyToMany`.
  - `@JoinColumn` : Définit les colonnes de jointure.
  - `mappedBy` : Indique le côté propriétaire de la relation.
  - `fetch` : Configure le chargement (`FetchType.LAZY` ou `FetchType.EAGER`).
  - `cascade` : Gère la propagation des opérations (e.g., `CascadeType.ALL`).

### 5.6 Gestion des Transactions
- **Annotation** : `@Transactional` pour assurer la cohérence des opérations sur la base de données.
- **Utilisation** : Appliquée au niveau des services pour gérer les transactions (rollback en cas d'erreur).

### 5.7 Lombok
- **Rôle** : Réduit le code boilerplate en générant automatiquement getters, setters, constructeurs, etc.
- **Annotations** :
  - `@Data` : Génère getters, setters, `toString`, `equals`, `hashCode`.
  - `@NoArgsConstructor`, `@AllArgsConstructor` : Constructeurs sans ou avec tous les paramètres.
  - `@ToString.Exclude` : Évite les boucles infinies dans les relations bidirectionnelles.

### 5.8 Injection de Dépendances
- **Concept** : Inversion de contrôle (IoC) via le conteneur Spring.
- **Méthodes** :
  - Constructor Injection (préférée, Partie 3).
  - `@Autowired` (Partie 2, dépréciée pour les champs).

### 5.9 Configuration Spring Boot
- **Fichier** : `application.properties` pour configurer la base de données, JPA, et Hibernate.
- **Propriétés clés** :
  - `spring.datasource.*` : URL, utilisateur, mot de passe de la base de données.
  - `spring.jpa.hibernate.ddl-auto` : Gère la création/mise à jour du schéma.
  - `spring.jpa.show-sql` : Affiche les requêtes SQL.
  - `spring.jpa.properties.hibernate.format_sql` : Formate les requêtes SQL.

## 6. Partie 1 : Gestion des Patients

### 6.1 Objectif
Développer une application simple pour gérer des patients avec des opérations CRUD.

### 6.2 Entité
- **Patient** :
  - `id` (Long, clé primaire)
  - `name` (String)
  - `dateOfBirth` (Date)
  - `sickness` (boolean)
  - `score` (int)

### 6.3 Repository
- **PatientRepository** :
  - Étend `JpaRepository<Patient, Long>`.
  - Méthodes personnalisées :
    - `findBySickness(boolean sickness)`
    - `findPatientsByScoreLessThan(int score)`
    - `findPatientsByNameContains(String name)`

### 6.4 Fonctionnalités
- **Création** : Ajout de patients avec des données fictives.
- **Lecture** : Récupération de tous les patients, d’un patient par ID, ou par critères (maladie, score, nom).
- **Mise à jour** : Modification des attributs d’un patient existant.
- **Suppression** : Suppression d’un patient par ID.

### 6.5 Configuration
- **H2 Database** (initialement) :
  ```properties
  spring.datasource.url=jdbc:h2:mem:patient-db
  spring.h2.console.enabled=true
  ```
- **MySQL** (migration) :
  ```properties
  spring.datasource.url=jdbc:mysql://localhost:3306/patients-db
  spring.jpa.hibernate.ddl-auto=update
  ```

### 6.6 Concepts Abordés
- Mapping simple avec `@Entity`, `@Table`, `@Column`.
- Utilisation de `@Temporal` pour les dates.
- Requêtes dérivées et personnalisées avec Spring Data.
- Migration de H2 vers MySQL.

## 7. Partie 2 : Système de Gestion Hospitalière

### 7.1 Objectif
Implémenter un système hospitalier avec des relations complexes entre patients, médecins, rendez-vous, et consultations.

### 7.2 Entités et Relations
- **Patient** : `id`, `nom`, `dateNaissance`, `malade`, `rendezVous` (One-to-Many).
- **Medecin** : `id`, `nom`, `email`, `specialite`, `rendezVous` (One-to-Many).
- **RendezVous** : `id`, `date`, `status` (enum), `patient` (Many-to-One), `medecin` (Many-to-One), `consultation` (One-to-One).
- **Consultation** : `id`, `date`, `rapport`, `rendezVous` (One-to-One).
- **StatusRDV** : Énumération (`PENDING`, `CONFIRMED`, `COMPLETED`, `CANCELLED`).

### 7.3 Repositories
- **PatientRepository** : `findByMaladeTrue()`, `findByNomContaining(String nom)`, `findByNom(String nom)`.
- **MedecineRepository** : `findBySpecialite(String specialite)`, `findByNom(String nom)`, `findByEmail(String email)`.
- **RendezVousRepository**, **ConsultationRepository** : Opérations CRUD de base.

### 7.4 Services
- **IHospitalService** et **HospitalServiceImpl** :
  - Gestion des patients, médecins, rendez-vous, et consultations.
  - Injection des repositories via `@Autowired`.

### 7.5 Contrôleur REST
- **PatientRestController** :
  - Endpoints : `GET /patients`, `POST /patients`, `GET /patients/{id}`, `PUT /patients/{id}`, `DELETE /patients/{id}`.

### 7.6 Configuration
- **H2 Database** :
  ```properties
  spring.datasource.url=jdbc:h2:mem:hospital-db
  spring.h2.console.enabled=true
  ```
- **MySQL** :
  ```properties
  spring.datasource.url=jdbc:mysql://localhost:3306/hospital-db
  ```

### 7.7 Concepts Abordés
- Relations complexes : `@OneToMany`, `@ManyToOne`, `@OneToOne`.
- Gestion des énumérations avec `@Enumerated`.
- Fetching strategies (`FetchType.LAZY`, `FetchType.EAGER`).
- Cascade operations (`CascadeType.ALL`).
- API REST avec Spring Web.
- Initialisation des données via `CommandLineRunner`.

## 8. Partie 3 : Gestion des Utilisateurs et Rôles

### 8.1 Objectif
Implémenter un système de gestion d'utilisateurs et de rôles avec une relation Many-to-Many.

### 8.2 Entités et Relations
- **User** :
  - `userId` (String, UUID)
  - `username` (String, unique)
  - `password` (String)
  - `roles` (Many-to-Many avec `Role`)
- **Role** :
  - `id` (Long)
  - `roleName` (String, unique)
  - `description` (String)
  - `users` (Many-to-Many avec `User`)
- **Table de jointure** : `role_users` (générée automatiquement par Hibernate).

### 8.3 Repositories
- **UserRepository** : `findByUsername(String username)`.
- **RoleRepository** : `findByRoleName(String roleName)`.

### 8.4 Services
- **UserService** et **UserServiceImpl** :
  - Ajout d’utilisateurs et rôles.
  - Attribution de rôles à des utilisateurs.
  - Authentification simple (vérification username/password).
  - Constructor injection (sans `@Autowired`).

### 8.5 Configuration
- **H2 Database** :
  ```properties
  spring.datasource.url=jdbc:h2:mem:users-db
  spring.jpa.hibernate.ddl-auto=create
  spring.h2.console.enabled=true
  ```

### 8.6 Fonctionnalités
- Création d’utilisateurs avec UUID généré.
- Création et attribution de rôles.
- Authentification des utilisateurs.
- Gestion bidirectionnelle de la relation Many-to-Many.

### 8.7 Concepts Abordés
- Relation Many-to-Many avec `@ManyToMany` et table de jointure.
- Fetching `EAGER` pour charger les rôles associés.
- Gestion des boucles infinies avec `@ToString.Exclude`.
- Génération d’UUID pour les clés primaires.
- Transactions avec `@Transactional`.
- Constructor injection moderne.

## 9. Comparaison des Projets

| **Critère** | **Partie 1** | **Partie 2** | **Partie 3** |
|-------------|--------------|--------------|--------------|
| **Complexité** | Simple (CRUD) | Moyenne (relations complexes) | Avancée (Many-to-Many) |
| **Entités** | 1 (Patient) | 4 (Patient, Medecin, RendezVous, Consultation) + 1 enum | 2 (User, Role) |
| **Relations** | Aucune | One-to-Many, Many-to-One, One-to-One | Many-to-Many |
| **Base de Données** | H2, MySQL | H2, MySQL | H2 |
| **API REST** | Non | Oui | Non |
| **Injection** | Non spécifié | `@Autowired` | Constructor Injection |
| **Cas d’Utilisation** | Gestion basique | Système hospitalier | Authentification et autorisation |

## 10. Conclusion
Ce TP a permis de maîtriser les concepts fondamentaux de l’ORM avec JPA, Hibernate, et Spring Data à travers trois projets complémentaires. Les points clés appris incluent :

- **Mapping d’entités** : Utilisation des annotations JPA pour mapper des objets Java aux tables relationnelles.
- **Gestion des relations** : Implémentation de relations simples et complexes (One-to-Many, Many-to-Many, etc.).
- **Spring Data JPA** : Simplification des accès aux données avec des repositories et des requêtes automatiques.
- **Migration de bases de données** : Transition de H2 (tests) à MySQL (production).
- **Bonnes pratiques** : Injection de dépendances, gestion des transactions, et réduction du code avec Lombok.
- **Développement d’API REST** : Exposition des fonctionnalités via des endpoints (Partie 2).
- **Débogage** : Utilisation de la console H2 et des logs SQL pour valider les schémas et requêtes.

Chaque projet a renforcé la compréhension des concepts ORM et des outils Spring, tout en introduisant des fonctionnalités de plus en plus complexes. Les compétences acquises sont directement applicables à des projets réels de gestion de données.

## 11. Annexes

### 11.1 Exemple de CommandLineRunner (Partie 1)
```java
@Bean
CommandLineRunner start(PatientRepository patientRepository) {
    return args -> {
        patientRepository.save(new Patient(null, "Hassan Morsi", new Date(), false, 85));
        patientRepository.save(new Patient(null, "Omar Nouri", new Date(), true, 65));
        List<Patient> patients = patientRepository.findAll();
        patients.forEach(System.out::println);
    };
}
```

### 11.2 Exemple de Requête JPQL (Partie 1)
```java
@Query("SELECT p FROM Patient p WHERE p.score < :score")
List<Patient> findPatientsByScoreLessThan(@Param("score") int score);
```

### 11.3 Configuration MySQL (Partie 1 et 2)
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/patients-db
spring.datasource.username=root
spring.datasource.password=
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
```

### 11.4 Table de Jointure Many-to-Many (Partie 3)
```sql
CREATE TABLE role_users (
    roles_id BIGINT,
    users_user_id VARCHAR(255),
    FOREIGN KEY (roles_id) REFERENCES role(id),
    FOREIGN KEY (users_user_id) REFERENCES users(user_id)
);
```

### 11.5 Instructions d’Exécution
```bash
# Cloner le projet
git clone [URL_DU_PROJET]

# Compiler
mvn clean compile

# Exécuter
mvn spring-boot:run

# Accéder à la console H2
http://localhost:8080/h2-console (ou 8081 pour Partie 3)
```
