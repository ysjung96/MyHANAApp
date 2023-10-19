# Getting Started

Welcome to your new project.

It contains these folders and files, following our recommended project layout:

File or Folder | Purpose
---------|----------
`app/` | content for UI frontends goes here
`db/` | your domain models and data go here
`srv/` | your service models and code go here
`package.json` | project metadata and configuration
`readme.md` | this getting started guide


## Next Steps

- Open a new terminal and run `cds watch` 
- (in VS Code simply choose _**Terminal** > Run Task > cds watch_)
- Start adding content, for example, a [db/schema.cds](db/schema.cds).


## Learn More

Learn more at https://cap.cloud.sap/docs/get-started/.


## 메모
1) https://developers.sap.com/tutorials/hana-cloud-deploying.html
2) https://developers.sap.com/tutorials/appstudio-onboarding.html
3) https://developers.sap.com/tutorials/hana-cloud-cap-create-project.html
4) https://developers.sap.com/tutorials/hana-cloud-cap-create-database-cds.html
npm add @cap-js/sqlite -D
npm install
cds build --for hana
cds add hana --for hybrid
cds deploy --to hana --profile hybrid
cds watch --profile hybrid
http://localhost:4004/
5) https://developers.sap.com/tutorials/hana-cloud-cap-create-ui.html
cd app
npm start
http://localhost:5000/
6) https://developers.sap.com/tutorials/hana-cloud-cap-add-authentication.html
   https://developers.sap.com/tutorials/hana-cloud-cap-deploy-mta.html
cds compile srv/ --to xsuaa > xs-security.json
cf create-service xsuaa application MyHANAApp-auth -c xs-security.json
cf create-service-key MyHANAApp-auth default  
cds bind -2 MyHANAApp-auth:default
cds bind --exec -- npm start --prefix app
1) https://developers.sap.com/tutorials/hana-cloud-cap-calc-view.html
2) https://developers.sap.com/tutorials/hana-cloud-cap-stored-proc.html
	  
{"cds":{
  "requires": {
    "db": {
      "[development]": { "kind": "sqlite", "impl": "@cap-js/sqlite", "credentials": { "url": "memory" } },
      "[production]": { "kind": "hana", "impl": "@sap/cds-hana", "deploy-format": "hdbtable" }
    }
  }
}}

## 배포
~~~
C:\MyHANAApp>cds deploy
Starting deploy to SAP HANA ...
Running build
[cds] - building project [C:\MyHANAApp], clean [true]
[cds] - cds-dk [7.3.0], cds [7.3.0], compiler [4.3.0], home [C:\MyHANAApp\node_modules\@sap\cds]

[cds] - the following build tasks will be executed
[cds] -    {
     "build": {
       "target": "gen",
       "tasks": [
         {"for":"hana", "src":"db", "dest":"../db", "options":{"model":["db","srv"]}}
       ]
     }
   }

[cds] - done > wrote output to:
   db\src\gen\.hdiconfig
   db\src\gen\.hdinamespace
   db\src\gen\CatalogService.Countries.hdbview
   db\src\gen\CatalogService.Countries_texts.hdbview
   db\src\gen\CatalogService.Interactions_Header.hdbview
   db\src\gen\CatalogService.Interactions_Items.hdbview
   db\src\gen\app.interactions.Interactions_Header.hdbtable
   db\src\gen\app.interactions.Interactions_Items.hdbtable
   db\src\gen\localized.CatalogService.Countries.hdbview
   db\src\gen\localized.CatalogService.Interactions_Header.hdbview
   db\src\gen\localized.CatalogService.Interactions_Items.hdbview
   db\src\gen\localized.app.interactions.Interactions_Header.hdbview
   db\src\gen\localized.app.interactions.Interactions_Items.hdbview
   db\src\gen\localized.sap.common.Countries.hdbview
   db\src\gen\sap.common.Countries.hdbtable
   db\src\gen\sap.common.Countries_texts.hdbtable

[cds] - build completed in 741 ms


Using container MyHANAApp-db
Getting service MyHANAApp-db
Getting service key MyHANAApp-db-key
Deploying to HANA from C:\MyHANAApp\db
Using HDI deployer from C:\Users\nihil\AppData\Roaming\npm\node_modules\@sap\cds-dk\node_modules\@sap\hdi-deploy\library.js
VCAP_SERVICES: {
  "hana": [
    {
      "name": "MyHANAApp-db",
      "tags": [
        "hana"
      ],
      "credentials": {
        "database_id": "ac954077-1d7c-4106-9540-160d5c6a9a0a",
        "host": "ac954077-1d7c-4106-9540-160d5c6a9a0a.hana.trial-us10.hanacloud.ondemand.com",
        "port": "443",
        "driver": "com.sap.db.jdbc.Driver",
        "url": "jdbc:sap://ac954077-1d7c-4106-9540-160d5c6a9a0a.hana.trial-us10.hanacloud.ondemand.com:443?encrypt=true&validateCertificate=true&currentschema=A24861FF20264F58A8E9DBE2420D39D2",
        "schema": "A24861FF20264F58A8E9DBE2420D39D2",
        "hdi_user": "A24861FF20264F58A8E9DBE2420D39D2_7YKQMPVW6VBXSFE29WYDBJI4O_DT",
        "hdi_p[...]
        "user": "A24861FF20264F58A8E9DBE2420D39D2_7YKQMPVW6VBXSFE29WYDBJI4O_RT",
        "p[...]
        "certificate": "-----BEGIN 
        xxxxxxxxxxxxxxxxxxxxxxxxxx
        -----END CERTIFICATE-----"
      }
    }
  ]
}
@sap/hdi-deploy, version 4.8.0 (mode default), server version 4.00.000.00.1696926395 (4.0.0.0), cloud version 2023.28.9, node version 18.18.0, HDI version 
1012, container API version 1006
Deployment started at 2023-10-19 18:59:51
Using @sap/hana-client@2.17.22 for connection
No ignore file at C:\MyHANAApp\db\.hdiignore.
Collecting files...
Collecting files... ok (0s 10ms)
2 directories collected
17 files collected
0 reusable modules collected
Target service: MyHANAApp-db
Session variable APPLICATION is set to "SAP_HDI//".
Previous build with request ID 123 finished at 2023-10-19 04:45:18.762169000 with status Committed and message: Make succeeded (2 warnings): 1 files deployed (effective 1), 0 files undeployed (effective 0), 0 dependent files redeployed.
Processing revoke files...
Processing revoke files... ok (0s 2ms)
Processing grants files...
Processing grants files... ok (0s 1ms)
Preprocessing files...
Preprocessing files... ok (0s 5ms)
Connecting to the container "A24861FF20264F58A8E9DBE2420D39D2"...
Connecting to the container "A24861FF20264F58A8E9DBE2420D39D2"... ok (3s 561ms)
Locking the container "A24861FF20264F58A8E9DBE2420D39D2"...
Locking the container "A24861FF20264F58A8E9DBE2420D39D2"... ok (3s 803ms)
Synchronizing files with the container "A24861FF20264F58A8E9DBE2420D39D2"...
  Deleting files...
  Deleting files... ok
  Writing files...
  Writing files... ok
Synchronizing files with the container "A24861FF20264F58A8E9DBE2420D39D2"... ok (10s 782ms)
added files: []
modified files: [
  "src/.hdiconfig"
]
deleted files: []
1 modified or added files are scheduled for deploy based on delta detection
0 deleted files are scheduled for undeploy based on delta detection (filtered by undeploy allowlist)
0 files are scheduled for deploy based on explicit specification
0 files are scheduled for undeploy based on explicit specification
Deploying to the container "A24861FF20264F58A8E9DBE2420D39D2"...
Polling messages for request id: 128
 Starting make in the container "A24861FF20264F58A8E9DBE2420D39D2" with 1 files to deploy, 0 files to undeploy... 
  Disabling table replication for the container schema "A24861FF20264F58A8E9DBE2420D39D2"... 
  Disabling table replication for the container schema "A24861FF20264F58A8E9DBE2420D39D2"... ok (0s 15ms)
  Migrating libraries...
  Migrating libraries... ok (2s 222ms)
  Making... 
   Preparing...
   Preparing the make transaction...
   Preparing the make transaction... ok (0s 635ms)
   Deploying the configuration file "src/.hdiconfig"...
   Warning: Could not find a configured library that contains the "com.sap.hana.di.afllangprocedure" build plugin [8211539]
     at "src/.hdiconfig" (0:0)
   Warning: Could not find a configured library that contains the "com.sap.hana.di.virtualfunctionpackage.hadoop" build plugin [8211539]
     at "src/.hdiconfig" (0:0)
   Deploying the configuration file "src/.hdiconfig"... ok (0s 68ms)
   Preparing... ok (0s 796ms)
   Calculating dependencies...
    Expanding...
    Expanding... ok (0s 42ms)
    Precompiling... 
    Precompiling... ok (0s 0ms)
    Merging...
    Merging... ok (0s 0ms)
   Calculating dependencies... ok (0s 71ms)
   Finalizing...
   Finalizing... ok (0s 27ms)
   Make succeeded (2 warnings): 1 files deployed (effective 1), 0 files undeployed (effective 0), 0 dependent files redeployed
  Making... ok (1s 89ms)
  Enabling table replication for the container schema "A24861FF20264F58A8E9DBE2420D39D2"...
  Enabling table replication for the container schema "A24861FF20264F58A8E9DBE2420D39D2"... ok (0s 94ms)
 Starting make in the container "A24861FF20264F58A8E9DBE2420D39D2" with 1 files to deploy, 0 files to undeploy... ok (3s 442ms)
Deploying to the container "A24861FF20264F58A8E9DBE2420D39D2"... ok (5s 913ms)
No default-access-role handling needed; global role "A24861FF20264F58A8E9DBE2420D39D2::access_role" will not be adapted
Unlocking the container "A24861FF20264F58A8E9DBE2420D39D2"...
Unlocking the container "A24861FF20264F58A8E9DBE2420D39D2"... ok (0s 2ms)
Deployment to container A24861FF20264F58A8E9DBE2420D39D2 done [Deployment ID: none].
Deployment ended at 2023-10-19 19:00:25
(48s 575ms)

Retrieving data from Cloud Foundry...
Binding db to Cloud Foundry managed service MyHANAApp-db:MyHANAApp-db-key with kind hana
Saving bindings to .cdsrc-private.json in profile hybrid
TIP: Run with cloud bindings: cds watch --profile hybrid
If not already done, use cds add hana to configure the project for SAP HANA.

Done.
~~~
~~~
C:\MyHANAApp>cds watch --profile hybrid
 
cds serve all --with-mocks --in-memory? --profile hybrid 
live reload enabled for browsers 
resolving cloud service bindings...
bound db to Cloud Foundry managed service MyHANAApp-db:MyHANAApp-db-key

        ___________________________

[cds] - loaded model from 3 file(s):

  srv\interaction_srv.cds
  db\interactions.cds
  node_modules\@sap\cds\common.cds

[cds] - connect using bindings from: { registry: '~/.cds-services.json' }
[cds] - connect to db > hana {
  database_id: 'ac954077-1d7c-4106-9540-160d5c6a9a0a',
  host: 'ac954077-1d7c-4106-9540-160d5c6a9a0a.hana.trial-us10.hanacloud.ondemand.com',
  port: '443',
  driver: 'com.sap.db.jdbc.Driver',
  url: 'jdbc:sap://ac954077-1d7c-4106-9540-160d5c6a9a0a.hana.trial-us10.hanacloud.ondemand.com:443?encrypt=true&validateCertificate=true&currentschema=A24861FF20264F58A8E9DBE2420D39D2',
  schema: 'A24861FF20264F58A8E9DBE2420D39D2',
  hdi_user: 'A24861FF20264F58A8E9DBE2420D39D2_7YKQMPVW6VBXSFE29WYDBJI4O_DT',
  hdi_password: '...',
  user: 'A24861FF20264F58A8E9DBE2420D39D2_7YKQMPVW6VBXSFE29WYDBJI4O_RT',
  password: '...',
  certificate: '...'
}
[cds] - using authentication: { kind: 'mocked' }

[cds] - serving CatalogService { path: '/odata/v4/catalog' }

[cds] - server listening on { url: 'http://localhost:4004' }
[cds] - launched at 2023. 10. 19. 오후 7:04:57, version: 7.3.0, in: 1.784s
[cds] - [ terminate with ^C ]
~~~

~~~
C:\MyHANAApp\app>npm start

> start
> node node_modules/@sap/approuter/approuter.js

#2.0#2023 10 19 19:31:14:041#+09:00#WARNING#/LoggingLibrary################PLAIN##Dynamic log level switching not available#
#2.0#2023 10 19 19:31:21:125#+09:00#INFO#/approuter#####lnx1kyli##########lnx1kyli#PLAIN##Application router version 14.3.3#
#2.0#2023 10 19 19:31:21:133#+09:00#INFO#/Configuration#####lnx1kylq##########lnx1kylq#PLAIN##No COOKIES environment variable#
#2.0#2023 10 19 19:31:21:143#+09:00#WARNING#/Configuration#####lnx1kylz##########lnx1kylz#PLAIN##No authentication will be used when accessing backends. Scopes defined in routes will be ignored.#
#2.0#2023 10 19 19:31:21:144#+09:00#INFO#/Configuration#####lnx1kylz##########lnx1kylz#PLAIN##Replacing $XSAPPNAME will not take place - 'xsappname' property not found in UAA configuration.#
#2.0#2023 10 19 19:31:21:468#+09:00#INFO#/approuter#####lnx1kyli##########lnx1kyli#PLAIN##Application router is listening on port: 5000#
~~~

~~~

C:\MyHANAApp>cds bind --exec -- npm start --prefix app
resolving cloud service bindings...
bound db to Cloud Foundry managed service MyHANAApp-db:MyHANAApp-db-key
bound auth to Cloud Foundry managed service MyHANAApp-auth:default

> start
> node node_modules/@sap/approuter/approuter.js

#2.0#2023 10 19 19:54:41:322#+09:00#WARNING#/LoggingLibrary################PLAIN##Dynamic log level switching not available#
#2.0#2023 10 19 19:54:42:374#+09:00#INFO#/approuter#####lnx2ezt2##########lnx2ezt2#PLAIN##Application router version 14.3.3#
#2.0#2023 10 19 19:54:42:381#+09:00#INFO#/Configuration#####lnx2ezt9##########lnx2ezt9#PLAIN##No COOKIES environment variable#
#2.0#2023 10 19 19:54:42:459#+09:00#INFO#/approuter#####lnx2ezt2##########lnx2ezt2#PLAIN##Application router is listening on port: 5000#
~~~