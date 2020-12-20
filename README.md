# WIP

Attempt to create a bitsery adapter that uses [liburing](https://github.com/axboe/liburing) for better performance.

## Requirements

This project depends on [bitsery](https://github.com/fraillt/bitsery) and on [liburing](https://github.com/axboe/liburing). It also provides a [FindIoUring.cmake](cmake/FindIoUring.cmake) find module for liburing for easier setup.
So you need to do two steps:

* install [bitsery](https://github.com/fraillt/bitsery)
```bash
git clone https://github.com/fraillt/bitsery
cd bitsery
mkdir build && cd build
cmake .. && make install
```

* install [liburing](https://github.com/axboe/liburing)
```bash
git clone https://github.com/axboe/liburing
cd liburing
make install 
```

and you're ready to go ;)

## How to develop

```bash
(from project root)
mkdir build && cd build
cmake ..
make
ctest

```


## TODO

* implement adapter that uses liburing
* discuss how to make it easier for users to use it
