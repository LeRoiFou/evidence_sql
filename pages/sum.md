---
sidebar_position: 9
---

# L'opérateur SUM

---

## <u>Montant total des ventes</u>

<!-- Requête SQL -->

```sql ex1
-- Colonnes récupérées
select sum(s.MontantTotal) as Total
-- BD récupérée
from data.Ventes s;
```

<!-- Markdown -->

Le CAHT total réalisé est de <Value data={ex1} fmt='# ### " €"'/>.

<!-- Graphique -->

<center>
<div class=kpi-css>
<BigValue
    data={ex1}
    value=Total
    fmt='# ### " €"'
    title="CAHT total"
/>
</div>
</center>

<!-- Style CSS -->
<style>
    .kpi-css{
        border: 1px black solid;
        display: inline;
        padding-bottom: 50px;
        padding-left: 20px;
        background-color: #40bcb8;
    }
</style>
