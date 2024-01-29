LINARO_PATH=gcc-linaro-11.3.1-2022.06-x86_64_aarch64-linux-gnu.tar.xz
LINARO_URL=https://snapshots.linaro.org/gnu-toolchain/11.3-2022.06-1/aarch64-linux-gnu/$(LINARO_PATH)

all: clean download unpack 

.PHONY: download

download: 
	mkdir -p download 
	( cd download && wget $(LINARO_URL) ) 

unpack: 
	 sudo tar -C /opt -xf download/$(LINARO_PATH) 

clean: 
	rm -rf download
	

