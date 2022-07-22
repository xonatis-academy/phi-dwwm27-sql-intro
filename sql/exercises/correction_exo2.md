# TP : Faisons des statistiques sur le covid !

### 1) Combien y a-t-il de départements enregistrés ?

```sql
178
```

### 2) Combien y a-t-il d'enregistrements dans la table des prélèvements ?

```
94839
```

### 3) Quelle est la date du dernier prélèvement ?

`2021-01-24`

```sql
SELECT jour FROM exo2_donnees ORDER BY jour DESC LIMIT 1;
```

### 4) Quelle est la date du premier prélèvement ?

`2020-03-18`

```sql
SELECT jour FROM exo2_donnees ORDER BY jour ASC LIMIT 1;
```

### 5) Sur l'ensemble des données, combien d'hommes ont été touchés (hospitalisés) par la covid ?

`2663153`

```sql
SELECT SUM(hosp) FROM exo2_donnees WHERE sexe = 1;
```

### 6) Sur l'ensemble des données, combien de femmes ont été touchés (hospitalisés) par la covid ?

`2458589`

```sql
SELECT SUM(hosp) FROM exo2_donnees WHERE sexe = 2;
```

### 7) Sur l'année 2020, combien de personnes au total ont été touchées par la covid ?

`4569985`

```sql
SELECT SUM(hosp) FROM exo2_donnees WHERE sexe = 0 AND YEAR(jour) = '2020';
```

### 8) Sur l'année 2021, quel a été la charge des hopitals (patients totals à gérer, entrées et sorties) ?

`6744647`

```sql
SELECT SUM(hosp + rea + rad + dc) FROM exo2_donnees WHERE sexe = 0 AND YEAR(jour) = '2021';
```

### 9) Quel est le nombre de décès par département ? Pouvez-vous m'envoyer une capture d'écran du résultat ?

`capture`

```sql
SELECT exo2_departements.nom, SUM(exo2_donnees.dc) FROM
exo2_departements LEFT OUTER JOIN exo2_donnees
ON exo2_departements.code = exo2_donnees.dep
WHERE exo2_donnees.sexe = 0
GROUP BY exo2_departements.nom;
```

### 10) Quel est le département le plus touché (décès) par le covid en 2021 ?

`Nord 98952`

```sql
SELECT exo2_departements.nom, SUM(exo2_donnees.dc) AS deces_total FROM
exo2_departements LEFT OUTER JOIN exo2_donnees
ON exo2_departements.code = exo2_donnees.dep
WHERE exo2_donnees.sexe = 0 AND YEAR(jour) = '2021'
GROUP BY exo2_departements.nom
ORDER BY deces_total DESC LIMIT 1;
```

### 11) Quel est le département le plus moins (décès) par le covid en 2021 ?

`Haute-Corse 966`

```sql
SELECT exo2_departements.nom, SUM(exo2_donnees.dc) AS deces_total FROM
exo2_departements LEFT OUTER JOIN exo2_donnees
ON exo2_departements.code = exo2_donnees.dep
WHERE exo2_donnees.sexe = 0 AND YEAR(jour) = '2021'
GROUP BY exo2_departements.nom
ORDER BY deces_total ASC LIMIT 1;
```

### 12) Quelle est la liste des 10 départements où il y a le plus de retour à domicile en France en 2021 ?

`capture`

```sql
SELECT exo2_departements.nom, SUM(exo2_donnees.rad) AS retours FROM
exo2_departements LEFT OUTER JOIN exo2_donnees
ON exo2_departements.code = exo2_donnees.dep
WHERE exo2_donnees.sexe = 0 AND YEAR(jour) = '2021'
GROUP BY exo2_departements.nom
ORDER BY retours DESC LIMIT 10;
```

### 13) Quel est le département qui a le plus grand ratio retour à domicile / hospitalisé en France l'année derniere ?

`Guyane (francaise) 21.5926`

```sql
SELECT exo2_departements.nom, SUM(rad)/SUM(hosp) AS ratio FROM
exo2_departements LEFT OUTER JOIN exo2_donnees
ON exo2_departements.code = exo2_donnees.dep
WHERE exo2_donnees.sexe = 0 AND YEAR(jour) = '2020'
GROUP BY exo2_departements.nom
ORDER BY ratio DESC LIMIT 1;
```