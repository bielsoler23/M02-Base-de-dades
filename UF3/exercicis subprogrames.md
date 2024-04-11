# EXERCICIS SUBPROGRAMES
## ENUNCIATS DE FUNCIONS
### Exercici 1
Fes una funció anomenada spData, tal que donada una data en format MySQL ( AAAA-MM-DD ) ens retorni una cadena de caràcters en format DD-MM-AAAA
Exemple : SELECT spData('1988-12-01') => 01-12-1988
```sql
DELIMITER //

CREATE FUNCTION spData(data_entrada DATE)
RETURNS VARCHAR(10)
BEGIN
    DECLARE data_sortida VARCHAR(10);
    SET data_sortida = DATE_FORMAT(data_entrada, '%d-%m-%Y');
    RETURN data_sortida;
END //

DELIMITER ;
```

### Exercici 2
Fes una funció anomenada spPotencia, tal que donada una base i un exponent, ens calculi la seva potència. Intenta no utilitzar la funció POW.
Exemple : SELECT spPotencia(2,3) => 8
```sql
DELIMITER //

CREATE FUNCTION spPotencia(base INT, exponent INT)
RETURNS INT
BEGIN
    DECLARE resultat INT DEFAULT 1;
    WHILE exponent > 0 DO
        SET resultat = resultat * base;
        SET exponent = exponent - 1;
    END WHILE;
    RETURN resultat;
END //

DELIMITER ;
```

### Exercici 3
Fes una funció anomenada spIncrement que donat un codi d’empleat i un % de increment, ens calculi el salari sumant aquest percentatge.
Per exemple, suposem que l’ empleat amb id_empleat = 124 té un salari de 1000
Exemple: SELECT spIncrement(124,10) obtindriem -> 1100
```sql
DELIMITER //

CREATE FUNCTION spIncrement(id_empleat INT, increment_pct DECIMAL(5,2))
RETURNS DECIMAL(8,2)
BEGIN
    DECLARE nou_salari DECIMAL(8,2);
    SELECT salari INTO nou_salari FROM empleats WHERE empleat_id = id_empleat;
    SET nou_salari = nou_salari * (1 + (increment_pct / 100));
    RETURN nou_salari;
END //

DELIMITER ;
```
### Exercici 4
Fes una funció anomenada spPringat, tal que li passem un codi de departament, i ens torni el codi d’empleat que guanya menys d’aquell departament.
```sql

```

### Exercici 5
Utilitzant la funció spPringat fes una consulta per obtenir de cada departament, l’empleat pringat. Mostra el codi i nom del departament, i el codi d’empleat.
```sql

```

### Exercici 6
Fes una funció anomenada spCategoria, tal que donat un codi d’empleat, ens digui en quina categoria professional està. 
El criteri que volem seguir per determinar la categoria professional és en funció dels anys que porta treballant a l’empresa:
- Entre 0 i 1 anys -> Auxiliar
- Entre 2 i 10 anys -> Oficial de Segona
- Entre 11 i 20 Anys -> Oficial de Primera
- Més de 20 anys -> Que es jubili!
```sql

```

### Exercici 7
Fes una consulta utilitzant la funció anterior perquè mostri mostri de cada empleat, el codi d’empleat, el nom, els anys treballats i la categoria professional a la que pertany.
```sql

```

### Exercici 8
Fes una funció anomenada **spEdat**, tal que donada una data per paràmetre ens retorni l'edat d'una persona. Les dates posteriors a la data d'avui han de retornar 0.
```sql

```

### Exercici 9
Fes una funció que ens retorni el número de directors (caps) diferents tenim.
```sql

```

### Exercici 10
Quina **instrucció** utilitzarem si volem veure el contingut de la funció **spPringat**?
```sql

```

##  ENUNCIATS DE PROCEDIMENTS
**NOTA**: En cada exercici, indica com ho faries per cridar el procediment.

### Exercici 1
Fes un procediment que permeti obtenir la data i hora del sistema i l’usuari actual.
```sql

```

### Exercici 2
Fes un procediment que intercanvii el sou de dos empleats passats per paràmetre.
```sql

```

### Exercici 3
Fes un procediment que donat dos Ids d'empleat assigni el codi de departament del primer en el segon.
```sql

```

### Exercici 4
Fes un procediment que donat dos codis de departament assigni tots els empleats del segon en el primer. 
Un cop executat el procediment el departament que correspont en el segon paràmetre ha de quedar desert/sense cap empleat.
```sql

```

### Exercici 5
Fes un procediment per mostrar un llistat dels empleats. Volem veure el id_empleat, nom_empleat, nom_departament i el nom de la localització del departament.
```sql

```

### Exercici 6
Fes un procediment que donat un codi d’empleat, ens doni la informació de l’empleat ( agafa la informació que creguis rellevant).
```sql

```

### Exercici 7
Volem fer un registre dels usuaris que entren al nostre sistema. Per fer-ho primer caldrà crear una taula amb dos camps, un per guardar l’usuari i l’altre per guardar la data i hora de l’accés.
```sql

```

### Exercici 8
A continuació feu un procediment sense arguments, de manera que cada vegada que el crideu, insereixi en aquesta taula l’usuari actual i la data i hora en que s’ha executat el procediment.
```sql

```

### Exercici 9
Fes un procediment que ens permeti afegir un nou departament però amb la següent particularitat: En cas que la localització no existeixi a la taula localitzacions, ens posarà un NULL en el camp id_localtizacio de la taula departaments. Al procediment li hem de passar el codi de departament, el nom del departament i el codi de la localització.
```sql

```

### Exercici 10
Fes un procediment que donat un codi d’empleat, ens posi en paràmetres de sortida el nom i el cognom. Indica com ho pots fer per comprovar si el procediment et funciona.
```sql

```

### Exercici 11
Fes un procediment que ens permeti modificar el nom i cognom d’un empleat.
```sql

```

### Exercici 12
Crea una taula d’auditoria anomenada logs_usuaris. Aquesta taula la utilitzarem per monitoritzar algunes de les accions que fan els usuaris sobre les dades, per exemple si actualitzen dades, eliminen registres.
La taula ha de tenir els següents camps:

<table>
  <tr>
    <td>usuari</td>
    <td>VARCHAR(100)</td>
    <td>Usuari que ha realitzat l'acció</td>
  </tr>
  <tr>
    <td>data</td>
    <td>DATETIME</td>
    <td>Data-Hora en que s’ha realitzat l’acció</td>
  </tr>
  <tr>
    <td>taula</td>
    <td>VARCHAR(50)</td>
    <td>Taula sobre la que es realitza l’acció</td>
  </tr>
  <tr>
    <td>accio</td>
    <td>VARCHAR(20)</td>
    <td>"ELIMINAR", "AFEGIR", "MODIFICAR", "INSERIR"</td>
  </tr>
  <tr>
    <td>valor_pk</td>
    <td>VARCHAR(200)</td>
    <td>valor que identifica el registre que ha patit l'acció</td>
  </tr>
</table>

Fes un procediment amb nom **spRegistrarLog** que rebrà com a paràmetres el nom de la taula, l’acció i el valor_pk. 
Aquest procediment només cal que insereixi un registre en la taula logs_usuaris amb les dades rebudes, tenint en compte l’usuari actual i la data-hora del sistema.
```sql

```

### Exercici 13
Fes un procediment que ens permeti eliminar un departament determinat. El departament s’ha d’eliminar de la taula departaments. Utilitza a més **dins d’aquest procediment**, el procediment creat anteriorment (**spRegistrarLog**) per guardar també un registre del que ha realitzat l’usuari. Ens ha de quedar clar que l’usuari actual, en data X ha eliminat de la taula DEPARTAMENTS el codi departament Y.
- Per exemple, si fem una crida al procediment per eliminar un departament:
CALL eliminarDept(300);

El departament 300 s’ha d’eliminar de la taula departaments, i a més si fem una SELECT de la taula logs_usuaris, veuriem per exemple el següent:
| uauri            | data                  | taula         | accio    | valor_pk |
|------------------|-----------------------|---------------|----------|----------|
| root@localhost   | 2012-04-30 12:34:00   | DEPARTAMENTS  | ELIMINAR | 300      |

```sql

```

### Exercici 14
Fes un procediment que ens posi en paràmetres de sortida, el número d’empleats que tenim, el número de departaments i el número de localitzacions.
```sql

```
