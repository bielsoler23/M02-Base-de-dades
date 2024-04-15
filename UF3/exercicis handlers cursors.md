# EXERCICIS HANDLERS I CURSORS
Resol aquests exercicis de l'elaboració de subprogrames mitjançant les BD proporcionades durant el curs.
### Exercici 1
Per realitzar l’execici caldrà tenir creada una taula logs_usuaris (si ja l’heu creat en exercicis anteriors la podeu reaprofitar) amb la següent especificació :
 ```sql
 CREATE TABLE logs_usuaris (
 usuari    VARCHAR(100),
 data      DATETIME,
 taula     VARCHAR(64),
       accio     VARCHAR(20),
       valor_pk  VARCHAR(200),
       error     INT(4)
 );

```
Fes un procediment tal que donat un codi d’empleat, crei una taula anomenada empleat_copia  ( en cas que no existeixi ) amb els camps: id_empleat, nom i cognoms. 

A continuació ha de fer una còpia (INSERT) de les dades de l’empleat a la nova taula. 

En cas que l’empleat indicat no existeixi en la taula empleats, registrarà la incidència en la taula logs_usuaris amb la següent informació.: 
- usuari: usuari actual
- data : data-hora actual
- taula : empleat_copia
- accio : 'COPIA_EMPL'
- valor_pk: el codi empleat que hem intentat traspassar
- error : 1

En el cas que l’empleat ja existeixi a la taula empleat_copia inserirem un
registre a la taula log_usuaris informant d’aquest fet:
- usuari: usuari actual
- data : data-hora actual
- taula : empleat_copia
- accio : COPIA_EMPL
- valor_pk: el codi empleat que hem intentat traspassar
- error : 2

**NOTA: utilitzar HANDLER’s per detectar que l’empleat no existeix i el possible error de clau duplicada en la taula empleat_copia.**

```sql

```

### Exercici 2
Crea la taula següent:
```sql
 CREATE TABLE categories (
 codi CHAR(2) PRIMARY KEY,
 nom VARCHAR(30),
 quantitat SMALLINT UNSIGNED
 );
```
Modifica la funció **sp_Categoria** creada a l'activitat de subprogrames per tal de que retorni un codi de categoria amb la nomenclatura següent:
- C1 = Auxiliar
- C2 = Oficial de Segona
- C3 = Oficial de Primera
- C4 = Que es jubili!

Crea un subprograma encarregat de comptabilitzar el número d'empleats de cada categoria i assigni aquest valor en el camp quantitat de la taula categories destinada a guardar aquesta informació. 
**Realitza aquesta acció amb l’ajuda d’un cursor.**

```sql

```

### Exercici 3
Afegeix un camp de tipus DECIMAL  a la taula departaments anomenat salari_avg.
Crea un subprograma que ompli aquest camp amb la mitjana de salaris dels empleats del departament corresponent.

**Nota: Fes-lo utilitzant CURSORS.**

```sql

```
### Exercici 4
Per tal de saber quins són els «Pringats» de cada departament es demana crear una nova taula anomenada pringats a on hi hagi l'identificador de l'empleat i l'identificador del departament el qual pertany. 
En aquesta taula s'hi guardaran tots els «pringats» de cada departament.
```sql
CREATE TABLE pringats (
 empleat_id      INT,
 departament_id
 INT,
  CONSTRAINT PK_PRINGATS PRIMARY KEY (departament_id, empleat_id)
 ) ;
```
Aquesta taula s'ha d'omplir mitjançant un subprograma mitjançant cursors. Aquest ha d'esborrar el contingut de la taula a l'inici de la seva execució. 
```sql

```

### Exercici 5
Modifica el subprograma anterior o creen un de nou de tal manera que el subprograma només afegeixi a la taula de pringats només aquells que no hi existeixin prèviament.
```sql

```

### Exercici 6
 Es vol segregar els empleats pel mes de l'any que van ser contractats. 
 Per això es vol crear una nova taula anomenada empleats_segregats que conté els camps id_empleat i el número del mes de l'any quan va ser contractat. 
 Crea un subprograma que mitjançant cursors realitzi aquesta feina.
```sql

```

### Exercici 7
Afegeix un nou camp a la taula FEINES a on volem guardar la quantitat de treballadors que han treballat d'aquest perfil en algun moment de la seva vida laboral dins l'empresa. 
Crea un subprograma que mitjançant cursors ompli aquest nou camp.
```sql

```

### Exercici 8
Donades les següents taules (les pots crear a la DB rrhh):
```sql
 CREATE TABLE factura (
 numf INT(8) PRIMARY KEY,
 data DATETIME,
 import DECIMAL(8,2)
 ) Engine = InnoDB;
 CREATE TABLE linia_factura ( 
numf INT(8),
 linia INT(4),
 article VARCHAR(2),
 descripcio VARCHAR(100),
 unitats INT(4),
 preuU DECIMAL(5,2),
  PRIMARY KEY(numf,linia),
  FOREIGN KEY (numf) REFERENCES factura(numf)  
) Engine InnoDB;
```
 Afegeix els següents registres inicials:
```sql
 INSERT INTO factura(numf,data) VALUES (1,'2012-04-30');
 INSERT INTO linia_factura VALUES(1,1,'01','Pistons Wiseco',2,120);
 INSERT INTO linia_factura VALUES(1,2,'02','Culata Scream Eagle',1,240);
 INSERT INTO factura(numf,data) VALUES (2,'2012-03-21');
 INSERT INTO linia_factura VALUES(2,1,'03','Arbol de levas',3,221.5);
 INSERT INTO factura(numf,data) VALUES (3,'2012-04-28');
 INSERT INTO linia_factura VALUES(3,1,'04','Centralita ThunderMax',3,355);
 INSERT INTO linia_factura VALUES(3,2,'05','Filtro Aire K&N',2,60);
 INSERT INTO linia_factura VALUES(3,2,'01','Pistons Wiseco',4,120);
```
Ens hem adonat que l’import resum de la taula factura no l’hem calculat! :(

Ara ens cal fer un procediment que recalculi aquests imports. (Aquí tenim tres factures i es podria arribar a fer a mà, però penseu que podrien haver centenars de factures a recalcular en un entorn real ).

Una possible estratègia a seguir pot ser la següent:

Fer un cursor sobre la taula factura agafant les dades que ens interessen ( en aquest cas només amb numf en tenim prou )

Per cada registre obtingut fer:
- Amb numf accedir a linia_factura i calcular l’import total
- Actualitzar el camp import de la taula factura  amb l’import obtingut en el pas anterior
```sql

```
