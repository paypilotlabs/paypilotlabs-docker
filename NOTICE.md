# Notice

PayPilotLabs Docker is a fork of [frappe/frappe_docker](https://github.com/frappe/frappe_docker),
Copyright (c) 2017 Frappe Technologies Pvt. Ltd., released under the MIT License (see `LICENSE`).

The PayPilotLabs products (`paypilotlabs-helpdesk`, `-crm`, `-erp`, `-hrms`, `-insights`, `-builder`)
build their images from `images/custom/Containerfile` in this repository.

PayPilotLabs changes:
- `images/custom/Containerfile`, `images/production/Containerfile`: `ENV OPENSSL_armcap=0` in the
  `base` stage, so builds and containers run on Apple M4 under Docker Desktop.
