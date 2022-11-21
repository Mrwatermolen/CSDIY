# Lab1

In Lab 1, you’ll implement a stream reassembler—a module that stitches small pieces of the byte stream (known as substrings, or segments) back into a contiguous stream of bytes in the correct sequence

**StreamReassembler**: it will recieve substrings ,try to megre them to be contigous and then write the consisting of a string to the ByteStream.

It should:

* have flow control. attribute : Capacity: the  maximum number of bytes it is ever allowed to store. it equals to (unread bytes + unreassmbled bytes)
* combine string correctly
* write bytes with correctl order to ByteStream

Program Structure and Design of the StreamReassembler: `std::map`(for its orderliness)

Implementation Challenges:
>number of RX bytes is incorrect

solve: megre strings to one if they are continuous as soon as possible.
