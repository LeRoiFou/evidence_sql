---
sidebar_position: 22
---

# L'opérateur PARTITION BY

---

## <u>Requête n° 1</u>

Donner le top 3 des meilleurs vendeurs en terme de CA par année

<!-- Requêtes SQL -->

```sql query1
-- Colonnes récupérées
select
    cast(cast(e.EmployeID as int)as varchar) as e_EmployeID
    , e.Nom
    , e.Prenom
    , year(s.DateVente) as Annee
    , round(sum(s.MontantTotal), 0) as total_sales
    -- Classement
    , dense_rank() over(
        -- Fraction par année
        partition by Annee
        -- Trie
        order by sum(s.MontantTotal) desc) as Classement
-- BD récupérées
from data.Employes e
join data.Ventes s
on e.EmployeID = s.EmployeID
-- TCD
group by
    e_EmployeID
    , e.Nom
    , e.Prenom
    , Annee
-- Trie
order by Annee asc
```

```sql query2
-- Colonnes récupérée
select
    q1.e_EmployeID as Employe
    , q1.Nom
    , q1.Prenom
    , q1.Annee
    , q1.total_sales as Montant
    , q1.Classement
-- BD récupérée
from ${query1} q1
-- Filtre
where q1.Classement between 1 and 3;
```

<!-- Table -->

<DataTable data={query2} rowShading=true rows=12 totalRow=true>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=Employe align=center/>
    <Column id=Annee align=center fmt=#### totalAgg=Total/>
    <Column id=Montant align=center fmt='# ### " €"' contentType=colorscale scaleColor=Brown/>
    <Column id=Classement align=center totalAgg='-'/>
</DataTable>

<!-- Graphique -->

<BarChart
    data={query2}
    x=Nom
    y=Montant
    series=Annee
    labels=true
    yFmt=eur1k
    chartAreaHeight=250
/>

## <u>Requête n° 2</u>

Donner le top 3 des meilleurs clients en terme de chiffre d'affaires par année et par trimestre

<!-- Requêtes SQL -->

```sql query3
-- Colonnes récupérées
select
    cast(cast(c.ClientID as int)as varchar) as c_ClientID
    , c.Nom
    , c.Prenom
    , year(s.DateVente) as Annee
    , quarter(s.DateVente) as Trimestre
    , round(sum(s.MontantTotal), 0) as total_sales
    -- Classement
    , dense_rank() over (
        -- Fraction
        partition by (Annee, Trimestre)
        -- Trie
        order by sum(s.MontantTotal) desc) as Classement
-- BD récupérées
from data.Clients c
join data.Ventes s
on c.ClientID = s.ClientID
-- TCD
group by
    c_ClientID
    , c.Nom
    , c.Prenom
    , Annee
    , Trimestre
-- Trie
order by
    Annee
    , Trimestre
```

```sql query4
-- Colonnes récupérées
select
    q4.Nom
    , q4.Prenom
    , q4.c_ClientID AS Numero
    , q4.Annee
    , q4.Trimestre
    , q4.total_sales as Montant
    , q4.Classement
-- BD récupérée
from ${query3} q4
-- Filtre
where q4.Classement between 1 and 3;
```

<!-- Table -->

<DataTable data={query4} search=true rowShading=true rows=12 totalRow=true>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=Numero align=center/>
    <Column id=Annee align=center fmt='####' totalAgg='-'/>
    <Column id=Trimestre align=center fmt='####' totalAgg='Moyenne'/>
    <Column id=Montant align=center fmt='# ### " €"' totalAgg=mean contentType=colorscale scaleColor=orange/>
    <Column id=Classement align=center/>
</DataTable>
