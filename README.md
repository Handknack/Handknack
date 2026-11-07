# Handknack

Handknack is an Excel add-in that lets you work with your database data directly in a worksheet. Load a table into Excel, edit it like any other spreadsheet, and save your changes back to the database. It works with SQL Server, Azure SQL and Microsoft Fabric Warehouse.

<!-- Purpose / who it is for: add here. -->

## Installing
Download: [Handknack 1.0.0-beta.zip](https://github.com/Handknack/handknack.github.io/releases/download/1.0.0-beta/Handknack.1.0.0-beta.zip)

1. **Unblock.** Before extracting the files. Go to **Properties** -> Check **Unblock** -> **Apply** to prevent Windows from blocking the installation.
2. **Extract.** Extract the files to a suitable location.
3. **Close Excel.** Close any open instance of Excel.
4. **Install.** Double-click the *setup.exe* to initialize the installer,  go through the steps.
5. **Done.** Open Excel and go to the *Handknack* tab to start using the addin.
<ol start="X">**Alternatively.** If the tab does not appear:
6. **Excel.** Go to **File** -> **Options** -> **Add-ins**
7. **Manage.** In the **Manage** dropdown. Select *COM Add-ins* and press **Go...**
8. **Handknack.** Check *Handknack* in the list and press **OK**
9. **Reopen Excel.** Close all open instances of Excel and then open Excel again to access the tab

## Getting started

1. **Connect.** On the Handknack tab, choose the button for a new connection. Enter the server, pick a database and sign in. Windows, SQL and Microsoft Entra ID sign-in are supported.
2. **Pick what to load.** The wizard lists everything you can open in that database. Use the filters to narrow the list by schema or type, and click a column header to sort (click once for ascending, twice for descending, a third time for the original order).
3. **Choose where it goes.** Select the cell where the table should start. The data appears as an Excel table.
4. **Edit.** Change cells, add rows at the bottom, or delete rows.
5. **Save.** Send your changes to the database. New rows are added, changed rows are updated and deleted rows are removed.
6. **Refresh** whenever you want the latest data from the database.

Each worksheet has its own connection and its own table, so one workbook can show data from several databases. When you open the workbook again, the sheets reconnect and refresh themselves. Passwords are never saved in the workbook, so with a SQL login you are asked for the password once per session.

## The ribbon

| Control | What it does |
|---|---|
| Object dropdown | Switch the sheet to another table or object from the same connection. |
| Refresh objects | Reloads the list of objects from the database, for example after something new was added. |
| Move table | Moves the table to another place on the sheet. |
| Manage connection | Change the server, database or sign-in for the current sheet. |
| Install / Uninstall | Adds or removes the optional meta tables in the database (see below). |
| Language menu | Chooses the language for column and object names. |
| License | Enter or remove a license key. |

## Working with your data

- **Hidden key column.** The table's primary key is kept in a hidden column. Leave it as it is; it is how Handknack knows which row is which.
- **Dropdowns.** Columns that point to another table show a dropdown with the available values, so you pick a value instead of typing an ID.
- **New rows.** Type in the empty row at the bottom of the table.
- **Headers.** The column headers can show friendly or translated names instead of the database's column names (see below).

## Meta tables (optional)

Handknack works out of the box. If you want to tailor how objects appear, use the **Install** button to create a small set of settings tables in the database, in a schema called `meta`. **Uninstall** removes them again; you are shown what will be deleted and asked to confirm first.

| Table | What you use it for |
|---|---|
| `meta.affix` | Tell Handknack how your tables and procedures are named so it can find the procedures that belong to a table. The defaults are table prefix `t`, and procedure suffixes `_insert`, `_update`, `_delete`. |
| `meta.reference` | Decide what column is shown and used as a validation list from a referenced table. The default is the second column. |
| `meta.alias` | Give tables and columns friendlier names, optionally per language. |

If the tables are not installed, everything still works with the standard conventions, the original names and no extra references.

### Friendly names and languages

In `meta.alias`, each row has an object, optionally a column, the new name (`Alias`) and optionally a language (`Language`, for example `en`, `en-US`, `sv` or `sv-SE`).

- Fill in a **column** to rename that column. Leave the column empty to rename the **table or object itself**. The new name then appears in the object list and the ribbon dropdown.
- Leave the **language** empty for a default name that is used unless there is another entry for your chosen language.
- A column that references another table is by default named after the column it shows, unless you give it a different alias.

By default Handknack follows Excel's display language. Choose a language in the language menu to override it, or choose Automatic to go back. Only languages that actually have names in the database are listed. Changes made in the meta tables are picked up when you refresh the object list.

## License

Handknack includes a 30-day trial. When the trial ends, feel free to contact sales@handknack.com about your future requirements.
