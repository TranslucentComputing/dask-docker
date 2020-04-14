TAG ?= 1.0.1
REGISTRY ?= gcr.io/tcinc-dev
IMGNAME ?= dask
IMAGE ?= $(REGISTRY)/$(IMGNAME)

.PHONY: build

build:
	docker build --pull -t $(IMAGE):$(TAG) .

push:
	gcloud docker --server=gcr.io -- push $(IMAGE):$(TAG)