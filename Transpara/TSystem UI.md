
# User-related 

## Auto-install required components

When one of the required components is not detected, they will get automatically created. A popup is shown while it's in progress, with the ability to cancel. But if the user hits "cancel", they won't be able to execute any other actions. Required components:

- tStore
- tStore Interface
- tMon

# Developer-related 

## Reducer

The reducer's state will have the following elements:

| Property       | Description                                                                            | Type   |
| -------------- | -------------------------------------------------------------------------------------- | ------ |
| baseURL        | the URL where all the API requests are going to be made                                | string |
| modules        | where all the tSystem components (and tSystem itself) are going to be stored           | array  |
| selectedModule | information about the currently selected component, and how it's going to be displayed | object |
| loading        | the loading state of the application. it can be "pending", "fulfilled", and "error"    | string       |

The `modules` property is an array of object, that more specifically are structured as follows:

| Property  | Description                                                                   | Required | Type   |
| --------- | ----------------------------------------------------------------------------- | -------- | ------ |
| name      | the name of the component                                                     | yes      | string |
| children  | where the children components of that component get stored                    | no       | array  |
| data      | Raw data of the component                                                     | no       | object |
| type      | type of the component (tsystem, tstore, tmon, tcalc, tbackup, tproxy)         | no       | string |
| pathLabel | if exists, it's the name that is takin in consideration when searching for it | no       | string       |


## Component types

| Component  | Type      |
| ---------- | --------- |
| tSystem    | tsystem   |
| tStore     | tstore    |
| tCalc      | tcalc     |
| tMon       | tmon      |
| tMon agent | tmonagent |
| tBackup    | tbackup   |
| tProxy     | tproxy          |

This table is useful to know the mappings of the components to their strings representing their types

## Loading States

| State      | name        |
| ---------- | ----------- |
| In Process | `pending`   |
| Completed  | `fulfilled` |
| Error      | `error`            |

