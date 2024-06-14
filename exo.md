### Exercice Avengers 
```sql 
-- Créez une base de données avec le nom avengers_db
create datebase avengers_db;
-- Sélectionnez la base de données nouvellement créée 
use avengers_db;
-- Créez la table "figurine" avec des colonnes telles que "id" (clé primaire), "nom", "super_pouvoir", "annee_sortie" et "description"
create table  figurine (
    id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(255),
    super_pouvoir VARCHAR(255),
    annee_sortie CHAR(4),
    description VARCHAR(255)
);
-- Insérez des données dans la table "figurine" pour représenter des figurine Avengers :
insert into figurine (nom,super_pouvoir,annee_sortie, description) values
('Iron Man', 'Armure surpuissante', 2008, 'Milliardaire et génie inventeur.'),
('Captain America', 'Force et endurance surhumaines', 2011, 'Héros emblématique de la Seconde Guerre mondiale.'),
('Thor', 'Contrôle de la foudre et marteau magique', 2011, 'Dieu nordique du tonnerre et prince d_Asgard.'),
('Hulk', 'Force et résistance surhumaines', 2008, 'Scientifique transformé en monstre vert lorsqu_il est en colère.'),
('Black Widow', 'Expert en arts martiaux et espionnage', 2010, 'Agent secret russe doté de grandes compétences.'),
('Black Panther', 'Force, vitesse et agilité surhumaines', 2018, 'Roi du Wakanda et protecteur de son peuple.');
-- Effectuez des requêtes pour afficher les figurine Avengers :
-- Afficher toutes les figurine :
select * from figurine ;
    
-- Afficher les figurine sorties après 2010 :
select * from figurine where annee_sortie > 2010;
    
-- Afficher les figurine avec le pouvoir "Force" dans leur super_pouvoir :
select* from figurine where super_pouvoir LIKE '%Force%';
-- Modifiez la description de "Black Panther" pour "Prince de Wakanda et protecteur de son peuple."
update figurine set description = 'Prince de Wakanda et protecteur de son peuple.' where nom= 'Black Panther';
-- Supprimez la figurine Black Widow de la table "figurine" :
delete from figurine where nom= 'Black Widow';
 ```
 ### Exercice 2
 ``` sql
-- Créer la table "weapon" avec des colonnes telles que "id" (clé primaire), "nom", "description" 
create table weapon (
    id INT UNSIGNED PRIMARY KEY,
    nom VARCHAR(255),
    description TEXT
);
-- Insérez des données dans la table "weapon" pour représenter des armes Avengers :
insert into weapon (nom, description) values ('Marteau', 'Marteau magique de Thor.'),
    ('Bouclier', 'Bouclier indestructible.'),
    ('Arc et flèches', 'Arc et flèches de Hawkeye.'),
    ('Armure', 'Armure spéciale conçue pour combattre Hulk.'),
    ('Vibranium Claws', 'Griffes en vibranium indestructible .');
-- Modifier la table "figurine" pour ajouter une colonne "weapon_id" 
ALTER TABLE figurine ADD COLUMN weapon_id INT;
-- Modifier la table "figurine" pour ajouter une contrainte de clé étrangère avec la table "weapon" :
ALTER TABLE figurine ADD CONSTRAINT fk_id_weapon FOREIGN KEY (weapon_id) REFERENCES weapon (id);
-- Mettre la table "weapon" en relation avec la table "figurine" :
UPDATE figurine SET weapon_id =1 where nom='Thor';
UPDATE figurine SET weapon_id =1 where id=3;
-- Récuperer le nom des avengers et le nom de leurs armes dont l'année de sortie est supérieur à 2010
SELECT figurine.nom, weapon.nom FROM figurine INNER JOIN weapon ON weapon.id=weapon_id WHERE annee_sortie> 2010;
-- Afficher les noms des figurines qui n'ont pas d'armes 
SELECT figurine.nom FROM figurine LEFT JOIN weapon ON weapon.id=weapon_id WHERE weapon_id= NULL

id 1 = 3
id 2 =2
id 4= 1
 ```