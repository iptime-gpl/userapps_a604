# uClibc dlopen tests
# Licensed under the LGPL v2.1, see the file COPYING.LIB in this tarball.

# rules need a little love to work with glibc ...
export UCLIBC_ONLY := 1

TESTS := dltest dltest2 dlstatic test1 test2 test3 dlundef dlafk dladdr

include ../Test.mak

CFLAGS_dltest    := -DLIBNAME="\"./libtest.so\""
CFLAGS_dltest2   := -DLIBNAME="\"./libtest3.so\""

LDFLAGS_dlstatic := -ldl
LDFLAGS_dltest   := -ldl -lpthread
LDFLAGS_dltest2  := -ldl -lpthread
LDFLAGS_dlundef  := -ldl
LDFLAGS_dlafk    := -ldl ./libafk.so -Wl,-rpath,.
LDFLAGS_test1    := -ldl
LDFLAGS_test2    := -ldl
LDFLAGS_test3    := -ldl ./libtest1.so ./libtest2.so -Wl,-rpath,.
LDFLAGS_dladdr   := -ldl

DEBUG_LIBS := X
WRAPPER := env $(DEBUG_LIBS)=all LD_LIBRARY_PATH="$$PWD:.:$(LD_LIBRARY_PATH)"

dltest: libtest.so
dltest2: libtest3.so
dlstatic: libstatic.so
dlundef: libundef.so
dlafk: libafk.so
libafk.so: libafk-temp.so
LDFLAGS_libafk.so := ./libafk-temp.so -Wl,-rpath,.
test1: libtest1.so
test2: libtest1.so libtest2.so
test3: libtest1.so libtest2.so
libtest1.so: libtest2.so
LDFLAGS_libtest1.so := ./libtest2.so -Wl,-rpath,.
LDFLAGS_libtest2.so := -Wl,-rpath,.
LDFLAGS_libtest3.so := -lpthread -Wl,-rpath,.
