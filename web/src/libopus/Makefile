.PHONY: module opus
all: module 

module:
	emcc -O3 -s WASM=1 -s ALLOW_MEMORY_GROWTH=1 -s EXPORT_ES6=1 -s SINGLE_FILE=1 \
	-s USE_ES6_IMPORT_META=0 -s EXTRA_EXPORTED_RUNTIME_METHODS='["cwrap"]' \
	-s BINARYEN_ASYNC_COMPILATION=1 -s EXPORTED_FUNCTIONS="['_free', '_malloc']" \
	-s MODULARIZE=1 -s EXPORT_NAME="libopus" -s ASSERTIONS=1 \
	-Iopus/include -Lopus/.libs -lopus api.c -o index.js

opus:
	cd opus && ./autogen.sh
	cd opus && emconfigure ./configure CFLAGS="-O3" --disable-stack-protector \
	--disable-intrinsics --disable-shared --enable-static
	cd opus && emmake make clean
	cd opus && emmake make -j$(nproc)