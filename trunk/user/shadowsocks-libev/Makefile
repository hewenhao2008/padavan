SRC_NAME=shadowsocks-libev

CFLAGS += -O3 -pipe -ffast-math -ftree-vectorize -flto -ffunction-sections -fdata-sections
LDFLAGS += -Wl,-flto --gc-sections

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
	rm -f ss-local
	rm -f ss-redir
	rm -f ss-tunnel

romfs:
	cp $(SRC_NAME)/src/ss-local .
	cp $(SRC_NAME)/src/ss-redir .
	cp $(SRC_NAME)/src/ss-tunnel .
	$(STRIP) ss-local
	$(STRIP) ss-redir
	$(STRIP) ss-tunnel
	$(ROMFSINST) /usr/bin/ss-local
	$(ROMFSINST) /usr/bin/ss-redir
	$(ROMFSINST) /usr/bin/ss-tunnel

