#
# Make Options
#
MK_OPTIONS := -s

.PHONY: $(SUBDIRS)

SYNCDIRS := ../app ../bases/crd ../bases/deployment ../bases/grant ../bases/role

sync:
	for dir in $(SYNCDIRS); do \
    $(MAKE) $(MK_OPTIONS) -C $$dir; \
  done

INSTALLDIR := $(RELEASE_NAME)-installer
RELEASEDIRS := ../app ../bases ../operator ../setup

create:
	#@ Make a new apicurito builddirectory
	mkdir -p $(INSTALLDIR)
	#@ Copy directories into build directory
	for dir in $(RELEASEDIRS); do \
    cp -rf $$dir $(INSTALLDIR)/; \
  done
	#@ Remove sync rules from Makefiles
	for f in `find $(INSTALLDIR) -name Makefile`; do \
		echo "sync:" > $$f; \
		echo "  #@ Not required in release" >> $$f; \
	done
	#@ Copy the root Makefile into build directory
	cp -f ../Makefile $(INSTALLDIR)/

release: sync create
ifndef RELEASE_VERSION
	$(error RELEASE_VERSION is not set)
endif
ifndef RELEASE_NAME
	$(error RELEASE_NAME is not set)
endif
	tar zcvf $(INSTALLDIR)-$(RELEASE_VERSION).tar.gz $(INSTALLDIR)

clean:
	rm -rf *-installer *.tar.gz
