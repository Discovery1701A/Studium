Geben Sie für die unten stehenden DB-Anfragen jeweils einen SQL-Select-Ausdruck bezogen auf die Mondial-Datenbank (mondial.sql im Ordner [Datenbanken](https://moodle.hs-emden-leer.de/moodle/mod/url/view.php?id=323657 "Datenbanken")) an. Die Zusammenhänge der Tabellen sind anhand des [ER-Modells](https://ipfs.ddnss.org/ipfs/QmY9aPngBfXMot1JCsnnWsxVdaguTebigQVf4vnpsTauUF) ersichtlich.
![[QmY9aPngBfXMot1JCsnnWsxVdaguTebigQVf4vnpsTauUF 1.pdf]]

1. Geben Sie alle Städte mit mehr als 9000000 Einwohnern aus.

```SQL
SELECT name, population
FROM city
WHERE population > 9000000;
```

2. Geben Sie aus, wie viele Städte mehr als 9000000 Einwohner vorweisen.

```SQL
SELECT COUNT(*) AS anzahl_grosse_staedte
FROM city
WHERE population > 9000000;
```

3. Geben Sie alle Städte mit mehr als 9000000 Einwohnern und dem zugehörigen Land aus.

```SQL
SELECT city.name As Stadt, city.population , country.name AS Land
FROM city, country
WHERE city.population > 9000000
AND city.country = country.code;
```

4. Geben Sie die Kürzel aller Länder aus, in denen es mindestens zwei Städte mit mehr als 5000000 Einwohner gibt.
  
  ```SQL
SELECT country
FROM city
WHERE population > 5000000
GROUP BY country
HAVING count(*) >= 2;
  ```
  
5. Geben Sie die unterschiedlichen Namen aller Länder in alphabetischer Reihenfolge aus, in denen es mindestens zwei Städte mit mehr als 5000000 Einwohner gibt.!

```SQL
SELECT country.name, count(*) AS Anzahl
FROM city, country
WHERE city.country = country.code
AND city.population > 5000000
GROUP BY country.name
HAVING count(*) >= 2
ORDER BY country.name ASC;
```

6. Geben Sie für jedes Land in Europa in Prozent an, welchen Anteil die Landesfläche an der Fläche von Gesamteuropa hat (Ausgabe: Name des Landes, Prozent).

```SQL
SELECT Name AS Country_Name,
ROUND(((Area* Encompasses.Percentage /100) / (SELECT SUM(Area * Encompasses.Percentage /100)
FROM Country, Encompasses
WHERE Country.code = Encompasses.Country AND Encompasses.Continent = 'Europe')) * 100, 2) AS Durchschnittsfläche_Europa_Area
FROM Country, Encompasses
WHERE Country.code = Encompasses.Country AND Encompasses.Continent = 'Europe'
ORDER BY Durchschnittsfläche_Europa_Area DESC;
```

7. Geben Sie für jedes Land die Anzahl der Städte mit mehr als 5000000 Einwohner aus (Ausgabe: Name des Landes, Anzahl).

```SQL
SELECT Country.Name AS Name_des_Landes, count(*) AS Anzahl
FROM City, Country
WHERE City.Country = Country.Code
AND City.Population > 5000000
GROUP BY Country.Name
ORDER BY Anzahl DESC;
```

8. Geben Sie die Namen aller Länder aus, für die eine Stadt keine Einwohnerzahl (somit NULL) vorweist.

```SQL
SELECT Country.Name
FROM Country
WHERE Country.code IN
(SELECT City.Country
FROM City
WHERE City.Population IS NULL);
```

9. Geben Sie den Ländernamen, den Namen der zugehörigen Hauptstadt und die Einwohnerzahl dieser Hauptstadt aller Länder in Amerika (Kontinent) sortiert nach den Ländernamen aus.

```SQL
SELECT Country.Name, Country.Capital,
(SELECT City.Population
FROM City
WHERE City.Name = Country.Capital AND City.Country = Country.Code) AS Hauptstadtbevölkerung
FROM Country,Encompasses
WHERE Country.Code = Encompasses.Country
AND Encompasses.Continent LIKE '%America%'
ORDER BY Country.Name ;
```

10. Geben Sie die Namen aller Länder in Europa aus, für die weder ein Fluss (GEO_RIVER) noch eine Wüste (GEO_DESERT) eingetragen sind.

```SQL
SELECT Country.Name
FROM Country, Encompasses
WHERE Country.Code = Encompasses.Country
AND Encompasses.Continent = 'Europe'
AND Country.Code NOT IN (SELECT GEO_RIVER.Country FROM GEO_RIVER)
AND Country.Code NOT IN (SELECT GEO_DESERT.Country FROM GEO_DESERT);
```

11. Geben Sie die Namen aller Länder aus, für die bei jeder Stadt dieses Landes keine Einwohnerzahl (also NULL) eingetragen ist.
  
  ```SQL
SELECT Country.Name
FROM Country
WHERE Country.Code NOT IN (
SELECT DISTINCT City.Country
FROM City
WHERE City.Population IS NOT NULL);
  ```
  
12. Geben Sie die Namen aller Länder aus, deren Hauptstadt weniger als 500000 Einwohner hat und für die mehr als fünf Städte in der Datenbank eingetragen sind.

 ```SQL
SELECT Country.Name
FROM Country
WHERE Country.Code IN (SELECT City.Country
FROM City
WHERE City.Population < 500000)
AND Country.Code IN (SELECT City.Country
FROM City
GROUP BY City.Country
HAVING COUNT(*) > 5);
  ```
  
13. Geben Sie die Namen der Länder an, die an kein Meer (sea) grenzen und deren Hauptstadt an einem Fluss liegt (located).

 ```SQL
SELECT Country.Name
FROM Country
WHERE Country.Code NOT IN (SELECT DISTINCT Located.Country
FROM Located
WHERE Located.Sea is not Null)
AND Country.Capital IN (SELECT DISTINCT Located.City
FROM Located
WHERE Located.River is not Null
AND Located.Country = Country.Code);
  ```
  
14. Geben Sie alphabetisch sortiert die Namen aller Städte aus, deren Breitengrad maximal einen Grad Differenz zur geographischen Breite von Berlin hat (Berlin selbst soll sich im Ergebnis befinden).

 ```SQL
SELECT City.Name
FROM City
WHERE City.latitude >
(SELECT City.latitude
FROM City
WHERE City.Name = 'Berlin') - 1
AND City.latitude <
(SELECT City.latitude
FROM City
WHERE City.Name = 'Berlin') + 1
ORDER BY City.Name ASC;
  ```
  
15. Geben Sie einmalig die Namen der Länder aus, von denen eine Stadt am Atlantik (Atlantic Ocean) und eine Stadt am Mittelmeer (Mediterranean Sea) liegen.

 ```SQL
SELECT DISTINCT Country.Name
FROM Country
WHERE Country.Code IN (SELECT Located.Country
FROM Located
WHERE Located.Sea = 'Atlantic Ocean'
GROUP BY Located.Country
HAVING COUNT(*) = 1)
AND Country.Code IN (SELECT Located.Country
FROM Located
WHERE Located.Sea = 'Mediterranean Sea'
GROUP BY Located.Country
HAVING COUNT(*) = 1);
  ```