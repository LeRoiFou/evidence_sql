---
sidebar_position: 15
---

# L'opérateur INNER JOIN

---

## <u>Donner pour chaque vente, le nom et le prénom de l'employé qui réalisé la vente</u>

<!-- Requête SQL -->

```sql ex1
-- Colonnes récupérées
select
    cast(cast(s.VenteID as int) as varchar) as VenteID
    , s.DateVente
    , cast(cast(s.ClientID as int) as varchar) as c_ClientID
    , s.QuantiteVendue
    , s.MontantTotal
    , e.Nom
    , e.Prenom
-- BD récupérées
from data.Ventes s
inner join data.Employes e
on s.EmployeID = e.EmployeID;
```

<!-- Table -->
<DataTable data={ex1} search=true rowShading=true totalRow=true rows=15>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=c_ClientID title="N° Client" align=center/>
    <Column id=DateVente title=Date align=center fmt="dd/mm/yyyy" totalAgg="Totaux"/>
    <Column id=QuantiteVendue title="Quantité vendue"align=center fmt="# ###" totalAgg=sum/>
    <Column id=MontantTotal title=CAHT align=center fmt='# ### " €"' totalAgg=sum contentType=colorscale scaleColor=brown/>
</DataTable>

## <u>Donner pour chaque produit de la base de données le nom, l'adresse et le n° de téléphone de son fournisseur</u>

```sql ex2
-- Colonnes récupérées
select
    cast(cast(p.ProduitID as int) as varchar) as ProduitID
    , p.NomProduit
    , p.PrixUnitaire
    , p.FournisseurID
    , s.NomFournisseur
    , s.Adresse
    , s.NumeroTelephone
-- BD récupérée
from data.Produits p
inner join data.Fournisseurs s
on p.FournisseurID = s.FournisseurID;
```

<!-- Table -->
<DataTable data={ex2} search=true rowShading=true rows=15>
    <Column id=NomProduit align=center/>
    <Column id=ProduitID title="Produit N°" align=center/>
    <Column id=PrixUnitaire title="Prix unitaire" align=center fmt='# ### " €"'/>
    <Column id=NomFournisseur title=Nom align=center/>
    <Column id=FournisseurID title="Fournisseur N°" align=center/>
    <Column id=NumeroTelephone title=Telephone align=center/>
    <Column id=Adresse align=center/>
</DataTable>

## <u>Donner le nom et prénom des employés ayant réalisé la somme des ventes les plus élevées</u>

```sql ex3
-- Colonnes récupérées
select
    cast(cast(e.EmployeID as int) as varchar) as e_EmployeID
    , e.Nom
    , e.Prenom
    , round(sum(s.MontantTotal), 0) as sales_total
-- BD récupérée
from data.Employes e
inner join data.Ventes s
on e.EmployeID = s.EmployeID
-- TCD
group by
    e_EmployeID
    , e.Nom
    , e.Prenom
-- Trie
order by
    sales_total desc
    , e.Nom asc
-- Affichage
limit 10;
```

<!-- Table -->

<DataTable data={ex3} rowShading=true totalRow=true>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=e_EmployeID title="N° Employe" align=center totalAgg="Total des ventes"/>
    <Column id=sales_total title=CAHT align=center fmt='# ### " €"' contentType=colorscale scaleColor=orange/>
</DataTable>

## <u>Donner pour chaque client, le nom, le prénom, l'adresse ainsi que le nombre d'achats réalisé</u>

```sql ex4
-- Colonnes récupérées
select
    cast(cast(c.ClientID as int) as varchar) as c_ClientID
    , c.Nom
    , c.Prenom
    , c.Adresse
    , round(count(s.VenteID), 0) as quantity
-- BD récupérée
from data.Clients c
inner join data.Ventes s
on c.ClientID = s.ClientID
-- TCD
group by
    c_clientID
    , c.Nom
    , c.Prenom
    , c.Adresse
-- Trie
order by
    quantity desc
    , c.Nom asc;
```

<DataTable data={ex4} search=true rowShading=true totalRow=true rows=15>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=c_ClientID title="N° Client" align=center/>
    <Column id=Adresse align=center totalAGg="Total quantités vendues"/>
    <Column id=quantity align=center contentType=colorscale scaleColor=yellow/>
</DataTable>

## <u>Requête par table interposée</u>

Donner la liste des noms des produits et les noms des clients pour tous les produits qui ont été achetés + d'une fois.

```sql query5
select
    p.NomProduit
    , c.Nom
    , count(s.VenteID) as sales_quantity
from data.Produits p
inner join data.Ventes s
on p.ProduitID = s.ProduitID
inner join data.Clients c
on c.ClientID = s.ClientID
group by
    p.NomProduit
    , c.Nom
having sales_quantity > 1
order by
    sales_quantity desc
    , c.Nom asc;
```

<DataTable data={query5} rows=11>
    <Column id=NomProduit title='Nom du produit' align=center/>
    <Column id=Nom title='Nom du client' align=center/>
    <Column id=sales_quantity title='Quantité achetée' align=center/>
</DataTable>
