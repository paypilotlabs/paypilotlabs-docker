# PayPilotLabs Docker

The image build kit for all PayPilotLabs products. It turns the PayPilotLabs framework and one product into a single Docker image, the same way every time.

## What it does

- Holds one build recipe: `images/custom/Containerfile`.
- Builds an image from the PayPilotLabs framework plus the apps listed in an `apps.json` file.
- Includes the fix for Apple M4 machines (`ENV OPENSSL_armcap=0`), so builds and containers run on Docker Desktop there.
- Also keeps ready-made Compose files, helper scripts and guides for running and developing in containers (`compose.yaml`, `overrides/`, `pwd.yml`, `development/`, `docs/`).

## How it helps your business

- One recipe for every product. A fix made here reaches Helpdesk, CRM, ERP, HRMS, Insights and Builder alike.
- Builds are repeatable. The same inputs give the same image on any machine.
- Nothing to set up by hand. A product only says which apps it needs.
- Secrets stay out of the image. `apps.json` goes in as a BuildKit secret.

## How it fits with other PayPilotLabs products

Each product (`paypilotlabs-helpdesk`, `-crm`, `-erp`, `-hrms`, `-insights`, `-builder`) has a `docker/build.sh`. That script:

1. Clones this repo (branch `main`, or the one in `DOCKER_REF`).
2. Builds `images/custom/Containerfile` with `paypilotlabs-framework` as the base and the product's `apps.json` on top.
3. Tags the result `paypilotlabs<product>`, for example `paypilotlabshelpdesk`.

Products run that image next to MariaDB and Redis. Run `./docker/build.sh` inside a product repo to use this kit. You do not need to clone this repo yourself.

## Run and develop

Try a disposable demo (not for production):

```sh
git clone https://github.com/paypilotlabs/paypilotlabs-docker
cd paypilotlabs-docker
docker compose -f pwd.yml up -d
```

Wait a couple of minutes for the site to be created, then open port `8080` (user `Administrator`, password `admin`).

Requirements: [Docker](https://docs.docker.com/get-docker/), [Docker Compose v2](https://docs.docker.com/compose/), [git](https://git-scm.com/).

More guides are in [`docs/`](docs/): [getting started](docs/getting-started.md), [ARM64 notes](docs/01-getting-started/03-arm64.md), [development](docs/05-development/01-development.md).

## Pull upstream updates later

This repo is a fork. The original project's address is in [NOTICE.md](NOTICE.md). To take in its new work:

```sh
git remote add upstream <address from NOTICE.md>   # once
git fetch upstream
git switch -c chore/upstream-sync main
git merge upstream/main
```

Re-check that `ENV OPENSSL_armcap=0` is still in the `base` stage of `images/custom/Containerfile` and `images/production/Containerfile`, then open a pull request.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Questions and requests: https://paypilotlabs.com/roadmap/

## Licence

MIT. See [LICENSE](LICENSE). Based on open-source work by others; see NOTICE.md for credits.
