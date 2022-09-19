# GitHub Actions for deployment testing

## Top-level actions

See `extended.yaml` for an example of use.

### install-cli

Installs stepzen CLI.

### steprz-login

Logins into an account on steprz.net, e.g. `testa`.

Sets the environment for following steps in the job so that `stepzen` CLI points to `steprz.io`
and sets `${STEPZEN_APIKEY}` to be the api (non-admin) key.

Requires that `install-cli` is an earlier step.

### schema-test

Composite action that deploys a schema and then runs tests against it.
The directory is expected to be a javascript project with:

- `schemas` directory with `index.graphql` that will be deployed on steprz.net
- tests that run with `npm test`.

When the tests are run they can acces these environment variables:

- `STEPZEN_ACCOUNT` - account name (steprz.net)
- `STEPZEN_ENDPOINT` - URL of GraphQL endpoint
- `STEPZEN_APIKEY` - API key (non-admin) for endpoint

Requires that `install-cli` and `steprz-login` are earlier steps.

## Basic Actions

### schema-deploy

Deploys a schema and set an output value `endpoint` to the endpoint's URL.
