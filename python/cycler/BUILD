python3 ./setup.py build &&

prepare_install &&

python3 ./setup.py install --root=/ &&

if module_installed setuptools; then
  python ./setup.py build &&
  python ./setup.py install --root=/
fi
