---
sidebar_position: 14
---

# L'opérateur HAVING

---

## <u>Liste des employés réalisant chaque année un CAHT moyen > à 1K € </u>

<!-- Requête SQL -->

```sql ex1
-- Colonnes récupérées
select
    cast(cast(s.EmployeID as int) as varchar) as EmployeID
    , round(avg(s.MontantTotal), 0) as avg_sales
-- BD récupérée
from data.Ventes s
-- TCD
group by EmployeID
-- Filtre
having avg_sales > 1000
-- Trie
order by
    avg_sales desc
    , EmployeID;
```

<!-- Table -->

<DataTable data={ex1} search=true rowShading=true totalRow=true rows=15>
    <Column id=EmployeID align=center title="N° Employe" totalAgg="CAHT moyen"/>
    <Column id=avg_sales align=center title="CAHT moyen réalisé" totalAgg=mean fmt='# ### " €"' contentType=colorscale scaleColor=brown/>
</DataTable>
