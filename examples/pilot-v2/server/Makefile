SHELL := /bin/bash

all: binary docker deploy

deploy:
	# ./build/distribute-image.sh go-chassis/pilotv2server:latest
	- kubectl delete -f ./build/k8s/
	kubectl apply -f ./build/k8s/

binary:
	CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo -ldflags '-w' -o ./build/pilotv2server

docker: binary
	cp -r ./conf ./build/
	docker build -t go-chassis/pilotv2server:latest ./build

