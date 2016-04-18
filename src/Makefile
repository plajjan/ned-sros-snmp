all:	fxs 
# Include standard NCS examples build definitions and rules
include $(NCS_DIR)/src/ncs/build/include.ncs.mk


SRC = $(wildcard mibs/*.mib)
FXS = $(SRC:mibs/%.mib=ncsc-out/modules/fxs/%.fxs)

fxs:	ncsc-out/modules

ncsc-out/modules:	$(SRC)
	$(NCSC) --ncs-compile-mib-bundle mibs \
                 --ncs-device-dir ncsc-out && \
        cp ncsc-out/modules/fxs/*.fxs ../load-dir;
	touch -m ncsc-out/modules


clean:
	rm -rf ncsc-out/* ncsc-out/.done ../fxs/* ../load-dir/*
	rm -f ../*jar/*.jar
