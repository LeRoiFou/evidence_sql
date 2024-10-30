---
sidebar_position: 2
---

# L'opérateur WHERE

---

### <u>Liste des produits vendus > à 200 €</u>

<!-- Requête SQL -->

```sql ex1
-- Colonnes récupérées
select
    p.ProduitID
    , p.NomProduit
    , p.PrixUnitaire
-- BD récupérée
from data.Produits p
-- Filtre
where p.PrixUnitaire > 200
-- Trie
order by p.PrixUnitaire asc;
```

<!-- Table
search = recherche dans le tableau
rowShading = bordure des lignes
totalRow = total des colonnes
rows = nombre de lignes à afficher
title = modification de l'en-tête
align = alignement
totalAgg = nom de la cellule total
fmt = mise en forme des données numériques
contentType = échelle de couleur des cellules
scaleColore = couleurs attribuées aux cellules
wrap= ajustement de la largeur de la colonne
-->

<div class='table-css'>
<DataTable data={ex1} search=true rowShading=true totalRow=true rows=5>
    <Column 
        id=ProduitID
        title='N° du produit'
        align=center
        totalAgg=""/>
    <Column 
        id=NomProduit 
        title='Nom' 
        align=center
        totalAgg="Prix moyen des produits vendus > à 200 €"/>
    <Column 
        id=PrixUnitaire 
        title='Prix unitaire' 
        align=center
        fmt='# ##0" €"' 
        totalAgg=mean
        contentType=colorscale
        scaleColor='#40bcb8'/>
</DataTable>
</div>

### <u>Information sur le produit "Nike Air Max"</u>

<!-- Requête SQL -->

```sql ex2
--- Colonnes récupérées
select p.*
-- BD récupérée
from data.Produits p
-- Filtre
where p.NomProduit like 'Nike Air Max'
-- Trie
order by p.PrixUnitaire asc;
```

<!-- Table -->

<DataTable data={ex2} search=true rowShading=true totalRow=true>
    <Column
        id=ProduitID
        title='Produit ID'
        align=center
        totalAgg=""/>
    <Column
        id=NomProduit
        title='Nom'
        align=center
        totalAgg=""/>
    <Column
        id=Description
        align=center
        totalAgg="Prix moyen des produits vendus"
        wrap=true/>
    <Column
        id=PrixUnitaire
        title='Prix unitaire'
        align=center
        fmt='# ##0" €"' 
        totalAgg=mean
        contentType=colorscale
        scaleColor='#40bcb8'/>
    <Column
        id=FournisseurID
        title='Fournisseur ID'
        align=center
        totalAgg=""/>
</DataTable>

### <u>Information sur les produits du fournisseur n° 13</u>

<!-- Requête SQL -->

```sql ex3
-- Colonnes récupérées
select p.*
-- BD récupérée
FROM data.Produits p
-- Filtre
where FournisseurID = 13
-- Trie
order by p.PrixUnitaire asc;
```

<!-- Table -->

<DataTable data={ex3} rowShading=true totalRow=true>
    <Column
        id=ProduitID
        title="Produit ID"
        align=center
        totalAgg=""/>
    <Column
        id=NomProduit
        title="Nom"
        align=center
        totalAgg=""/>
    <Column
        id=Description
        align=center
        wrap=true
        totalAgg="Prix moyen des produits vendus"/>
    <Column
        id=PrixUnitaire
        title="Prix unitaire"
        align=center
        fmt='# ###0" €"'
        totalAgg=mean/>
    <Column
        id=FournisseurID
        title="ID Fournisseur"
        align=center
        totalAgg=""/>
</DataTable>

<!-- Graphique -->

<BarChart 
    data={ex3}
    x=NomProduit
    y=PrixUnitaire
    swapXY=true
    yFmt='# ###0" €"'
    title="Produits du fournisseur n° 13"
    sort=false
/>

<!-- ******** Style opéré sous format CSS ******** -->

<style>

.table-css { /*pour les tables*/
        width: 80%; /*largeur du tableau*/
        margin: 0 auto; /*tableau centré sur la page*/
    }
    
</style>
