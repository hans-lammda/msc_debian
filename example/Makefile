CROSS_COMPILE=/opt/gcc-linaro-7.5.0-2019.12-x86_64_aarch64-linux-gnu/bin/aarch64-linux-gnu
CC=$(CROSS_COMPILE)-gcc


static: 
	$(CC)  hello.c -static -o hello.static

dynamic:
	$(CC)  hello.c  -o hello

clean: 
	rm -f hello hello.static 

