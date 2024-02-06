The task is give a powershell A .CSV file that will have the following columns

| Pi Server Name          | Metric Name                           | tStore endpoint                                | Database Name | Username                                           | Password                                 | Tag filter                                                                                                         |
| ----------------------- | ------------------------------------- | ---------------------------------------------- | -------- | -------------------------------------------------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Name of the data source | Name that will be on the tStore table | Reachable location from the data source server | Name of the database where the data is in         | User for tStore login<br>(tstoredev@transpara.com) | Password for tStore login (tStoreDev!22) | Regex, or Standard templating to filter all the tags that will get selected from the source (will be hardcoded fo) |

