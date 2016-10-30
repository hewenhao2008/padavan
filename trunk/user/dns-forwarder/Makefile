SRC_NAME=dns-forwarder-1.1.1

CFLAGS += -O3 -pipe -ffast-math -ftree-vectorize -ffunction-sections -fdata-sections
LDFLAGS += -Wl,--gc-sections

all: build

build:
	$(MAKE) -C $(SRC_NAME)
	touch build_done

clean:
	( if [ -f ./build_done ]; then \
		$(MAKE) -C $(SRC_NAME) clean; \
	fi )
	rm -f build_done
	rm -f dns-forwarder

romfs:
	cp $(SRC_NAME)/src/dns-forwarder .
	$(STRIP) dns-forwarder
	$(ROMFSINST) /usr/bin/dns-forwarder

