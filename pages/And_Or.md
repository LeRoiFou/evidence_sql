---
sidebar_position: 3
---

# Les opérateurs AND et OR

---

### <u>Produits dont le prix est compris entre 50 € et 100 €</u>

<!-- Requête SQL -->

```sql ex1
-- Colonnes récupérées
select p.*
-- BD récupérée
from data.Produits p
-- Filtre
where p.PrixUnitaire >= 50 and p.PrixUnitaire <=100
-- Trie
order by p.PrixUnitaire asc;
```

<!-- Table -->

<DataTable data={ex1} search=true rowShading=true totalRow=true row=7>
    <Column
        id=ProduitID
        title="Produit n°"
        align=center
        totalAgg=""
    />
    <Column
        id=NomProduit
        title=Nom
        align=center
        totalAgg=""
    />
    <Column
        id=Description
        title=Description
        align=center
        wrap=true
        totalAgg="Prix compris entre 50 € et 100 € "
    />
    <Column
        id=PrixUnitaire
        title="Prix unitaire"
        align=center
        totalAgg=mean
        fmt='# ###0 "€"'
        contentType=colorscale
        scaleColor='#40bcb8'
    />
    <Column
        id=FournisseurID
        title="ID Fournisseur"
        align=center
        totalAgg=""
    />
</DataTable>

<!-- Graphique -->

<BarChart
    data={ex1}
    x=NomProduit
    y=PrixUnitaire
    yFmt='# ###0 "€"'
    swapXY=true
    title="Prix moyen des produits compris entre 50 et 100 €"
/>

<br>

### <u>Produits vendus par le fournisseur n° 12 ou le fournisseur n° 13</u>

<!-- Requête SQL -->

```sql ex2
-- Colonnes récupérées
select p.*
-- BD récupérée
from data.Produits p
-- Filtre
where p.FournisseurID = 12 or p.FournisseurID = 13
-- Trie
order by
    p.FournisseurID asc
    , p.PrixUnitaire asc;
```

<!-- Table -->

<DataTable data={ex2} rowShading=true>
    <Column
        id=FournisseurID
        title="ID Fournisseur"
        align=center
    />
    <Column
        id=ProduitID
        title="Produit n°"
        align=center
    />
    <Column
        id=NomProduit
        title=Nom
        align=center
    />
    <Column
        id=Description
        title=Description
        align=center
        wrap=true
    />
    <Column
        id=PrixUnitaire
        title="Prix unitaire"
        align=center
        fmt='# ###0 "€"'
    />
    
</DataTable>
