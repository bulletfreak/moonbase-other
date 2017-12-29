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

_PYDESTDIR=$SOURCE_DIRECTORY/__pythondest
mkdir -p $_PYDESTDIR &&
default_config &&
make &&
# Avoid rebuild on make install
sedit 's;^all:.*$;all: build_all;' Makefile &&
make DESTDIR="$_PYDESTDIR" altinstall maninstall &&

rm "$_PYDESTDIR"/usr/share/man/man1/python.1 &&

# Create a few symlinks
ln -sf python${_BASEVER}-config "$_PYDESTDIR"/usr/bin/python2-config &&
ln -sf python${_BASEVER} "$_PYDESTDIR"/usr/bin/python2 &&
ln -sf python-${_BASEVER}.pc "$_PYDESTDIR"/usr/lib/pkgconfig/python2.pc &&
ln -sf ../../libpython${_BASEVER}.so "$_PYDESTDIR"/usr/lib/python${_BASEVER}/config/libpython${_BASEVER}.so &&

install -dm755 "$_PYDESTDIR"/usr/lib/python${_BASEVER}/Tools/{i18n,scripts} &&
install -m755 $SOURCE_DIRECTORY/Tools/i18n/{msgfmt,pygettext}.py "$_PYDESTDIR"/usr/lib/python${_BASEVER}/Tools/i18n/ &&
install -m755 $SOURCE_DIRECTORY/Tools/scripts/{README,*.py} "$_PYDESTDIR"/usr/lib/python${_BASEVER}/Tools/scripts/ &&
install -m755 $SOURCE_DIRECTORY/Tools/scripts/pydoc "$_PYDESTDIR"/usr/bin/pydoc2 &&
install -m755 $SOURCE_DIRECTORY/Tools/scripts/idle "$_PYDESTDIR"/usr/bin/idle2 &&
install -m755 $SOURCE_DIRECTORY/Tools/scripts/2to3 "$_PYDESTDIR"/usr/bin/2to3-${_BASEVER} &&

prepare_install &&

cp -rfv --remove-destination "$_PYDESTDIR"/* / &&

# Docs
mv Misc/{cheatsheet,NEWS} . &&
chmod 644 cheatsheet NEWS README &&
gather_docs cheatsheet NEWS README
