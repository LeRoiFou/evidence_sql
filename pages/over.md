---
sidebar_position: 21
---

# L'opérateur OVER

---

Avec cette opérateur :

- On peut effectuer un classement par numérotation avec RANK() et DENSE_RANK()
- On peut récupérer la valeur de la ligne précédente avec LEAD() ou récupérer les valeur de la ligne suivante avec LAG()
- On peut ajouter un n° par ligne avec ROW_NUMBER()
- Récupérer la première valeur avec FIRST_VALUE() ou la dernière valeur avec LAST_VALUE()

## <u>Requête n° 1</u>

Donner le classement des produits en fonction de la somme des quantités vendues

<!-- Requête SQL -->

```sql query1
-- Colonnes récupérées
select
    cast(cast(p.ProduitID as int)as varchar) as p_ProduitID
    , p.NomProduit
    , coalesce(count(s.QuantiteVendue), 0) as quantity_sales
    -- Classement
    , dense_rank() over (order by coalesce(count(s.QuantiteVendue), 0) desc) as Classification
-- BD récupérées
from data.Produits p
left join data.Ventes s
on p.ProduitID = s.ProduitID
-- TCD
group by
    p_ProduitID
    , p.NomProduit;
```

<!-- Table -->

<DataTable data={query1} search=true rowShading=true rows=15 totalRow=true>
    <Column id=NomProduit title=Produit align=center totalAgg=''/>
    <Column id=p_ProduitID title="N° Produit" align=center totalAgg=Moyenne/>
    <Column id=quantity_sales title='Quantités vendues' align=center fmt='# ###' totalAgg=mean contentType=colorscale scaleColor=brown />
    <Column id=Classification align=center totalAgg=''/>
</DataTable>

## <u>Requête n° 2</u>

Donner le classement des employés qui ont réalisé le plus grand chiffre d'affaires

<!-- Requête SQL -->

```sql query2
-- Colonnes récupérées
select
    cast(cast(e.EmployeID as int)as varchar) as e_EmployeID
    , e.Nom
    , e.Prenom
    , round(sum(s.MontantTotal), 0) as total_sales
    -- Classement
    , dense_rank() over (order by sum(s.MontantTotal) desc) as Classification
-- BD récupérées
from data.Employes e
join data.Ventes s
on e.EmployeID = s.EmployeID
-- TCD
group by
    e_EmployeID
    , e.Nom
    , e.Prenom
-- Affichage
limit 10;
```

<!-- Table -->

<DataTable data={query2} rowShading=true rows=10 totalRow=true>
    <Column id=Nom align=center totalAgg=''/>
    <Column id=Prenom align=center totalAgg=''/>
    <Column id=e_EmployeID title='N° Employe' align=center totalAgg=Moyenne/>
    <Column id=total_sales title=CAHT align=center fmt='# ### " €"' totalAgg=mean contentType=colorscale scaleColor=orange/>
    <Column id=Classification align=center totalAgg=''/>
</DataTable>

<!-- Graphique -->

<BarChart
    data={query2}
    x=Nom
    y=total_sales
    swapXY=true
    labels=true
    yFmt='# ### " €"'
    fillColor=orange
/>
