## Script: Manage_Schema_Ownership.sql

**Description**:
This script allows you to **view** and **change** the ownership of schemas in a SQL Server database. Managing schema ownership is crucial for maintaining proper security and organizing object permissions.

---

### 🔎 Part 1: List Current Schema Owners

```sql
SELECT 
    s.name AS SchemaName, 
    u.name AS SchemaOwner 
FROM sys.schemas s 
JOIN sys.sysusers u ON s.principal_id = u.uid 
ORDER BY s.name;
```

This returns a list of all schemas in the current database along with their owning users.

---

### 🔄 Part 2: Change Schema Owner

```sql
ALTER AUTHORIZATION ON SCHEMA::[SchemaName] TO [NewOwner];
```

> 🔁 Replace:
> - `[SchemaName]` with the name of the schema you want to reassign
> - `[NewOwner]` with the **user or role** you want to assign ownership to

---

### ✅ Use Case:
- Transfer schema ownership to another login/user
- Align schema owners with service accounts or application users
- Resolve deployment or permission conflicts due to ownership mismatch

---

### ⚠️ Notes:
- Make sure the **new owner exists** in the database.
- Schema owner should typically **match object owners** to prevent permission issues.
- Avoid assigning ownership to roles like `db_datareader`, `db_owner`, etc.

