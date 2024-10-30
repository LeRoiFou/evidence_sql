---
sidebar_position: 23
---

# L'opérateur LAG

---

## <u>Requête n° 1</u>

Créer une colonne sur l'évolution du CA année par année par taux de croissance

<!-- Requête SQL -->

```sql query1
-- Colonnes récupérées
select
    year(s.DateVente) as Annee
    , round(sum(s.MontantTotal), 0) as Total_sales
    -- Variation du CAHT en %
    , (Total_sales - lag(Total_sales) over (order by Annee)) / (lag(Total_sales) over (order by Annee)) * 100 as Variation
-- BD récupérée
from data.Ventes s
-- TCD
group by Annee;
```

<!-- Table -->

<DataTable data={query1} rowShading=true totalRow=true>
    <Column id=Annee align=center fmt='####' totalAgg='CAHT moyen'/>
    <Column id=Total_sales title=CAHT align=center fmt='### ### " €"' totalAgg=mean contentType=colorscale scaleColor=brown/>
    <Column id=Variation title="Taux de croissance" align=center fmt='### " %"' totalAgg=''/>
</DataTable>

<!-- Graphique -->

<BarChart
    data={query1}
    x=Annee
    y=Total_sales
    labels=true
/>

## <u>Requête n° 2</u>

Quel est le montant total des ventes par trimestre et par année et comment le CA évolue d'un trimestre à l'autre

<!-- Requête SQL -->

```sql query2
-- Colonnes récupérées
select
    quarter(s.DateVente) as quater_sales
    , year(s.DateVente) as year_sales
    , sum(s.MontantTotal) as total_sales
    -- Variation du CAHT par trimestre en €
    , coalesce((total_sales - lag(total_sales) over (order by year_sales, quater_sales)), 0) as variation1
    -- Variation du CAHT par trimestre en %
    , coalesce(variation1 / (lag(total_sales) over (order by year_sales, quater_sales)) * 100, 0) as variation2
-- BD récupérée
from data.Ventes s
-- TCD
group by
    quater_sales
    , year_sales;
```

<!-- Table -->

<DataTable data={query2} search=true rowShading=true rows=8 totalRow=true>
    <Column id=year_sales title=Annee align=center fmt=#### totalAgg=''/>
    <Column id=quater_sales title=Trimestre align=center totalAgg='Moyenne'/>
    <Column id=total_sales title=CAHT align=center fmt='### ### " €"' totalAgg=mean contentType=colorscale scaleColor=orange/>
    <Column id=variation1 title=Ecart align=center fmt='### ### " €"' totalAgg=''/>
    <Column id=variation2 title='Ecart en %' align=center fmt='### " %"' totalAgg=''/>
</DataTable>
