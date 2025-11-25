# Trustify

### Infrastructure

- Move your terminal to:

```shell
 cd localdev/guacsec/trustify/
```

- Start Database and Keycloak:

```shell
podman compose up
```

### Start the Backend

Move your terminal to where your cloned https://github.com/guacsec/trustify

- Create tables in database:

```shell
cargo run --bin trustd db migrate
```

- Start the API service:

```shell
AUTHENTICATOR_OIDC_ISSUER_URL=http://localhost:9090/realms/trustify UI_ISSUER_URL=http://localhost:9090/realms/trustify AUTHENTICATOR_OIDC_CLIENT_IDS=frontend,cli cargo run --bin trustd api
```

- Start the Importer:

```shell
cargo run --bin trustd importer
```

- Verify everything works opening http://localhost:8080

### Start the Frontend

Move your terminal to where your cloned https://github.com/guacsec/trustify-ui

```shell
TRUSTIFY_API_URL=http://localhost:8080 OIDC_SERVER_URL=http://localhost:9090/realms/trustify npm run start:dev
```

### Execute playwright tests

Move your terminal to where your cloned https://github.com/guacsec/trustify-ui

- Start the playwright container

```shell
podman compose -f etc/compose.yaml up
```

- Run the tests:

```shell
TRUSTIFY_UI_URL=http://localhost:3000 PW_TEST_CONNECT_WS_ENDPOINT=ws://localhost:5000/ npm run -w e2e test -- --workers=4
```