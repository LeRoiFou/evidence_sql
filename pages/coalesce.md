---
sidebar_position: 17
---

# L'opérateur COALESCE

---

## <u>Requête n° 1</u>

Donner le nom, le prénom et la moyenne des ventes par clients et conserver les clients pour lesquels aucune vente n'a été réalisée : remplacer les valeurs nulles par 0.

<!-- Requête SQL -->

```sql query1
-- Colonnes récupérées
select
    cast(cast(c.ClientID as int) as varchar) as c_clientID
    , c.Nom
    , c.Prenom
    , coalesce(round(avg(s.MontantTotal), 0), 0) as mean_sales
-- BD récupérées
from data.Clients c
left join data.Ventes s
on c.ClientID = s.ClientID
-- TCD
group by
    c_clientID
    , c.Nom
    , c.Prenom
-- Trie
order by
    mean_sales desc
    , c.Nom;
```

<!-- Table -->
<DataTable data={query1} search=true rowShading=true totalRow=true rows=15>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=c_clientID title="N° Client" align=center totalAgg="Moyenne"/>
    <Column id=mean_sales title="CAHT moyen par client" align=center fmt='# ### " €"' totalAgg=mean contentType=colorscale scaleColor=brown/>
</DataTable>

## <u>Requête n° 2</u>

Donner le nom, le prénom et la somme des achats réalisés par chaque client, et afficher la valeur zéro dans le cas où certains clients n'ont effectué aucun achat.

<!-- Requête SQL -->

```sql query2
-- Colonnes récupérées
select
    cast(cast(c.ClientID as int) as varchar) as c_ClientID
    , c.Nom
    , c.Prenom
    , coalesce(round(sum(s.MontantTotal), 0), 0) as sales_sum
-- BD récupérées
from data.Clients c
left join data.Ventes s
on c.ClientID = s.ClientID
-- TCD
group by
    c_ClientID
    , c.Nom
    , c.Prenom
-- Trie
order by
    sales_sum desc
    , c.Nom;
```

<!-- Table -->

<DataTable data={query2} search=true rowShading=true totalRow=true rows=15>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=c_ClientID title="N° client" align=center totalAgg=Total/>
    <Column id=sales_sum title="CAHT par client" align=center fmt='# ### " €"' contentType=colorscale scaleColor=orange/>
</DataTable>
