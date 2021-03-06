export CFLAGS+=" -fPIC"
  
OPTS+=" --disable-static \
        --disable-krb4 \
        --disable-srp \
        --disable-srp-setpass \
        --disable-cmulocal \
        --enable-login \
        --enable-ntlm \
        --enable-otp \
        --enable-auth-sasldb \
        --without-sqlite \
        --with-devrandom=/dev/urandom \
        --with-dbpath=/var/lib/sasl/sasl.db  \
        --with-pwcheck=/run/saslauthd \
        --with-saslauthd=/run/saslauthd \
        --with-configdir=/etc/sasl2 \
        --with-plugindir=/usr/lib/sasl2"

if module_installed Linux-PAM; then
  OPTS+=" --with-pam"
else
  OPTS+=" --without-pam"
fi &&

# Enable sql if any of the following databases is a dependency
if in_depends $MODULE sqlite || in_depends $MODULE postgresql || in_depends $MODULE %MYSQL; then
  OPTS+=" --enable-sql"
else
  OPTS+=" --disable-sql"
fi &&

# gdbm first if both gdbm and db was enabled
if in_depends $MODULE gdbm; then
  OPTS+=" --with-dblib=gdbm"
elif in_depends $MODULE db; then
  OPTS+=" --with-dblib=berkeley"
else
  OPTS+=" --with-dblib=none"
fi &&

# Autoconf stuff
rm -f config/config.guess config/config.sub &&
rm -f config/ltconfig config/ltmain.sh config/libtool.m4 &&
rm -fr autom4te.cache &&
libtoolize -c &&
aclocal -I config -I cmulocal &&
automake -a -c &&
autoheader &&
autoconf &&

pushd saslauthd &&
rm -f config/config.guess config/config.sub &&
rm -f config/ltconfig config/ltmain.sh config/libtool.m4 &&
rm -fr autom4te.cache &&
libtoolize -c &&
aclocal -I config -I ../cmulocal -I ../config &&
automake -a -c &&
autoheader &&
autoconf &&
popd &&

default_build &&

if [ ! -d /var/lib/sasl ]; then
  mkdir -p /var/lib/sasl
fi &&

if [ ! -d /etc/sasl2 ]; then
  mkdir -p /etc/sasl2
fi &&

if [ ! -e /etc/sasl2/smtpd.conf ] ; then
  echo "pwcheck_method: sasldb" > /etc/sasl2/smtpd.conf
fi
