# Datagroom `v0.5`

Datagroom aims to provide tools to maintain and groom arbitrary datasets with a simple and intuitive user-experience. The data grooming can be done by multiple users simultaneously. 

* [datagroom-gateway](https://github.com/h-tendy/datagroom-gateway): This constitutes the backend of datagroom. 

* [datagroom-ui](https://github.com/h-tendy/datagroom-ui): Constitutes the react front-end for it. 

## Features

1. The data is stored in `MongoDb` at the backend. 

1. The front-end features the wonderful `Tabulator` (tabulator.info) component. 

1. Shared editing of data with similar user-experience like a Google sheet. 
    * Per-cell locking.
    * Dynamic updates to edited cells. 
    * Guaranteed to not overwrite a more recent edit by someone else. 

1. Supports markdown in cells. You edit markdown and the html is rendered in the table. Use of `codemirror` as an editor for markdown is enabled. 

1. Export of all data to `xlsx` file format. 

1. Paging, Filtering, Searching (regex), Sorting of data. All from the backend, enabling the tool to work with very large datasets. 

1. Import your data from `xlsx` and `csv` formats. 

1. Adjust and set views that is visible for everyone. 

1. Easy copy of rendered HTML to clipboard. 

1. Configurable single or multiple selection of preset items on a column. 

1. Configurable conditional values for a column based on other column values. 

1. Right-click menu for useful tools. 

1. Per-column editable controls. Also allows you to hide some columns. Set a few formatting attribute on a per column basis. 

1. Edit-log for every single edit by any user. No danger of losing data. 

1. Hook it up to your company's active-directory for user authentication. Or use a single guest user account to start. 

## Filters

1. Click on `Show filters` checkbox to see additional controls for filtering. With these controls, you can save various column filters (with regex support), column visibility and column widths as well. 

    ![](img/2020-11-26-13-40-21.png)

1. Select from the stored filters to immediately reset the view to the stored value. The URL also changes and is directly routable. 

    ![](img/2020-11-26-13-41-38.png)

## Bulk editing

Bulk editing features are now available. Yet to be documented

## Installation

1. Install `MongoDb` community edition, if you want local installation. In case of cloud `MongoDb` installation. Follow the following steps:-
    * Make a new `project` and a new empty `cluster` inside that project on mongodb atlas.
    * For the newly connected `cluster`. Click on `connect -> connect your application` and copy the url. Sample url:- mongodb+srv://<username>:<password>@<clusterName>.onvfm2f.mongodb.net/?retryWrites=true&w=majority
    * Now go to `database access` option and add new user with the same username which will be used for login to datagroom. (In case of ldap server, it will be org username. For others, create a `guest` user.). Give the user `readWriteAnyDatabase` permission.
    * Now go to `network access` option and add the ip address of the server where datagroom-gateway will run. Or, otherwise allow access from anywhere.

1. git clone the `datagroom-gateway` and `datagroom-ui` repos. If all of the repos and the mongodb installation is on the same machine, go to next step. Otherwise, in `datagroom-gateway`, add one .env file and update it with key `DATABASE` and value as the the mongodb server url. Alternatively, you can tweak `this.url` in `dbAbstraction.js` directly if url doesn't consist any sensitive information.

1. Build react-ui by doing `cd datagroom-ui; npm run build`. Note that `datagroom-gateway` and `datagroom-ui` should be at the same level because `datagroom-gateway` serves the files built in `datagroom-ui`. 

1. Start server: `cd datagroom-gateway; node ./server.js disableAD=true`. Login as `guest` with `guest` as password. If you want active-directory integration, update the configuration in `ldapSettings.js`. (`node ./server.js` if you have updated `ldapSettings.js`) If you want to use the JIRA plug-in, update the configuration in `jiraSettings.js`. 

1. Open a browser and navigate to `localhost:8887` 


## Uses

1. For quick bug lists, scrum todo lists, personal lists, code notes etc. 

1. Light enough for personal use on a single computer. 

1. Any table-like data that can be shared/edited. 

## Screenshots

1. A sample table once populated:
![](img/2020-11-26-13-44-24.png)

1. Markdown editing in progress
![](./img/2020-09-19-16-16-44.png)
![](img/2020-11-26-09-43-23.png)

1. Markdown rendered once editing is done
![](./img/2020-09-19-16-17-42.png)

1. Right-click menu
![](img/2020-11-26-13-43-06.png)

1. Filters in action
![](./img/2020-09-19-16-28-22.png)

1. Edit-log
![](./img/2020-09-19-16-31-38.png)


