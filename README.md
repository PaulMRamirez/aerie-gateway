![GitHub package.json version](https://img.shields.io/github/package-json/v/NASA-AMMOS/plandev-gateway?color=brightgreen)

# plandev-gateway

The API gateway for [PlanDev](https://github.com/NASA-AMMOS/plandev).

## Need Help?

- Join us on the [NASA-AMMOS Slack](https://join.slack.com/t/nasa-ammos/shared_invite/zt-1mlgmk5c2-MgqVSyKzVRUWrXy87FNqPw) (#plandev-users)
- Contact plandev-support@googlegroups.com

## Develop

First make sure you have [Node.js LTS](https://nodejs.org) installed.

If you are doing active local development outside of a container, duplicate the `.env.template` and rename it to `.env`. Set the default `GATEWAY_DB_USER`, `GATEWAY_DB_PASSWORD`, and `HASURA_GRAPHQL_JWT_SECRET` [environment variables](./docs/ENVIRONMENT.md).
If your Hasura instance is not hosted on `http://localhost:8080`, update the value of `HASURA_API_URL` in the `.env` as well. Afterwards, run the following:

```sh
npm install
npm run dev
```

This will watch for code changes and rebuild and restart the gateway server automatically.

If you are running PlanDev Gateway within a container (i.e. the docker-compose from the main PlanDev repo), run the following before starting the container:

```sh
npm install
npm run build
npm start
```

## License

The scripts and documentation in this project are released under the [MIT License](LICENSE).
