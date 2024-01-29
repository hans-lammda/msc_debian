LINARO_PATH=gcc-linaro-7.5.0-2019.12-x86_64_aarch64-linux-gnu.tar.xz
LINARO_URL=https://releases.linaro.org/components/toolchain/binaries/latest-7/aarch64-linux-gnu/$(LINARO_PATH)



all: clean download unpack 

.PHONY: download

download: 
	mkdir -p download 
	( cd download && wget $(LINARO_URL) ) 

unpack: 
	 sudo tar -C /opt -xf download/$(LINARO_PATH) 

clean: 
	rm -rf download
	

