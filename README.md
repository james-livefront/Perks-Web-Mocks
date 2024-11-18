# Optum Perks Online Care Mock Data Config

This repo contains code for generating a JSON file we can feed to Mockoon CLI to get Online Care API spec compliant data back.

## Contents

- [Optum Perks Online Care Mock Data Config](#optum-perks-online-care-mock-data-config)
  - [Contents](#contents)
  - [Using the Mockoon JSON file](#using-the-mockoon-json-file)
  - [Updating the Mockoon JSON file](#updating-the-mockoon-json-file)

## Using the Mockoon JSON file

To use the current [Mockoon JSON file](./src/mockoon_env.final.json) as your mock server config. Do the following.

1. Run `npm install` if you haven't yet.
2. Run `npm run pipeline` to add rules for all examples and generate the additional, necessary mock data files.
3. Run `npx mockoon-cli start -d ./src/mockoon_env.final.json`.
4. Send calls to [http://localhost:3005/api/v1](http://localhost:3005/api/v1). So if you wanted to, for example, hit the `/conditions` endpoint, you would call [http://localhost:3005/api/v1/conditions](http://localhost:3005/api/v1/conditions).

## Updating the Mockoon JSON file

The Mockoon JSON file should never be edited manually. If you want to test something quick with a manual edit, make sure to either discard the change once you no longer need it, or add the change via script if you want it to persist.

If the spec is updated and we need to get the mock server in sync with it, complete the following steps.

1. Replace [the bundled yaml spec file](./config/openapi.yml) with the updated file.
2. Run `api-types` to update our generated types.
3. Make the necessary fixes for any type errors in our [responses](./src/responses) and [mock data](./src/mock-data) files.
4. Feed the new bundled spec file you used in step one to the Mockoon desktop app and see all of the routes populate.
5. Click on the three dots in the configuration you just created (in the farthest left panel) and click "Copy configuration to clipboard (JSON)".
6. Replace the current [Mockoon JSON file](./src/mockoon_env.final.json) with the JSON you just copied to your clipboard.
7. Run `npm run pipeline` to make the necessary changes to the new config file.
8. Run `npx mockoon-cli start -d ./src/mockoon_env.final.json` and make sure the mock server is working by hitting the unchanged routes and the routes that had updates at [http://localhost:3005/api/v1](http://localhost:3005/api/v1).
