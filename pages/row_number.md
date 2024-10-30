---
sidebar_position: 25
---

# L'opérateur ROW NUMBER

---

## <u>Requête n° 1</u>

Classer les ventes de la plus ancienne à la plus récente en ajoutant le numéro de ligne

<!-- Requête SQL -->

```sql query1
-- Colonnes récupérées
select
    s.DateVente
    , cast(cast(s.ClientID as int) as varchar) as c_ClientID
    , s.QuantiteVendue
    , s.MontantTotal
    -- Nouvelle colonne : classement par numérotation selon la date de vetne
    , row_number() over (partition by year(s.DateVente) order by s.DateVente) as Sales_number
-- BD récupérée
from data.Ventes s;
```

<!-- Table -->

<DataTable data={query1} search=true rowShading=true totalRow=true rows=15>
    <Column id=DateVente title=Date align=center fmt='dd/mm/yyyy'/>
    <Column id=c_ClientID title='N° Client' align=center totalAgg=Moyenne/>
    <Column id=QuantiteVendue title='Quantite vendue' align=center totalAgg=mean/>
    <Column id=MontantTotal title=CAHT align=center fmt='### ### " €"' totalAgg=mean contentType=colorscale scaleColor=brown/> 
    <Column id=Sales_number title='N° vente' align=center totalAgg='-'/>
</DataTable>

## <u>Requête n° 2</u>

Classer les 3 ventes les plus importantes par année en ajoutant le numéro de ligne

<!-- Requête SQL - VIEW -->

```sql query2
-- Colonnes récupérée
select
    s.DateVente
    , sum(s.MontantTotal) as Total_sales
    -- Nouvelle colonne : classement par numérotation selon le CAHT total
    , row_number() over (partition by year(s.DateVente) order by Total_sales desc) as Classification
-- BD récupéréee
from data.Ventes s
-- TCD
group by s.DateVente
```

<!-- Requête SQL -->

```sql query3
-- Colonnes récupérées
select
    q2.DateVente
    , q2.Total_sales
    , q2.Classification
-- BD récupérée (VIEW)
from ${query2} q2
-- Filtre
where q2.Classification between 1 and 3;
```

<DataTable data={query3} rowShading=true rows=12>
    <Column id=DateVente title=Date align=center fmt='dd/mm/yyyy'/>
    <Column id=Total_sales tile=CAHT align=center fmt='### ### " €"' contentType=colorscale scaleColor=orange/>
    <Column id=Classification align=center/>
</DataTable>
