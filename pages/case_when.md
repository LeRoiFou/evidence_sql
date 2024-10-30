---
sidebar_position: 20
---

# L'opérateur CASE WHEN

---

## <u>Requête n° 1</u>

Écrire une requête SQL permettant de classifier pour chaque produit sa catégorie :

- "Petit Budget" si le prixUnitaire est inférieur à 200 euros
- "Moyen Budget" si le prixUnitaire est compris entre 200 et 500
- "Grand Budget" si le prix unitaire est supérieur à 500

<!-- Requête SQL -->

```sql query1
-- Colonnes récupérées
select
    cast(cast(p.ProduitID as int) as varchar) as p_ProduitID
    , p.NomProduit
    , p.Description
    , p.PrixUnitaire
    , case
        when p.PrixUnitaire < 200 then 'Petit Budget'
        when p.PrixUnitaire >= 200 AND p.PrixUnitaire < 500 then 'Moyen Budget'
        else 'Grand Budget'
    end as Categorie
-- BD récupérée
from data.Produits p
-- Trie
order by
    Categorie asc
    , p.PrixUnitaire desc
    , p.ProduitID asc;
```

<!-- Table -->

<DataTable data={query1} search=true rowShading=true totalRow=true rows=15>
    <Column id=NomProduit title=Nom  align=center/>
    <Column id=Description align=center wrap=true totalAgg="Prix moyen"/>
    <Column id=PrixUnitaire title="Prix unitaire" align=center totalAgg=mean fmt='# ### " €"' contentType=colorscale scaleColor=brown/>
    <Column id=p_ProduitID title='N° Produit' align=center/>
    <Column id=Categorie align=center/>
</DataTable>

## <u>Requête n° 2</u>

Écrire une requête permettant d'afficher pour chaque employe, son nom, son prénom, ainsi que le nombre de ventes réalisée et une variable qui indique si le nombre de vente est inférieur à 1, ou compris entre 1 et 2, ou supérieur à 2

<!-- Requête SQL -->

```sql query2
-- Colonnes récupérées
select
    cast(cast(e.EmployeID as int) as varchar) as e_EmployeID
    , e.Nom
    , e.Prenom
    , count(s.VenteID) as sales_quantity
    , case
        when sales_quantity < 1 then 'A virer'
        when sales_quantity >=1 and sales_quantity <=2 then 'Bof'
        else 'Prime à donner'
    end as Classification
-- BD récupérées
from data.Employes e
left join data.Ventes s
on e.EmployeID = s.EmployeID
-- TCD
group by
    e_EmployeID
    , e.Nom
    , e.Prenom
-- Trie
order by
    sales_quantity desc
    , e.Nom asc
    , e.Prenom asc;
```

<!-- Table -->

<DataTable data={query2} search=true rowShading=true totalRow=true rows=15>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=e_EmployeID title='N° Employe' align=center totalAgg=Moyenne/>
    <Column id=sales_quantity title='Quantite vendue' align=center totalAgg=mean fmt='# ###' contentType=colorscale scaleColor=orange/>
    <Column id=Classification align=center/>
</DataTable>

## <u>Requête n° 3</u>

Créer une requête qui donne le nom du client, son prénom :

- Si le montant total des achats du client inférieur à 1 000 € : SILVER
- Entre 1 000 € et 5 000 € : GOLD
- Supérieur à 5 000 € : premium

<!-- Requête SQL -->

```sql query3
-- Colonnes récupérées
select
    cast(cast(c.ClientID as int) as varchar) as c_ClientID
    , c.Nom
    , c.Prenom
    , coalesce(round(sum(s.MontantTotal), 0), 0) as sales_sum
    , case
        when sales_sum < 500 then '-'
        when sales_sum >= 500 and sales_sum < 1000 then 'SILVER'
        when sales_sum >= 1000 and sales_sum < 5000 then 'GOLD'
        else 'PREMIUM'
    end as Classification
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
    , c.Nom asc
    , c.Prenom asc ;
```

<!-- Table -->

<DataTable data={query3} search=true rowShading=true totalRow=true rows=15>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=c_ClientID title='N° Client' align=center totalAgg='Moyenne'/>
    <Column id=sales_sum title=Achats align=center fmt='# ### " €"' totalAgg=mean contentType=colorscale scaleColor=yellow/>
    <Column id=Classification align=center/>
</DataTable>
