---
sidebar_position: 10
---

# L'opérateur AVG

---

## <u>CAHT moyen de toutes les ventes réalisées</u>

<!-- Requête SQL -->

```sql ex1
-- Colonnes récupérées
select round(avg(s.MontantTotal), 0) as MoyenneCA
-- BD récupére
from data.Ventes s;
```

<!-- Markdown -->

Le CAHT moyen des données exploitées est de <Value data={ex1} column=MoyenneCA fmt='# ###'/> €.

<br>

<!-- Graphique -->
<center>
    <div class=kpi-css>
        <BigValue
            data={ex1}
            value=MoyenneCA
            title="CAHT moyen"
            fmt='# ### " €"'
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
