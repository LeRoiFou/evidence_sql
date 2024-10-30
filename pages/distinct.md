---
sidebar_position: 12
---

# L'opérateur DISTINCT

---

## <u>Montant total du CAHT en prenant les valeurs uniques</u>

<!-- Requête SQL -->

```sql ex1
-- Colonnes récupérées
select sum(distinct(s.MontantTotal)) as total_sales
-- BD récupérée
from data.Ventes s;
```

<!-- Markdown -->

Montant total des ventes par valeurs uniques : <Value data={ex1} column=total_sales fmt='# ###'/> €.

<!-- Graphique -->

<center>
<div class=kpi-css>
<BigValue
    data={ex1}
    value=total_sales
    fmt='# ### " €"'
    title="Total des ventes"
/>
</div>
</center>

<br>

## <u>Montant moyen du CAHT en prenant les valeurs uniques</u>

<!-- Requête SQL -->

```sql ex2
-- Colonnes récupérées
select avg(distinct(s.MontantTotal)) as avg_sales
-- BD récupérée
from data.Ventes s;
```

<!-- Markdown -->

Montant moyen du CAHT : <Value data={ex2} column=avg_sales fmt='# ###'/> €.

<!-- Graphique -->

<center>
<div class=kpi-css>
<BigValue
    data={ex2}
    value=avg_sales
    fmt='# ### " €"'
    title="CAHT moyen"
/>
</div>
</center>

<br>

## <u>Montant max du CAHT en prenant les valeurs uniques</u>

<!-- Requête SQL -->

```sql ex3
-- Colonnes récupérées
select max(distinct(s.MontantTotal)) as sales_max
-- BD récupérée
from data.Ventes s;
```

<!-- Markdown -->

Montant maximum du CAHT : <Value data={ex3} column=sales_max fmt='# ###'/> €.

<!-- Graphique -->

<center>
<div class=kpi-css>
<BigValue
    data={ex3}
    value=sales_max
    fmt='# ### " €"'
    title="CAHT maximum"
/>
</div>
</center>

<br>

## <u>Montant min CAHT en prenant les valeurs uniques</u>

<!-- Requête SQL -->

```sql ex4
-- Colonnes récupérées
select min(distinct(s.MontantTotal)) min_sales
-- BD récupérée
from data.Ventes s;
```

<!-- Markdown -->

Montant minimum du CAHT : <Value data={ex4} column=min_sales fmt='# ###'/> €.

<!-- Graphique -->

<center>
<div class=kpi-css>
<BigValue
    data={ex4}
    value=min_sales
    fmt='# ### " €"'
    title="CAHT minimum"
/>
</div>
</center>

<!-- ************* Style CSS ************* -->
<style>
    .kpi-css{
        border: 1px black solid;
        display: inline;
        padding-bottom: 45px;
        padding-left: 20px;
        background-color: cyan;
    }
</style>
