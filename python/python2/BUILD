OPTS+=" --enable-shared \
        --enable-ipv6 \
        --enable-unicode=ucs4 \
        --with-threads \
        --with-system-expat \
        --with-system-ffi \
        --with-computed-gotos \
        --without-ensurepip"

_BASEVER=${VERSION%.*}
export OPT="$CFLAGS"

default_config &&
make &&
# Avoid rebuild on make install
sedit 's;^all:.*$;all: build_all;' Makefile &&
prepare_install &&
make altinstall &&

# Create a few symlinks
ln -sf python${_BASEVER}-config /usr/bin/python2-config &&
ln -sf python${_BASEVER} /usr/bin/python2 &&
ln -sf python-${_BASEVER}.pc /usr/lib/pkgconfig/python2.pc &&
ln -sf ../../libpython${_BASEVER}.so /usr/lib/python${_BASEVER}/config/libpython${_BASEVER}.so &&

install -dm755 /usr/lib/python${_BASEVER}/Tools/{i18n,scripts} &&
install -m755 $SOURCE_DIRECTORY/Tools/i18n/{msgfmt,pygettext}.py /usr/lib/python${_BASEVER}/Tools/i18n/ &&
install -m755 $SOURCE_DIRECTORY/Tools/scripts/{README,*.py} /usr/lib/python${_BASEVER}/Tools/scripts/ &&
install -m755 $SOURCE_DIRECTORY/Tools/scripts/pydoc /usr/bin/pydoc2 &&
install -m755 $SOURCE_DIRECTORY/Tools/scripts/idle /usr/bin/idle2 &&
install -m755 $SOURCE_DIRECTORY/Tools/scripts/2to3 /usr/bin/2to3-${_BASEVER} &&

# Docs
mv Misc/{cheatsheet,NEWS} . &&
chmod 644 cheatsheet NEWS README &&
gather_docs cheatsheet NEWS README
