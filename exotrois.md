<!-- Créer la base de données school_db
create database school_db
Utiliser la base de données
use school_db
Créer la table "student" avec id, nom prenom, date_naissance, adresse, email

create table student(
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(255),
    prenom VARCHAR(255),
    date_naissance DATE,
    adresse VARCHAR(255),
    email VARCHAR(255)
    );
Créer la table "subject" id, nom, description

create table subject(
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(255),
    description TEXT);

Créer la table "note" avec uid note et des clés étrangères pour student_id et subject_id

CREATE TABLE note(
    id INT PRIMARY KEY AUTO_INCREMENT,
    note INT,
    student_id INT,
    subject_id INT,
    foreign key (student_id) references student(id),
    foreign key (subject_id) references subject(id)
    );

Insérez des données dans les tables :

-- Insertion des étudiants
INSERT INTO student (nom, prenom,date_naissance,adresse, email) values
    ('Doe', 'John', '2000-01-01', '123 Main Street', 'john.doe@example.com'),
    ('Smith', 'Emma', '1999-03-15', '456 Elm Street', 'emma.smith@example.com'),
    ('Johnson', 'Michael', '2001-05-10', '789 Oak Street', 'michael.johnson@example.com'),
    ('Brown', 'Olivia', '2002-07-20', '321 Pine Street', 'olivia.brown@example.com'),
    ('Taylor', 'Sophia', '2003-09-25', '654 Maple Street', 'sophia.taylor@example.com'),
    ('Anderson', 'Liam', '2000-12-05', '987 Cedar Street', 'liam.anderson@example.com'),
    ('Clark', 'Ava', '1998-02-14', '741 Birch Street', 'ava.clark@example.com'),
    ('Lewis', 'Noah', '1999-04-30', '852 Walnut Street', 'noah.lewis@example.com'),
    ('Walker', 'Mia', '2001-06-08', '369 Oakwood Street', 'mia.walker@example.com'),
    ('Hall', 'Elijah', '2002-08-16', '258 Cherry Street', 'elijah.hall@example.com');

-- Insertion des matières
INSERT INTO subject (nom, description) values
    ('Mathématiques', 'Calcul et algèbre'),
    ('Sciences', 'Physique et chimie'),
    ('Histoire', 'Événements historiques'),
    ('Français', 'Grammaire et littérature'),
    ('Anglais', 'Conversation et grammaire');

-- Insertion des notes pour chaque étudiant (exemples)
INSERT INTO note (student_id, subject_id, note) values
    (1, 1, 15.5),
    (1, 2, 12.0),
    (2, 3, 14.5),
    (2, 4, 16.0),
    (3, 5, 13.5),
    (3, 1, 17.0),
    (4, 2, 13.0),
    (4, 3, 11.5),
    (5, 4, 18.0),
    (5, 5, 16.5);

---

Voici quelques exemples de requêtes SQL avec des conditions, des limites et du tri appliqués à la table "étudiant" :

1. Sélectionner tous les étudiants dont le nom est "Doe" :

SELECT * FROM student WHERE nom='Doe';

2. Sélectionner tous les étudiants âgés de moins de 20 ans :

SELECT * FROM student WHERE YEAR(CURDATE())- YEAR(date_naissance) < 20 ;

3. Sélectionner les 5 premiers étudiants dans l'ordre alphabétique des noms :

SELECT * FROM student ORDER BY nom LIMIT 5;

4. Sélectionner les étudiants par ordre décroissant de leur date de naissance :

SELECT * FROM student ORDER BY date_naissance DESC;

5. Sélectionner les étudiants dont l'adresse contient le mot "Street" et limiter les résultats à 3 :

SELECT * FROM student WHERE adresse LIKE '%Street%' LIMIT 3;

6. Sélectionner les étudiants dont le nom commence par "S" et trier les résultats par prénom :

SELECT * FROM student WHERE nom LIKE 's%' ORDER BY prenom;

Ces exemples montrent comment appliquer des conditions, des limites et du tri dans vos requêtes SQL pour la table "student". N'hésitez pas à les ajuster en fonction de vos critères de recherche spécifiques.

---

Voici quelques exemples de requêtes SQL qui utilisent les fonctions MIN, MAX, COUNT, GROUP BY et HAVING :

1. Sélectionner la note minimale, maximale et le nombre total de notes pour chaque matière :

SELECT subject.nom AS matieres,MIN(note) AS min_note, MAX(note) AS max_note, COUNT(*) AS nbr_notes FROM note INNER JOIN subject on subject.id=subject_id GROUP BY subject_id;

2. Sélectionner les étudiants ayant une moyenne supérieure à 15 :

SELECT student.prenom  AS prenom_etudiant, AVG(note) FROM note INNER JOIN student on student.id=student_id GROUP BY student.prenom HAVING AVG(note)>15;


3. Sélectionner le nombre d'étudiants ayant obtenu une note supérieure à 16 dans chaque matière :

SELECT nom COUNT(*) FROM note JOIN subject_id=subject.id WHERE note >16 GROUP BY subject_id

4. Sélectionner les matières ayant au moins cinq étudiants :

SELECT COUNT(*) FROM note GROUP BY subject_id HAVING count(*) >5;

SELECT nom, COUNT(*) FROM note INNER JOIN subject ON subject_id=subject.id GROUP BY subject_id HAVING COUNT(*) >5;

5. Sélectionner les étudiants ayant obtenu une note maximale dans chaque matière :

select student.*, max(note), subject.nom from student join note on student.id = note.student_id join subject on subject.id = note.subject_id group by subject.nom, student.nom;
(NE MARCHE PAS CAR IMPOSSIBLE DE METTRE 2 CONDITIONS)

Ces exemples illustrent l'utilisation des fonctions MIN, MAX, COUNT, GROUP BY et HAVING pour effectuer des calculs et filtrer les données en fonction de certaines conditions.
N'hésitez pas à les adapter en fonction de votre base de données et de vos besoins spécifiques.

---

Cette requête sélectionne les noms d'étudiants dont la date de naissance est postérieure au 1er janvier 2000, groupe les résultats par nom, filtre les groupes ayant plus de 2 étudiants, trie les résultats par nom et limite les résultats à 10.
 -->