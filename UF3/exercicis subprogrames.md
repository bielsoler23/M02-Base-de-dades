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
