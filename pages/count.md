---
sidebar_position: 8
---

# L'opérateur COUNT

---

## <u>Combien y-a-t'il de client dans la base de données ?</u>

<!-- Requête SQL -->

```sql ex1
-- Colonnes récupérées
select COUNT(c.ClientID) AS Quantity
-- BD récupérée
from data.Clients c;
```

<!-- Markdown -->

Il y a <Value data={ex1}/> clients dans la base de données.
<br>

<!-- Graphique -->

<center>
    <div class=kpi-css>
    <BigValue
        data={ex1}
        value=Quantity
        title="Nombre de clients"
    />
    </div>
</center>

<!-- *************** Style CSS ***************** -->
<style>
    .kpi-css {
        border: 1px black solid;
        display: inline;
        padding-bottom: 40px;
        padding-left: 20px;
        background-color: #40bcb8;
    }

</style>
