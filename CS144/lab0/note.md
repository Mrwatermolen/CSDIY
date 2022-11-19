# Lab0

## Prepare

Read [lab0.pdf](https://cs144.github.io/assignments/lab0.pdf)
Read [lab0 document](https://cs144.github.io/doc/lab0/index.html)

> Run Ubuntu version 18.04 LTS, then run our setup script. You can do this on your actual computer, inside VirtualBox, or on EC2 or another virtual machine

### Build Env

```bash
git clone --recursive https://github.com/Kiprey/sponge.git
mkdir -p sponge/build
cd sponge/build
CC=gcc CXX=g++ CLANG_TIDY=clang-tidy-15 CLANG_FORMAT=clang-format-15  cmake .. -DCMAKE_BUILD_TYPE=Debug
make
```

## Networking by hand

### Fetch a Web page

Assignment: Now that you know how to fetch a Web page by hand, show us you
can! Use the above technique to fetch the URL <http://cs144.keithw.org/lab0/sunetid>,
replacing sunetid with your own primary SUNet ID. You will receive a secret code in
the X-Your-Code-Is: header. Save your SUNet ID and the code for inclusion in your
writeup.

```bash
curl -v http://cs144.keithw.org/lab0/sunetid
```

### Send yourself an emai

No method

### Listening and connecting

following

## Writing a network program using an OS stream socket

you will simply use the operating system’s pre-existing support for the Transmission Control Protocol. You’ll write a program called “webget” that creates a TCP stream socket, connects to a Web server, and fetches a page

> Pay particular attention to the documentation for the FileDescriptor, Socket,TCPSocket, and Address classes. (Note that a Socket is a type of FileDescriptor, and a TCPSocket is a type of Socket.)

## An in-memory reliable byte stream

You will implement, in memory on a single computer, an object that provides this abstraction.

Your byte stream will also be flow-controlled to limit its memory consumption at any given time.

The object is initialized with a particular “capacity”: the maximum number of bytes it’s willing to store in its own memory at any given point
