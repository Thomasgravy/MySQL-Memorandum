# STORED PROCEDURES

La base de données MySQL prend en charge les procédures stockées. Une procédure stockée est un sous-programme stocké dans 
le catalogue de base de données. Les applications peuvent appeler et exécuter la procédure stockée. L' CALLinstruction SQL 
est utilisée pour exécuter une procédure stockée.

**Exemple :**
```
USE [name_database];
DROP PROCEDURE IF EXISTS [name_procedure];

DELIMITER |
CREATE PROCEDURE [name_procedure]()
  BEGIN
      DECLARE _i INT;
      DECLARE _txt VARCHAR(100) DEFAULT '';
  
      SET _i = 1;
      SET _txt = 'txt';
  
      SELECT _i, _txt AS Impair;

  end |
DELIMITER ;
CALL [name_procedure]();
```
**Paramètre**

Les procédures stockées peuvent avoir IN, INOUTet les OUTparamètres, en fonction de la version de MySQL. L'interface mysqli 
n'a pas de notion particulière pour les différents types de paramètres.

**Paramètre : IN / OUT / INOUT**

Les paramètres d'entrée sont fournis avec CALL instruction. Veuillez vous assurer que les valeurs sont correctement échappées.

**Exemple :**

```
DELIMITER //
CREATE PROCEDURE Proc1(IN _idPers INT)
  BEGIN
      SELECT * FROM World.personne WHERE id_pers = _idPers;
  END//
DELIMITER ;
SET @idPers = 6;
CALL Proc1(@idPers);

DELIMITER //
CREATE PROCEDURE Proc2(IN _idPers INT,  OUT _nom VARCHAR(24),  OUT _prenom VARCHAR(24))
  BEGIN
      SELECT nom_pers, prenom_pers INTO _nom, _prenom
      FROM World.personne
      WHERE id_pers = _idPers;
  END//
DELIMITER ;
SET @idPers = 5;
CALL Proc2(@idPers, @nom, @prenom);
SELECT @nom;
SELECT @prenom;
DROP PROCEDURE  Proc2;
```