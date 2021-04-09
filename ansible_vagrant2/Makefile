
# Root directory of the project (absolute path).
ROOTDIR=$(dir $(abspath $(lastword $(MAKEFILE_LIST))))
# Base path used to install.
DESTDIR ?= /usr/local
# Emojis
WHALE = "🇩"
ONI = "👹"
PHONY=help

setup: ## Install all requirements for your system
	@echo Installing packages
	@sudo apt-get update && \
		sudo apt-get install -y \
			wget \
			curl \
			virtualbox \
			virtualbox—ext–pack \
			vagrant \
			python3 \
			python3-pip
	@pip3 install -U pip ansible molecule


ansible_roles:
	@ansible-galaxy install --roles-path ./provisioning/roles -r provisioning/requirements.yml 


vagrant: ## Create and provision all vagrant VMs
	@vagrant up --parallel --provision


docker_lb: ## Ups a load_balancer for the others
	@docker-compose -f nginx/docker-compose.yml up --build


vendor: ## vendor
	@echo "$@: Felipe Rocha, Raipe Systems $(ONI)"


help: ## this help
	@awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z_-]+:.*?## / {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}' $(MAKEFILE_LIST) | sort