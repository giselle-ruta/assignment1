
ID:25143
-------
Name:Tuyinganyiki giselle

# README: Oracle Pluggable Database (PDB) Creation and Management

## Introduction

A *Pluggable Database (PDB)* is a self-contained, fully functional Oracle database that resides within a *Container Database (CDB)*. PDBs allow easy provisioning, management, and consolidation of multiple databases. In this guide, we'll create a PDB, perform alterations, and manage users. This README will walk you through the key SQL operations and their outputs.

---

## Enter into SQLPlus

Before starting, enter into SQLPlus as the *SYSDBA* user with the following command:

bash
sys as sysdba


This logs you into Oracle as a DBA, allowing you to manage the databases.

---

## Check Existing PDBs

To check the list of Pluggable Databases (PDBs) within the Container Database (CDB), use:

sql
show pdbs;

*Output:*

 CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 XEPDB1                         READ WRITE NO
         4 PLCOURSE                       MOUNTED
         5 IR_PLSQLAUCA                   MOUNTED


---

## Create a New Pluggable Database (PDB)

We will now create a new PDB called plsql_class2024db. The FILE_NAME_CONVERT clause is used to specify the location of the data files for the new PDB.

sql
CREATE PLUGGABLE DATABASE ir_plsqlauca
ADMIN USER tuyinganyiki IDENTIFIED BY tuyinganyiki
FILE_NAME_CONVERT = ('C:\app\oradata\XE\pdbseed', 'C:\plsql\pdbs\ir_plsqlauca');


## Open the New PDB

To use the PDB, you need to open it. The following command will open the plsql_class2024db PDB:

sql
ALTER PLUGGABLE DATABASE tu_plsqlauca OPEN;


## Create and Delete a PDB

### 1. Create a PDB to be Deleted

Let's create another PDB named ir_to_delete_pdb, which we will later delete:

sql
CREATE PLUGGABLE DATABASE ir_to_delete_pdb
ADMIN USER tuyinganyiki IDENTIFIED BY tuyinganyiki
FILE_NAME_CONVERT = ('C:\'app\oradata\XE\pdbseed, 'C:\plsql\pdbs\ir_to_delete_pdb');


### 2. Delete the PDB

Before dropping a PDB, it must be closed. First, we close the tu_to_delete_pdb PDB:

sql
ALTER PLUGGABLE DATABASE tu_to_delete_pdb CLOSE IMMEDIATE;


Finally, drop the tu_to_delete_pdb along with its associated data files:

sql
DROP PLUGGABLE DATABASE tu_to_delete_pdb INCLUDING DATAFILES;



---

## Conclusion

This guide demonstrates how to create, open, manage, and delete pluggable databases in Oracle SQLPlus. You now have a functional PDB named plsql_class2024db and a new user ir_plsqlauca ready for operations.
