RUN_ARGS=--runtime nvidia --gpus=all

.PHONY: all
all: build

.PHONY: shell run
shell:
	docker run --rm -it ${RUN_ARGS} stixes/motioneye /bin/bash
run:
	docker run --rm -it ${RUN_ARGS} -p 8765:8765 stixes/motioneye

.PHONY: lint
lint:
	docker run -i --rm -v ${PWD}:/work -w /work hadolint/hadolint hadolint Dockerfile

.PHONY: build
build:
	docker build . -t stixes/motioneye -t motioneye
