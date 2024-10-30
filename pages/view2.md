---
sidebar_position: 19
---

# L'opérateur VIEW (2)

---

_Travaux effectués directement à partir de ce fichier_

**Attention ! Ne pas mettre de point virgule à la fin de la requête en tant que VIEW !**

## <u>Requête n° 1</u>

Créez une vue des ventes ventes_2021 de l'année 2021.

<!-- Requête SQL en tant que VIEW -->

```sql sales2021
-- Colonnes récupérées
select
    cast(cast(s.ClientID as int) as varchar) as ClientID
    , cast(cast(s.EmployeID as int) as varchar) as EmployeID
    , year(s.DateVente) as Annee
    , s.MontantTotal
from data.Ventes s
where year(s.DateVente) = 2021
```

<DataTable data={sales2021} rowShading=true>
    <Column id=ClientID align=center/>
    <Column id=EmployeID align=center/>
    <Column id=Annee align=center fmt='# ###'/>
    <Column id=MontantTotal align=center fmt='# ### " €"'/>
</DataTable>

## <u>Requête n° 2</u>

À partir de la vue créée : sales2021, donner la liste des clients qui ont réalisé plus d'un achat en 2021.

<!-- Requête SQL -->

```sql query1
-- Colonnes récupérées
select
    cast(cast(c.ClientID as int)as varchar) as c_ClientID
    , c.Nom
    , c.Prenom
    , count(s.MontantTotal) as sales_quantity
-- BD récupérées
from data.Clients c
join ${sales2021} s
on c.ClientID = s.clientID
-- TCD
group by
    c_ClientID
    , c.Nom
    , c.Prenom
-- Filtre
having sales_quantity > 1
-- Trie
order by
    sales_quantity desc
    , c.Nom asc;
```

<!-- Table -->
<DataTable data={query1} rowShading=true totalRow=true rows=7>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=c_ClientID title="N° Client" align=center totalAgg="Quantité totale"/>
    <Column id=sales_quantity title=Quantite align=center fmt='# ###'/>
</DataTable>

## <u>Requête n° 3</u>

À partir de la vue créée : sales2021, donner la liste des employés qui ont réalisé des ventes moyennes supérieures à 500 en 2021.

<!-- Requête SQL -->

```sql query2
-- Colonnes récupérées
select
    cast(cast(e.EmployeID as int)as varchar) as e_EmployeID
    , e.Nom
    , e.Prenom
    , e.Fonction
    , round(avg(s.MontantTotal), 0) as sales_avg
-- BD récupérées
from data.Employes e
join ${sales2021} s
on e.EmployeID = s.EmployeID
-- TCD
group by
    e_EmployeID
    , e.Nom
    , e.Prenom
    , e.Fonction
-- Filtre
having sales_avg > 500
-- Trie
order by
    sales_avg desc
    , e.Nom asc;
```

<!-- Table -->

<DataTable data={query2} search=true rowShading=true rows=13 totalRow=true>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=Fonction align=center/>
    <Column id=e_EmployeID title="N° Employe" align=center totalAgg=Moyenne/>
    <Column id=sales_avg title="CAHT moyen" align=center fmt='# ### " €"' contentType=colorscale scaleColor=brown/>
</DataTable>
