export DOCKER_REPO ?= europe-docker.pkg.dev/vaxine/ci

export ELIXIR_VERSION ?= 1.13.4
export OTP_VERSION ?= 24.3
export DEBIAN_VERSION ?= bullseye-20210902-slim

export SYSBENCH_COMMIT ?= df89d34c410a2277e19f77e47e535d0890b2029b

ifdef CI
	build_command = buildx build --platform linux/arm64/v8,linux/amd6 --push
else
	build_command = build
endif

all: electric_builder electric_runner sysbench
.PHONY: all electric_builder electric_runner sysbench

electric_builder:
	cd electric_builder && docker $(build_command) \
		--build-arg ELIXIR_VERSION \
		--build-arg OTP_VERSION \
		--build-arg DEBIAN_VERSION \
		-t ${DOCKER_REPO}/electric-builder:latest .

electric_runner:
	cd electric_runner && docker $(build_command) \
		--build-arg DEBIAN_VERSION \
		-t ${DOCKER_REPO}/electric-runner:latest .

sysbench:
	cd sysbench && docker $(build_command) \
		--build-arg SYSBENCH_COMMIT \
		-t ${DOCKER_REPO}/sysbench:latest .
