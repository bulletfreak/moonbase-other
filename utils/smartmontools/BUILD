OPTS+=" --with-initscriptdir=/etc/init.d \
        --prefix=/usr"

default_build &&

if [ -e /etc/init.d/smartd ]; then
    rm -f /etc/init.d/smartd
    rm -f /etc/rc?.d/???smartd
fi
