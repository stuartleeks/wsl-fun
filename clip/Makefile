
help: ## show this help
	@grep -E '^[a-zA-Z0-9_-]+:.*?## .*$$' $(MAKEFILE_LIST) \
	| awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%s\033[0m|%s\n", $$1, $$2}' \
	| column -t -s '|'

docker-build: ## build the Docker image
	docker build -t wsl-fun-clip container

docker-run: ## run a disposable interactive instance
	docker run --rm -it --name wsl-fun-clip --mount type=bind,source="$(PWD)/container",target=/demo --workdir /demo wsl-fun-clip bash

