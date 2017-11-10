


cd /home/ffmpeg
NDK=/home/ndk
PLATFORM=$NDK/platforms/android-23/arch-arm
PREBUILT=$NDK/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64
PREFIX=/home/android-ffmpeg


./configure --target-os=linux --prefix=$PREFIX --enable-cross-compile --enable-runtime-cpudetect --disable-asm --arch=arm --cc=$PREBUILT/bin/arm-linux-androideabi-gcc --cross-prefix=$PREBUILT/bin/arm-linux-androideabi- --disable-stripping \--nm=$PREBUILT/bin/arm-linux-androideabi-nm --sysroot=$PLATFORM --enable-nonfree --enable-version3 --disable-everything --enable-gpl --disable-doc --enable-avresample --enable-demuxer=rtsp --enable-muxer=rtsp --disable-ffplay --disable-ffserver --enable-ffmpeg --disable-ffprobe --enable-libx264 --enable-encoder=libx264 --enable-decoder=h264 --enable-protocol=rtp --enable-hwaccels --enable-zlib --disable-devices --disable-avdevice --extra-cflags="-I/home/android-ffmpeg/include -fPIC -DANDROID -D__thumb__ -mthumb -Wfatal-errors -Wno-deprecated -mfloat-abi=softfp -mfpu=vfpv3-d16 -marm -march=armv7-a" --extra-ldflags="-L/home/android-ffmpeg/lib"



make&make -j8 install

$PREBUILT/bin/arm-linux-androideabi-ar d libavcodec/libavcodec.a inverse.o
$PREBUILT/bin/arm-linux-androideabi-ld -rpath-link=$PLATFORM/usr/lib -L$PLATFORM/usr/lib -L$PREFIX/lib  -soname libffmpeg.so -shared -nostdlib   -Bsymbolic --whole-archive --no-undefined -o $PREFIX/libffmpeg.so libavcodec/libavcodec.a libavfilter/libavfilter.a libavresample/libavresample.a libavformat/libavformat.a libavutil/libavutil.a libswscale/libswscale.a libpostproc/libpostproc.a -lc -lm -lz -ldl -llog -lx264 --dynamic-linker=/system/bin/linker $PREBUILT/lib/gcc/arm-linux-androideabi/4.9.x/libgcc.a

#压缩
$PREBUILT/bin/arm-linux-androideabi-strip --strip-unneeded libffmpeg.so