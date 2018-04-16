# Hello World Example

Starts a FreeRTOS task to print "Hello World"

See the README.md file in the upper level 'examples' directory for more information about examples.

## Note about "CMake-based" IDEs

This ESP32 template contains a CMakeList.txt for CLion/QtCreator. But it's only used for indexing as the compilation needs original Kconfig scripts.

Before import, you need to: 

1. either comment out Arduino framework related script in CMakeList template if you don't need to use that, or pull a copy of Arduino framework to `components` directory. 
2. You may also need to compile the project manually by commandline manually (i.e. `make menuconfig` then `make`) before importing the project to IDE. Otherwise the indexer may not work.

By the way, this template has been tested and proved working with CLion 2018.1.1 on macOS 10.13.4 and Ubuntu 18.04.