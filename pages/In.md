---
sidebar_position: 4
---

# L'opérateur IN

---

## <u>Sélectionner les noms des produits vendus par les fournisseurs n° 13, 15, 45, 55, 89</u>

<!-- Requête SQL -->

```sql ex1
-- Colonnes à récupérer
select
    p.NomProduit
    , p.FournisseurID
    , p.PrixUnitaire
-- BD à récupérer
from data.Produits p
-- Filtre
where p.FournisseurID IN (13, 15, 45, 55, 89)
-- Trie
order by
    p.FournisseurID asc
    , p.PrixUnitaire asc
```

<!-- Table -->
<DataTable data={ex1} search=true rowShading=true totalRow=true>
    <Column
        id=FournisseurID
        title="Fournisseur ID"
        align=center
        totalAgg=""
    />
    <Column
        id=NomProduit
        title="Nom du produit"
        align=center
        totalAgg="Prix moyen pratiqué par ces fournisseurs"
    />
    <Column
        id=PrixUnitaire
        title="Prix unitaire"
        align=center
        fmt='# ###0 " €"'
        totalAgg=mean
    />
</DataTable>

<!-- Graphique -->

<BarChart
    data={ex1}
    x=NomProduit
    y=PrixUnitaire
    swapXY=true
    yFmt='# ###0 " €"'
    title="Prix moyen des produits"
/>
