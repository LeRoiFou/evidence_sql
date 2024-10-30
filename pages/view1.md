---
sidebar_position: 18
---

# L'opérateur VIEW (1)

---

_Travaux effectués à partir du fichier .ipynb_

## <u>Requête n° 1</u>

À partir de la vue créée : Sales_2021, donner la liste des clients qui ont réalisé plus d'un achat en 2021.

<!-- Requête SQL -->

```sql query1
-- Colonnes récupérées
select
    cast(cast(c.ClientID as int) as varchar) as c_ClientID
    , c.Nom
    , c.Prenom
    , coalesce(count(s.MontantTotal), 0) as quantity_sales
-- BD récupérées
from data.Clients c
join data.Sales_2021 s
on c.ClientID = s.ClientID
-- TCD
group by
    c_ClientID
    , c.Nom
    , c.Prenom
-- Filtre
having quantity_sales > 1
-- Trie
order by
    quantity_sales desc
    , c.Nom;
```

<!-- Table -->
<DataTable data={query1} rowShading=true totalRow=true rows=7>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=c_ClientID title="N° Client" align=center totalAgg="Quantité totale"/>
    <Column id=quantity_sales title=Quantite align=center fmt='# ###'/>
</DataTable>

## <u>Requête n° 2</u>

À partir de la vue créée : Sales_2021, donner la liste des employés qui ont réalisé des ventes moyennes supérieures à 500 en 2021.

<!-- Requête SQL -->

```sql query2
-- Colonnes récupérées
select
    cast(cast(e.EmployeID as int) as varchar) as e_EmployeID
    , e.Nom
    , e.Prenom
    , e.Fonction
    , round(avg(s.MontantTotal), 0) as avg_sales
-- BD récupérées
from data.Employes e
join data.Sales_2021 s
on e.EmployeID = s.EmployeID
-- TCD
group by
    e_EmployeID
    , e.Nom
    , e.Prenom
    , e.Fonction
-- Filtre
having avg_sales > 500
-- Trie
order by
    avg_sales desc
    , e.Nom asc;
```

<!-- Table -->

<DataTable data={query2} search=true rowShading=true rows=13 totalRow=true>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=Fonction align=center/>
    <Column id=e_EmployeID title="N° Employe" align=center totalAgg=Moyenne/>
    <Column id=avg_sales title="CAHT moyen" align=center fmt='# ### " €"' contentType=colorscale scaleColor=brown/>
</DataTable>
