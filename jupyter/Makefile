include .env

NAME   := tristanbrown/jupyterenv
TAG    := $(shell git rev-parse --short HEAD)
BRANCH := $(shell git rev-parse --abbrev-ref HEAD)
IMG    := ${NAME}:${TAG}
GIT    := ${NAME}:${BRANCH}
LATEST := ${NAME}:latest
 
build:
	docker build -t ${IMG} .
	docker tag ${IMG} ${GIT} 
	docker tag ${IMG} ${LATEST}
 
push:
	docker push ${IMG}
	docker push ${GIT}
	docker push ${LATEST}
 
login:
	@docker login -u ${DOCKER_USER} -p ${DOCKER_PASS}
