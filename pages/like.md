---
sidebar_position: 6
---

# L'opérateur LIKE

---

## <u>Ensemble des clients dont le nom commence par la lettre 'C'</u>

<!-- Requête SQL -->

```sql ex1
-- Colonnes récupérées
select
    c.ClientID
    , c.Nom
    , c.Prenom
    , c.Email
    , c.NumeroTelephone
-- BD récupérée
from data.Clients c
-- Filtre
where c.Nom like 'C%'
-- Trie
order by c.Nom asc;
```

<!-- Table -->
<DataTable data={ex1} search=true rowShading=true>
    <Column
        id=Nom
        align=center
    />
    <Column
        id=Prenom
        align=center
    />
    <Column
        id=Email
        align=center
    />
    <Column
        id=NumeroTelephone
        title=Telephone
        align=center
    />
    <Column
        id=ClientID
        title="N° client"
        align=center
    />
</DataTable>

## <u>Ensemble des clients dont le nom commence par la lettre 'C' et qui finit par la lettre 'A'</u>

<!-- Requête SQL -->

```sql ex2
-- Colonnes récupérées
select
    c.ClientID
    , c.Nom
    , c.Prenom
    , c.Email
    , c.NumeroTelephone
-- BD récupérée
from data.Clients c
-- Filtre
where c.Nom like 'C%%a';
```

<!-- Table -->
<DataTable data={ex2}>
    <Column
        id=Nom
        align=center
    />
    <Column
        id=Prenom
        align=center
    />
    <Column
        id=Email
        align=center
    />
    <Column
        id=NumeroTelephone
        titlee=Telephone
        align=center
    />
    <Column
        id=ClientID
        title="N° client"
        align=center
    />
</DataTable>

## <u>Ensemble des clients dont le nom commence par la lettre 'C' et que le prénom se finit par 'Y'</u>

<!-- Requête SQL -->

```sql ex3
-- Colonnes récupérées
select
    c.ClientID
    , c.Nom
    , c.Prenom
    , c.Email
    , c.NumeroTelephone
-- BD récupérée
from data.Clients c
-- Filtre
where c.Nom like 'C%' and c.Prenom like '%y'
-- Trie
order by c.Nom asc;
```

<!-- Table -->
<DataTable data={ex3} rowShading=true>
    <Column
        id=Nom
        align=center
    />
    <Column
        id=Prenom
        align=center
    />
    <Column
        id=Email
        align=center
    />
    <Column
        id=NumeroTelephone
        title=Telephone
        align=center
    />
    <Column
        id=ClientID
        title="N° client"
        align=center
    />
</DataTable>

## <u>Donner les noms des clients qui contiennent la lettre 'N'</u>

<!-- Requête SQL -->

```sql ex4
-- Colonnes récupérées
select
    c.ClientID
    , c.Nom
    , c.Prenom
    , c.Email
    , c.NumeroTelephone
-- BD récupérée
from data.Clients c
-- Filtre
where c.Nom like '%n%' or c.Nom like 'N%'
-- Trie
order by c.Nom asc;
```

<!-- Table -->
<DataTable data={ex4} search=true rowShading=true>
    <Column
        id=Nom
        align=center
    />
    <Column
        id=Prenom
        align=center
    />
    <Column
        id=Email
        align=center
    />
    <Column
        id=NumeroTelephone
        title=Telephone
        align=center
    />
    <Column
        id=ClientID
        title="N° client"
        align=center
    />
</DataTable>

## <u>Donner les noms de clients qui commencent par la lettre R et qui ont au moins 5 caractères</u>

<!-- Requête SQL -->

```sql query5
-- Colonnes récupérées
select
    cast(cast(c.ClientID as int)as varchar) AS c_ClientID
    , c.Nom
    , c.Prenom
    , c.Email
    , c.NumeroTelephone
-- BD récupérée
from data.Clients c
-- Filtre
where c.Nom like 'R____%'
-- Trie
order by
    c.Nom
    , c.Prenom ;
```

<!-- Table -->

<DataTable data={query5} search=true rows=15>
    <Column id=Nom align=center/>
    <Column id=Prenom align=center/>
    <Column id=Email align=center/>
    <Column id=NumeroTelephone title=Telephone align=center/>
    <Column id=c_ClientID title='N° client' align=center/>
</DataTable>
