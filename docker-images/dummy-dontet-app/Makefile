
IMAGE_NAME ?= dummy-dotnet-app
REGISTRY ?= registry.local:5000

GIT_VERSION := $(shell git describe --tags --always --dirty --match='v*' 2>/dev/null || echo "unknown")
GIT_COMMIT := $(shell git rev-parse --short HEAD 2>/dev/null || echo "unknown")
IS_DIRTY := $(shell git diff --quiet 2>/dev/null || echo "-dirty")

TAG ?= $(GIT_VERSION)$(IS_DIRTY)
FULL_IMAGE ?= $(if $(REGISTRY),$(REGISTRY)/$(IMAGE_NAME):$(TAG),$(IMAGE_NAME):$(TAG))

build:
	@echo "Building Docker image: $(FULL_IMAGE)"
	docker build -t $(FULL_IMAGE) .
	@echo "Build complete!"
	@echo "Image: $(FULL_IMAGE)"

push: build
	@if [ -z "$(REGISTRY)" ]; then \
		echo "Error: REGISTRY is not set. Please set it in the Makefile or as an environment variable."; \
		echo "Example: make push REGISTRY=docker.io/username"; \
		exit 1; \
	fi
	@echo "Pushing image: $(FULL_IMAGE)"
	docker push $(FULL_IMAGE)
	@echo "Push complete!"

.PHONY: help build push clean info
