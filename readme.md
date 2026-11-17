## Création de branche de pour chaque exercice

-Exercice 1 : Branche exo1
-Exercice 2 : Branche exo2
-Exercice 3 : Branche exo3
-Exercice 4.2 : Branche exo4.1 Les bases de la modélisation : MCD
-Exercice 4.2 : Branche exo4.2 Les bases de la modélisation : MLD
-Exercice 4.3 : Branche exo4.3 Les bases de la modélisation : MPD

## -Exercice 4.2 : Branche exo4.2 Les bases de la modélisation : MLD

Le schéma représenté consiste à établir la relation en 2 entités à savoir les tables Potion et Ingredient. La relation est de type Many to Many, avec la création d'une table intermédiaire qui détient les clés primaires (id_Potion et id_Ingredient) comme clés étangères.

## -Exercice 4.3 : Branche exo4.3 Les bases de la modélisation : MPD

## Atélier Modéliser une base de données

# MCD : Modélisation des entités de la base de données

Entités : Animal, Espèce, Race, Adoptant, Refuge
Attributs

- Animal : animal_id(PK), name, age_estimé, num_tatou, sterilise, vaccin
- Espèce : espece_id(PK), name
- Race : race_id(PK), name
- Adoptant : adoptant_id(PK), prenom, nom, date_naissance, adresse
- Refuge : refuge_id(PK), name, adresse

Associations et cardinalités

- Appartient (Espèce 0,N — 1,1 Race) : une race appartient à une seule espèce ; une espèce regroupe plusieurs races.
- Est de race (Race 0,N — 1,1 Animal) : un animal possède une seule race ; une race concerne plusieurs animaux.
- Est recueilli par (Refuge 0,N — 1,1 Animal) : un animal est recueilli par un seul refuge ; un refuge accueille plusieurs animaux.
- Adoption [date_adoption] (Adoptant 0,N — 0,1 Animal) : un adoptant peut adopter un ou plusieurs animaux ; un animal est adopté au plus une fois avec enregistrement de la date.

# MLD : Modélisation logique des tables relationnelles

Tables : espece, race, refuge, adoptant, animal, adoption
Schéma relationnel (PK = Clé Primaire, FK = Clé Étrangère)

- espece : espece_id(PK), name
- race : race_id(PK), name, #espece_id(FK)
- refuge : refuge_id(PK), name, adresse
- adoptant : adoptant_id(PK), prenom, nom, date_naissance, adresse
- animal : animal_id(PK), name, age_estime, num_tatou, sterilise, vaccin, #race_id(FK), #refuge_id(FK)
- adoption : adoption_id(PK), date_adoption, #adoptant_id(FK), #animal_id(FK, UQ)

# MPD : Modélisation physique pour PostgreSQL

Tables physiques (SGBDR : PostgreSQL)
Colonnes et types SQL

- espece : espece_id SERIAL PRIMARY KEY, name VARCHAR(65) NOT NULL UNIQUE
- race : race_id SERIAL PRIMARY KEY, name VARCHAR(65) NOT NULL, espece_id INTEGER NOT NULL REFERENCES espece(espece_id)
- refuge : refuge_id SERIAL PRIMARY KEY, name VARCHAR(65) NOT NULL, adresse VARCHAR(255) NOT NULL
- adoptant : adoptant_id SERIAL PRIMARY KEY, firstName VARCHAR(100) NOT NULL, name VARCHAR(65) NOT NULL, date_naissance DATE NOT NULL, adresse VARCHAR(255) NOT NULL
- animal : animal_id SERIAL PRIMARY KEY, name VARCHAR(65) NOT NULL, age_estime SMALLINT NOT NULL CHECK (age_estime >= 0), num_tatou VARCHAR(30) UNIQUE, sterilise BOOLEAN NOT NULL DEFAULT FALSE, vaccin BOOLEAN NOT NULL DEFAULT FALSE, race_id INTEGER NOT NULL REFERENCES race(race_id), refuge_id INTEGER NOT NULL REFERENCES refuge(refuge_id)
- adoption : adoption_id SERIAL PRIMARY KEY, date_heure_adoption TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP, adoptant_id INTEGER NOT NULL REFERENCES adoptant(adoptant_id), animal_id INTEGER NOT NULL UNIQUE REFERENCES animal(animal_id)

## Repo sur chaque branche

Capture des résultats des exo et push sur les branches sur Github

## Difficultés rencontrées

Confusion sur les commandes SQL en PostGreSql et MySql
