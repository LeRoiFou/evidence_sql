---
sidebar_position: 5
---

# L'opérateur BETWEEN

---

## <u>Ensemble des ventes du 1er trimestre 2021</u>

<!-- Requête SQL -->

```sql ex1
-- Colonnes récupérées
select s.*
-- BD récupérée
from data.Ventes s
-- Filtre
where s.DateVente between '2021-01-01' and '2021-03-31'
-- Trie
order by
    month(s.DateVente) asc
    , day(s.DateVente) asc
    , s.VenteID asc;
```

<!-- Table -->
<DataTable data={ex1} search=true rowShading=true totalRow=true>
    <Column
        id=VenteID
        title="N° vente"
        align=center
        totalAgg=""
    />
    <Column
        id=DateVente
        title="Date"
        align=center
        totalAgg=""
    />
    <Column
        id=ClientID
        title="Client ID"
        align=center
        totalAgg=""
    />
    <Column
        id=EmployeID
        title="Employe ID"
        align=center
        totalAgg=""
    />
    <Column
        id=ProduitID
        title="N° Produit"
        align=center
        totalAgg="Total"
    />
    <Column
        id=QuantiteVendue
        title="Quantité vendue"
        align=center
        totalAgg=sum
        fmt='# ##0'
        contentType=colorscale
        scaleColor='#40bcb8'
    />
    <Column
        id=MontantTotal
        title="Montant total"
        align=center
        totalAgg=sum
        fmt='# ### " €"'
        contentType=colorscale
        scaleColor='#40bcb8'
    />
</DataTable>

<!-- Graphiques -->

<BarChart
    data={ex1}
    x=DateVente
    y=QuantiteVendue
    labels=true
    title="Quantités vendues au 1er trimestre 2021"
/>

<BarChart
    data={ex1}
    x=DateVente
    y=MontantTotal
    yFmt='# ### " €"'
    labels=true
    title="CAHT au 1er trimestre 2021"
/>
