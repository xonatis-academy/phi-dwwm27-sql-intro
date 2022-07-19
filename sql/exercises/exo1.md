# Requêtes avec FROM

### Selectionner toutes les colonnes de la table categories

```sql
SELECT * FROM exo1_categories;
```

### Selectionner toutes les colonnes de la table utilisateur

```sql
SELECT * FROM exo1_users;
```

### Selectionner toutes les references des commandes

```sql
SELECT reference FROM exo1_orders;
```

### Selectionner toutes les dates des commandes

```sql
SELECT created_at FROM exo1_orders;
```

### Selectionner toutes les quantites des commandes

```sql
SELECT quantity FROM exo1_order_details;
```

# Requêtes avec WHERE

### Quel est le prix du produit 4 ?

```sql
SELECT price FROM exo1_products WHERE id = 4;
```

### Quel est le prenom de l'utilisateur qui a l'adresse email leo.part@gmail.com ?

```sql
SELECT firstname FROM exo1_users WHERE email = 'leo.part@gmail.com';
```

### Quel est le numero de l'utilisateur qui a passé la commande de reference 94809503 ?

```sql
SELECT user_id FROM exo1_orders WHERE reference = '94809503';
```

### A quelle date s'est faite la commande de reference 39820342 ?

```sql
SELECT created_at FROM exo1_orders WHERE reference = '39820342';
```

# Requêtes avec GROUP BY

### Quel est le nombre de commandes par numero d'utilisateur ?

```sql
SELECT user_id, COUNT(id) AS nombre_de_commandes FROM exo1_orders GROUP BY user_id
```

### Quel est la quantite totale commandée par numero de commande ?

```sql
SELECT order_id AS id_de_commande, SUM(quantity) AS quantite_totale FROM exo1_order_details GROUP BY order_id;
```

### Quel est la quantite totale commandée par numero de produit ?

```sql
SELECT product_id, SUM(quantity) AS quantite_totale FROM exo1_order_details GROUP BY product_id;
```

### Quel est le nombre de commandes par numero de produit ?

```sql
SELECT product_id, COUNT(order_id) FROM exo1_order_details GROUP BY product_id;
```

### Quel est le nombre de produits par numero de commande ?

```sql
SELECT order_id, COUNT(product_id) FROM exo1_order_details GROUP BY order_id;
```

# Requêtes avec HAVING

### Quels sont les clients ayant passé 2 commandes ?

```sql
SELECT user_id FROM exo1_orders GROUP BY user_id HAVING COUNT(id) >= 2;
```

### Quelles sont les commandes ayant 3 produits différents ?

```sql
SELECT order_id FROM exo1_order_details GROUP BY order_id HAVING COUNT(product_id) = 3;
```

### Quelles sont les commandes ayant 6 articles à expédier ?

```sql
SELECT order_id FROM exo1_order_details GROUP BY order_id HAVING SUM(quantity) = 6;
```

# Requêtes avec ORDER BY, LIMIT

## Quelle est la commande la plus récente ?

```sql
SELECT * FROM exo1_orders ORDER BY created_at DESC LIMIT 1;
```

### Quelle est la commande la plus anciennce ?

```sql
SELECT * FROM exo1_orders ORDER BY created_at ASC LIMIT 1;
```

### Quel est le nom des 3 produits qui coutent le plus chers ?

```sql
SELECT name FROM exo1_products ORDER BY price DESC LIMIT 3;
```

### Quelle sont les références des 2 commande les plus récentes ?

### Quels sont les 2 produits les plus populaires (qui ont été commandés le plus de fois) ?

# Requêtes avec JOIN

### Quelles sont toutes les informations des utilisateurs et des commandes ?

```sql
SELECT * 
FROM  exo1_users u 
LEFT OUTER JOIN exo1_orders o ON o.user_id = u.id;
```

### Quel est l'adresse email de l'utilisateur ayant passé la commande 39820342 ?

```sql
SELECT exo1_users.email FROM exo1_users 
LEFT OUTER JOIN exo1_orders ON exo1_users.id = exo1_orders.user_id
WHERE exo1_orders.reference = '39820342';
```

### Quel est le prenom de l'utilisateur ayant passé la commande 39820342 ?

```sql
SELECT exo1_users.firstname 
FROM exo1_users 
LEFT OUTER JOIN exo1_orders ON exo1_users.id = exo1_orders.user_id
WHERE exo1_orders.reference = '39820342';
```

### Quels sont les numeros de produits commandés et la référence de la commande associée ?

```sql
SELECT exo1_order_details.product_id, exo1_orders.reference 
FROM exo1_order_details 
LEFT OUTER JOIN exo1_orders ON exo1_order_details.order_id = exo1_orders.id;
```

### Quels sont les noms des produits et leur quantité commandée ?

```sql
SELECT exo1_order_details.quantity, exo1_products.name 
FROM exo1_order_details 
LEFT OUTER JOIN exo1_products ON exo1_order_details.product_id = exo1_products.id;
```

### Quels sont les noms et les prix de produits commandés et la référence de la commande associée ?

```sql
SELECT exo1_products.name, exo1_products.price, exo1_orders.reference 
FROM exo1_products 
JOIN exo1_order_details ON exo1_order_details.product_id = exo1_products.id
JOIN exo1_orders ON exo1_orders.id = exo1_order_details.order_id
```

# BONUS

### Filtrer sur l'année d'une date

```sql
SELECT * FROM exo2_donnees WHERE YEAR(jour) = '2020';
```

### Filtrer les doublons

```sql
SELECT DISTINCT(jour) FROM exo2_donnees;
```

### Filtrer en limitant le nombre

```sql
SELECT * FROM exo2_donnees LIMIT 3;
```

```sql
SELECT * FROM exo2_donnees LIMIT 3 OFFSET 2;
```

```sql
SELECT * FROM exo2_donnees LIMIT 2, 3;
```

### Faire des operations

```sql
SELECT SUM(hosp + rea + rad + dc) AS charge_hopital FROM exo2_donnees;
```