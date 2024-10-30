---
sidebar_position: 7
---

# L'opérateur LIMIT

---

## <u>Donner la liste des 10 premiers clients par ordre alphabétique</u>

<!-- Requêtes SQL -->

```sql ex1
-- Récupération des colonnes
select
    c.ClientID
    , c.Nom
    , c.Prenom
    , c.Email
    , c.NumeroTelephone
-- BD récupérée
from data.Clients c
-- Trie
order by
    c.Nom
    , c.Prenom
-- Affichage limité
limit 10;
```

<!-- Table -->

<DataTable data={ex1} row=10 rowShading=true>
    <Column
        id=Nom
        align=center
    />
    <Column
        id=Prenom
        align=center
    />
    <Column
        id=Email
        align=center
    />
    <Column
        id=NumeroTelephone
        title="Numero telephone"
        align=center
    />
    <Column
        id=ClientID
        title="N° client"
        align=center
    />
</DataTable>

## <u>Donner la liste des 10 produits les plus chers</u>

<!-- Requête SQL -->

```sql ex2
-- Colonnes récupérées
select
    p.NomProduit
    , p.PrixUnitaire
    , p.ProduitID
    , p.FournisseurID
-- BD récupérée
from data.Produits p
-- Trie
order by
    p.PrixUnitaire desc
    , p.ProduitID asc
-- Affichage
limit 10;
```

<!-- Table -->

<DataTable data={ex2} row=10 rowShading=true totalRow=true>
    <Column
        id=NomProduit
        title=Nom
        align=center
        totalAgg="Prix unitaire moyen"
    />
    <Column
        id=PrixUnitaire
        title="Prix unitaire"
        align=center
        totalAgg=mean
        fmt='# ### " €"'
    />
    <Column
        id=ProduitID
        title="N° produit"
        align=center
        totalAgg=""
    />
    <Column
        id=FournisseurID
        title="N° Fournisseur"
        align=center
        totalAgg=""
    />
</DataTable>

<!-- Graphique -->

<BarChart
data={ex2}
x=NomProduit
y=PrixUnitaire
swapXY=true
yFmt='# ### " €"'
labels=true
title="Prix moyen des 10 produits les plus chers"
/>
