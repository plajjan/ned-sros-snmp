# Include standard NCS examples build definitions and rules
include $(NCS_DIR)/src/ncs/build/include.ncs.mk


SRC = $(wildcard mibs/*.mib)
YANG = $(SRC:mibs/%.mib=yang/%.yang)
FXS = $(SRC:mibs/%.mib=ncsc-out/modules/fxs/%.fxs)

all: fxs

#fxs:	ncsc-out/modules


yang/%.yang: mibs/%.mib
	mkdir -p yang
	cd mibs && /opt/ncs/current/bin/ncsc --mib2yang-std --prefix $(shell echo $@ | tr '[:upper:]' '[:lower:]' | sed -e 's/^yang.//' -e 's/\.yang//') -o ../$@ ../$<

fxs: $(YANG)
	/opt/ncs/current/bin/ncsc --ncs-compile-bundle yang --ncs-skip-config --ncs-device-type snmp-ned --ncs-device-dir ncsc-out

#$(YANG):yang/%.yang:mib/%.mib
#	@echo $@ $<



#ncsc-out/modules:	$(SRC)
#	$(NCSC) --ncs-compile-mib-bundle mibs \
#		--ncs-skip-config --ncs-device-dir ncsc-out && \
#		cp ncsc-out/modules/fxs/*.fxs ../load-dir;
#	touch -m ncsc-out/modules


clean:
	rm -rf ncsc-out/* ncsc-out/.done ../fxs/* ../load-dir/* yang/*
	rm -f ../*jar/*.jar
