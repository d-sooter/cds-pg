![npm version](https://img.shields.io/npm/v/cds-pg)
![Package Build](https://github.com/sapmentors/cds-pg/workflows/Node.js%20Package/badge.svg)

# cds-pg - PostgreSQL adapter for SAP CDS (CAP)

This node module provides an adapter to the PostgreSQL database.

For a short introduction on the background of this project you can check out [a short video](https://www.youtube.com/watch?v=b9sPczwYN5Q&t=2310s) that has been captured as part of the SAP devtoberfest.

## Current status

This is an alpha version and **not yet ready for production usage**! _cds-pg_ is able to connect to a PostgreSQL database and execute basic CRUD statements, but there is definitly some more work to do to bring the library to a mature state.

Please see [`CONTRIBUTING.md`](./docs/CONTRIBUTING.md) for how to contribute additional capabilities!

### TODO

- [x] implement basic `SELECT|READ`(~ OData `GET`)
- [x] implement basic `INSERT|CREATE`(~ OData `POST`)
- [x] implement basic `UPDATE`(~ OData `PUT|PATCH`)
- [x] implement basic `DELETE`(~ OData `DELETE`)
- [x] map OData to PostgreSQL vocabulary
- [x] implement basic cds deployment
- [x] use default query builders for UPDATE/DELETE
- [ ] add draft support (see [issue #30](https://github.com/sapmentors/cds-pg/issues/30))
- [ ] add advanced deployment model that supports delta handling/migrations (see [issue #27](https://github.com/sapmentors/cds-pg/issues/27))
- [ ] add support for multitenancy (see [issue #25](https://github.com/sapmentors/cds-pg/issues/25))
- [ ] add support for full OData vocabulary
- [ ] add more tests to make the module more robust to @sap/cds core changes
- [ ] maybe add some PostgreSQL specific data type support

## usage in your CAP project

Add this package to your [SAP Cloud Application Programming Model](https://cap.cloud.sap/docs/) project by running:

```bash
npm install cds-pg
```

Then add this configuration to the cds section of your package.json:

```JSON
  "cds": {
    "requires": {
      "db": {
        "kind": "postgres"
      },
      "postgres": {
        "impl": "cds-pg",
        "model": [
          "srv"
        ]
      }
    }
  }
```

For local development you can provide the credentials in the file `default-env.json` in the root folder of your project:

```JSON
{
  "VCAP_SERVICES": {
    "postgres": [
      {
        "name": "postgres",
        "label": "postgres",
        "tags": [
          "postgres"
        ],
        "credentials": {
          "host": "localhost",
          "port": "5432",
          "database": "dbname",
          "user": "postgres",
          "password": "postgres",
          "schema":"public"
        }
      }
    ]
  }
}
```

### CDS deployment

With the command:

`npx cds-pg deploy srv --to db`

you can deploy all tables and views defined in your CDS model to the PostgreSQL DB specified in `default-env.json`. Initial data will also be filled from the provided .csv files following the approach described in [Providing Initial Data](https://cap.cloud.sap/docs/guides/databases#providing-initial-data). Be aware that the existing tables and views are deleted and then re-created according the CDS model.

## Projects using cds-pg

Example project [pg-beershop](https://github.com/gregorwolf/pg-beershop)
