SPIGOT_VERSION = 1.13.1
DOCKER_REPO = docker.ttys0.net
ROOT_DIR := $(dir $(abspath $(lastword $(MAKEFILE_LIST))))

# build spigot
.PHONEY: spigot
spigot:
	@echo 'building spigot $(SPIGOT_VERSION)'
ifneq ($(wildcard *.jar),)
	@echo 'removing existing jar files...'
	@rm -f *.jar
endif
	@echo 'running spigot-build.docker'
	docker build --build-arg SPIGOT_VERSION=$(SPIGOT_VERSION) --tag spigot-build:$(SPIGOT_VERSION) --file spigot-build.docker .
	docker run --rm -v $(ROOT_DIR):/spigot spigot-build:$(SPIGOT_VERSION)
	docker build --tag $(DOCKER_REPO)/spigot-server:$(SPIGOT_VERSION) --file spigot-server.docker .
	docker push $(DOCKER_REPO)/spigot-server:$(SPIGOT_VERSION)

.PHONEY: bungee
bungee:
	@echo 'building bungeecord'
	docker build --tag $(DOCKER_REPO)/bungeecord --file bungeecord.docker .
	docker push $(DOCKER_REPO)/bungeecord
