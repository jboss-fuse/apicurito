ASSETS := ../../../deploy
TMPL := tmpl
YAML := yaml
NAMESPACE_VAR := {NAMESPACE}
USER_VAR := {KUBE_USER}
TAG_VAR := {TAG}
IMAGE_VAR := {IMAGE}

DEPLOYMENT := ./deployment.gen

# User customisable variables
IMAGE ?=  registry.redhat.io/fuse7/fuse-apicurito-rhel7-operator
NAMESPACE ?= apicurito
TAG ?= 1.9

.PHONY: sync init

# start-sync
#
# Copy the deploy template from the deploy directory
#
sync:
	cp $(ASSETS)/operator.yaml $(DEPLOYMENT).$(TMPL)
	sed -i 's~apicurio/apicurito-operator~$(IMAGE_VAR):$(TAG_VAR)~' $(DEPLOYMENT).$(TMPL)
# end-sync

init: sync
	cp $(DEPLOYMENT).$(TMPL) $(DEPLOYMENT).$(YAML)
	sed -i 's/$(NAMESPACE_VAR)/$(NAMESPACE)/' $(DEPLOYMENT).$(YAML)
	sed -i 's/$(TAG_VAR)/$(TAG)/' $(DEPLOYMENT).$(YAML)
	sed -i 's~$(IMAGE_VAR)~$(IMAGE)~' $(DEPLOYMENT).$(YAML)
