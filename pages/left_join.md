---
sidebar_position: 16
---

# L'opérateur LEFT JOIN

---

## <u>1ère requête</u>

Donner pour chaque employé, le nom, le prénom et le nombre de ventes réalisées et il faut conserver les employés qui n'ont réalisé aucune vente

<!-- Requête SQL -->

```sql ex1
-- Colonnes récupérées
select
    cast(cast(e.EmployeID as int) as varchar) as e_EmployeID
    , e.Nom
    , e.Prenom
    , count(s.VenteID) as quantity
-- BD récupérée
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
    quantity desc
    , e.Nom asc;
```

<!-- Table -->
<DataTable data={ex1} search=true rowShading=true totalRow=true rows=15>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=e_EmployeID title="N° Employe" align=center totalAgg="Quantité moyenne vendue"/>
    <Column id=quantity title="Quantité vendue" align=center totalAgg=mean fmt='# ###' contentType=colorscale scaleColor=brown/>
</DataTable>

## <u>2ème requête</u>

Donner pour chaque fournisseur, son nom, son email et le nombre de produits fournis et conserver les fournisseurs qui ne fournisseurs aucun produit

<!-- Requête SQL -->

```sql ex2
-- Colonnes récupérées
select
    cast(cast(s.FournisseurID as int)as varchar) as s_FournisseurID
    , s.NomFournisseur
    , s.Email
    , count(p.ProduitID) as Quantity
-- BD récupérées
from data.Fournisseurs s
left join data.Produits p
on s.FournisseurID = p.FournisseurID
-- TCD
group by
    s_FournisseurID
    , s.NomFournisseur
    , s.Email
-- Trie
order by
    quantity desc
    , s.NomFournisseur asc;
```

<DataTable data={ex2} search=true rowShading=true totalRow=true rows=15>
    <Column id=NomFournisseur align=center/>
    <Column id=s_FournisseurID title="N° Fournisseur" align=center/>
    <Column id=Email align=center totalAgg="Quantité moyenne achetée"/>
    <Column id=Quantity align=center totalAgg=mean fmt='# ###' contentType=colorscale scaleColor=orange/>
</DataTable>
