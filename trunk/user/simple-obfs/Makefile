SRC_NAME=simple-obfs-0.0.1

CFLAGS += -O3 -pipe -ffast-math -ftree-vectorize -ffunction-sections -fdata-sections
CPPFLAGS += -O3 -pipe -ffast-math -ftree-vectorize -ffunction-sections -fdata-sections
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
	./configure \
		--disable-documentation \
		--disable-assert \
		--disable-ssp \
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
	rm -f obfs-server
	rm -f obfs-local

romfs:
	cp $(SRC_NAME)/src/obfs-server .
	cp $(SRC_NAME)/src/obfs-local .
	$(STRIP) obfs-server
	$(STRIP) obfs-local
	$(ROMFSINST) /usr/bin/obfs-server
	$(ROMFSINST) /usr/bin/obfs-local

