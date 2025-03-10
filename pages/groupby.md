---
sidebar_position: 13
---

# L'opérateur GROUP BY

---

## <u>Requête n° 1</u>

_Le n° ID des 10 employés qui réalisent le CAHT le plus élevé_

<!-- Requête SQL -->

```sql ex1
-- Récupération des colonnes
select
    cast(cast(s.EmployeID as int) as varchar) as EmployeID
    , round(sum(s.MontantTotal), 0) as sales_total
-- BD récupérée
from data.Ventes s
-- TCD
group by s.EmployeID
-- Trie
order by sales_total desc
-- Affichage
limit 10;
```

<!-- Table -->

<DataTable data={ex1} rowShading=true totalRow=true>
    <Column id=EmployeID title="N° Employe" fmt=## align=center totalAgg="Total"/>
    <Column id=sales_total title="Montant des ventes" align=center totalAgg=sum fmt='# ### " €"' contentType=colorscale scaleColor='cyan'/>
</DataTable>

<!-- Graphique -->

<BarChart
data={ex1}
x=EmployeID
y=sales_total
swapXY=true
title="Les 10 meilleurs employés"
subtitle="Classement par n° ID des employés"
labels=true
yFmt='# ### " €"'
chartAreaHeight=300
fillColor='cyan'
/>

## <u>Requête n° 2</u>

_Nombre de ventes réalisé par employé par ordre décroissant_

<!-- Requête SQL -->

```sql ex2
-- Colonnes récupéres
select
    s.EmployeID
    , count(distinct(s.VenteID)) as quantity
-- BD récupérée
from data.Ventes s
-- TCD
group by s.EmployeID
-- Trie
order by quantity desc;
```

<!-- Table -->

<DataTable data={ex2} search=true rowShading=true totalRow=true rows=8>
    <Column id=EmployeID align=center title="N° Employe" totalAgg="Total des quantités vendues"/>
    <Column id=quantity align=center title="Quantite" fmt='# ###' totalAgg=sum contentType=colorscale colorScale='green'/>
</DataTable>

## <u>Requête n° 3</u>

_Somme des ventes journalières par trie croissant_

<!-- Requête SQL -->

```sql ex3
-- Colonnes récupérées
select
    s.DateVente
    , round(sum(s.MontantTotal), 0) as sales_total
-- BD récupérée
from data.Ventes s
-- TCD
group by s.DateVente
-- Trie décroissant
order by
    sales_total desc
    , s.DateVente asc;
```

<!-- Table -->
<DataTable data={ex3} search=true rows=15 rowShading=true totalRow=true>
    <Column id=DateVente align=center title=Date totalAgg="Total des ventes" fmt='dd/mm/yyyy'/>
    <Column id=sales_total title="Montant des ventes" align=center totalAgg=sum fmt='# ### " €"' contentType=colorscale scaleColor='orange'/>
</DataTable>

<!-- Graphique -->

<LineChart data={ex3} x=DateVente y=sales_total yFmt='# ### " €"' lineColor='orange' title='Ventes journalières' chartAreaHeight=300>
    <ReferenceLine y=20000 label='Objectif'/>
    <ReferenceArea xMin='2020-03-01' xMax='2020-04-30' label='Covid'/>
</LineChart>

## <u>Requête n° 4</u>

_Somme des ventes par année par trie croissant_

<!-- Requête SQL -->

```sql ex4
-- Colonnes récupérées
select
    cast(cast(year(s.DateVente) as int) as varchar) as sales_year
    , round(sum(s.MontantTotal), 0) as sales_total
-- BD récupérée
from data.Ventes s
-- TCD
group by sales_year
-- Trie
order by sales_total asc;
```

<!-- Table -->

<DataTable data={ex4} rowShading=true totalRow=true>
    <Column id=sales_year align=center title=Annee totalAgg="Total des ventes réalisées" fmt='###'/>
    <Column id=sales_total align=center title="CAHT realise" totalAgg=sum fmt='# ### " €"' contentType=colorscale scaleColor=yellow/>
</DataTable>

<!-- Graphique -->

<BarChart
data={ex4}
x=sales_year
y=sales_total
title="Cumul des ventes par année"
labels=true
yFmt='# ### " €"'
fillColor='yellow'
/>

## <u>Requête n° 5</u>

_Moyenne des ventes par année et par employé_

<!-- Requête SQL -->

```sql ex5
-- Colonnes réccupérées
select
    s.EmployeID
    , year(s.DateVente) as sales_year
    , round(avg(s.MontantTotal), 0) as sales_avg
-- BD récupérée
from data.Ventes s
-- TCD
group by
    s.EmployeID
    , sales_year
-- Trie
order by
    sales_year asc
    , sales_avg desc;
```

<!-- Table -->
<DataTable data={ex5} search=true rowShading=true totalRow=true rows=12>
    <Column id=EmployeID align=center title="N° employe" totalAgg=""/>
    <Column id=sales_year align=center title=Annee totalAgg="Ventes moyennes" fmt='###'/>
    <Column id=sales_avg align=center title="CAHT realise" totalAgg=mean fmt='# ### " €"' contentType=colorscale scaleColor=brown/>
</DataTable>

## <u>Requête n° 6</u>

_Donner la liste des 5 employés ayant réalisé le plus gros du CAHT_

<!-- Requête SQL -->

```sql ex6
-- Colonnes récupérées
select
    cast(cast(s.EmployeID as int) as varchar) as EmployeID
    , year(s.DateVente) as sales_year
    , round(sum(s.MontantTotal), 0) as sales_total
-- BD récupérée
from data.Ventes s
-- TCD
group by
    s.EmployeID
    , sales_year
-- Trie
order by sales_total desc
-- Affichage
limit 5;
```

<!-- Table -->

<DataTable data={ex6} rowShading=true totalRow=true>
    <Column id=EmployeID align=center title="N° employe" totalAgg=""/>
    <Column id=sales_year align=center title=Annee fmt=### totalAgg="Total des ventes réalisées"/>
    <Column id=sales_total align=center title=CAHT fmt='# ### " €"' totalAgg=sum contentType=colorscale scaleColor=blue/>
</DataTable>

<!-- Graphique -->

<BarChart
data={ex6}
x=EmployeID
y=sales_total
title="Employés top 5"
subtitle="Classement par n° ID des employés"
labels=true
yFmt='# ### " €"'
fillColor='blue'
xAxisTitle=true
/>
