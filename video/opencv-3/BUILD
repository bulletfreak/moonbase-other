if in_depends $MODULE qt5; then
  . /etc/profile.d/qt5.rc
else
  if in_depends $MODULE qt4; then
    . /etc/profile.d/qt4.rc
  else
    OPTS+=" -DWITH_QT=OFF"
  fi
fi &&

# bug: examples have to be build, if they (the sources) will be installed
if [[ "`get_module_config EXAMPLES`" = "y" ]]; then
  OPTS+=" -DBUILD_EXAMPLES=ON"
else
  OPTS+=" -DBUILD_EXAMPLES=OFF"
fi &&

OPTS+=" -DBUILD_WITH_DEBUG_INFO=OFF \
        -DBUILD_TESTS=OFF \
        -DBUILD_EXAMPLES=OFF \
        -DCMAKE_SKIP_RPATH=ON \
        -DBUILD_PERF_TESTS=OFF \
        -DBUILD_SHARED_LIBS=ON \
        -DINSTALL_C_EXAMPLES=ON \
        -DBUILD_WITH_DYNAMIC_IPP=ON \
        -DINSTALL_PYTHON_EXAMPLES=OFF \
        -DOPENCV_EXTRA_MODULES_PATH=../opencv_contrib-$VERSION/modules" &&

default_cmake_build
