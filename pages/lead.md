---
sidebar_position: 24
---

# L'opérateur LEAD

## <u>Requête</u>

Ajouter pour chaque année, une colonne avec le CA de l'année précédente et une colonne avec le CA de l'année suivante

<!-- Requête SQL -->

```sql query1
-- Colonnes récupérées
select
    year(s.DateVente) as year_sales
    , sum(s.MontantTotal) as total_sales
    -- CAHT N-1
    , lag(total_sales) over (order by year_sales) as "N-1"
    -- CAHT N+1
    , lead(total_sales) over (order by year_sales) as "N+1"
-- BD récupérée
from data.Ventes s
-- TCD
group by year_sales;
```

<DataTable data={query1} rowShading=true totalRow=True>
    <Column id=year_sales title=Annee align=center totalAgg=Moyenne fmt=####/>
    <Column id=total_sales title=CAHT align=center totalAgg=mean fmt='### ### " €"'/>
    <Column id="N-1" title="CAHT N-1" align=center totalAgg=mean fmt='### ### " €"'/>
    <Column id="N+1" title="CAHT N+1" align=center totalAgg=mean fmt='### ### " €"'/>
</DataTable>
