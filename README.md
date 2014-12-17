# dot-kerlrc

Configuration file `.kerlrc` for [kerl](https://github.com/yrashk/kerl/).

## compilation command set example

    kerl update releases
    kerl build 17.4 17.4
    kerl install 17.4 /home/kenji/otp/17.4

## For obtaining git release from GitHub Erlang/OTP archive

    # use the following `kerl build git` command
    kerl build git https://github.com/erlang/otp/ OTP-17.4 17.4

## Enforcing concurrency in `make`

    # set env variable MAKEFLAGS (see otp_build script)
    env MAKEFLAGS="-j8" kerl build 17.4 17.4-test

## .kerlrc

### NOTE VERY WELL

* Since .kerlrc is a dot file for /bin/sh, exporting inside the environment will define the env variables
* The `export` commands will affect *your login environment* when activating curl!
* Rule of thumb: keep .kerlrc entries *all commented out* or use independent shell scripts

### FreeBSD clang without .kerlrc with an independent shell script

    # with stack protector and dtrace options
    # note: multiple options in `CFLAGS` have to be specified in the environment
    env KERL_CONFIGURE_OPTIONS="--disable-native-libs \
                                --with-dynamic-trace=dtrace \
                                --with-ssl=/usr/local \
                                --with-javac \
                                --disable-hipe \
                                --enable-kernel-poll \
                                --with-wx-config=/usr/local/bin/wxgtk2u-2.8-config \
                                --without-odbc \
                                --enable-threads \
                                --enable-sctp \
                                --enable-smp-support" \
        CC=clang CXX=clang \
        CFLAGS="-g -O0 -fstack-protector" \
        LDFLAGS="-fstack-protector" \
    kerl build 17.4 17.4

### for FreeBSD 10.1-STABLE

* See `dot-kerlrc-freebsd`
* Use `clang`

### for Mac OS X 10.10

* See `dot-kerlrc-osx`
* Use `gcc-4.9` in HomeBrew

