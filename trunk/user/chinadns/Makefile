SRC_NAME=ChinaDNS-1.3.2

CFLAGS += -O3 -pipe -ffast-math -ftree-vectorize -ffunction-sections -fdata-sections
LDFLAGS += -Wl,--gc-sections

all: config_test build

config_test:
	( if [ -f ./config_done ]; then \
		echo "The same configuration."; \
	else \
		make configure && touch config_done; \
	fi )

configure:
	( cd $(SRC_NAME) ; \
	./autogen.sh && ./configure \
		--host=$(HOST_TARGET) \
		--build=$(HOST_BUILD) ; \
	)

build:
	$(MAKE) -C $(SRC_NAME)

clean:
	( if [ -f ./config_done ]; then \
		$(MAKE) -C $(SRC_NAME) clean; \
	fi )
	rm -f config_done
	rm -f chinadns

romfs:
	cp $(SRC_NAME)/src/chinadns .
	$(STRIP) chinadns
	$(ROMFSINST) /usr/bin/chinadns

