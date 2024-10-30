---
sidebar_position: 11
---

# Les opérateurs MIN et MAX

---

## <u>CAHT journalier le plus bas</u>

<!-- Requête SQL -->

```sql ex1
-- Colonnes récupérées
select min(s.MontantTotal) as sales_min
-- BD récupérée
from data.Ventes s;
```

<!-- Markdown -->

Le montant le plus bas réalisé est de <Value data={ex1} column=sales_min fmt='# ###'/> €.
<br>

<!-- Graphique -->

<center>
    <div class=kpi-css>
        <BigValue
            data={ex1}
            value=sales_min
            fmt='# ### " €"'
            title="Montant le plus bas"
        />
    </div>
</center>

<br>

## <u>CAHT journalier le plus important</u>

<!-- Requête SQL -->

```sql ex2
-- Colonnes récupérées
select max(s.MontantTotal) as sales_max
-- BD récupérée
from data.Ventes s;
```

<!-- Markdown -->

Meilleur vente des données récupérées : <Value data={ex2} column=sales_max fmt='# ###'/> €.
<br>

<!-- Graphique -->

<center>
<div class=kpi-css>
    <BigValue
        data={ex2}
        value=sales_max
        fmt='# ### " €"'
        title="Montant de la meilleur vente"
    />   
</div>
</center>

<br>

## <u>Le produit le plus cher et le produit le moins cher de la table produits</u>

<!-- Requête SQL -->

```sql ex3
-- Colonnes récupérées
select
    max(p.PrixUnitaire) as up_amount
    , min(p.PrixUnitaire) as bottom_amount
-- BD récupérée
from data.Produits p;
```

<!-- Markdown -->

Le produit le plus cher est de <Value data={ex3} column=up_amount fmt='# ###'/> € et le produit le moins cher est de <Value data={ex3} column=bottom_amount fmt='# ###'/> €.

<br>

<!-- Graphiques -->

<center>
<div class=kpi-css>
    <BigValue
        data={ex3}
        value=up_amount
        fmt='# ### " €"'
        title="Montant du produit le plus cher"
    />
</div>

<div class=kpi-css>
    <BigValue
        data={ex3}
        value=bottom_amount
        fmt='# ### " €"'
        title="Montant du produit le moins cher"
    />
</div>
</center>

<!-- *********** Style CSS *********** -->
<style>
    .kpi-css{
        border: 1px black solid;
        display: inline;
        padding-bottom: 50px;
        padding-left: 20px;
        background-color: cyan;
    }
</style>
