# coa-build

Builds the Windows server (worldserver and authserver) from:

- [azerothcore-wotlk-coa](https://github.com/Brytenwally/azerothcore-wotlk-coa) (`main`), with the CoA modules it
  already contains;
- [mod-10-man-world](https://github.com/Brytenwally/mod-10-man-world) (`master`), its core patch applied;
- [mod-playerbots](https://github.com/Brytenwally/mod-playerbots) (`coa-bot-strategies`: CoA bots with the Molten
  Core and Scarlet Monastery strategies);
- [mod-ale](https://github.com/Brytenwally/mod-ale) (`master`).

## Running a build

1. Open **Actions**, pick **Windows build**, click **Run workflow**. The branches can be changed in that dialog.
2. The build takes about one to two hours. Click the run to follow each step.
3. When it is green, download **coa-server-windows** under **Artifacts** at the bottom of the run page.
4. Unzip it over your server folder (for example `D:\build\bin\Release`). Keep your own `.conf` files and the `Data`
   folder. `versions.txt` says which commit of each repository went into the build.

The databases and the `Data` folder (dbc, maps, vmaps, mmaps) are not part of the build.

## MySQL version

The worldserver refuses to start unless its `libmysql.dll` is the exact MySQL version it was compiled against
("Used MySQL library version ... does not match", ACE00046). The **mysql_version** field of the Run workflow
dialog (default `8.4.2`, the version of the portable server) picks that version: the build downloads it, compiles
against it and puts its `libmysql.dll` in the zip. Use the zip's `libmysql.dll`, not an older one.
