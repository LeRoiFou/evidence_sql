---
sidebar_position: 26
---

# L'opérateur UNION

---

## <u>Requête</u>

Donner une liste combinant tous les noms et prénoms des employés et des clients

<!-- Requête SQL -->

```sql query
-- Colonnes récupérées
select
    e.Nom
    , e.Prenom
-- BD récupérée
from data.Employes e
-- Concaténation
union
-- Colonnes récupérées
select
    c.Nom
    , c.Prenom
-- BD récupérée
from data.Clients c;
```

<!-- Table -->

<DataTable data={query} search=true rowShading=true rows=15>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
</DataTable>
