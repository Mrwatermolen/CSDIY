# Lab3

Implement the TCPSender.

## Pineline

### 1. Initialiaze TCPSender

Upper service will initialiaze a `TCPSender` object. You should keep `TCPSender`state is closed.

### 2. Send SYN

Upper service will call function `fill_window()` to ask `TCPSender` to generate a segment with SYN is true to send to `_segment_out`.

### 3. Processing

#### ACK Recieved

Upper service will call function `ack_received()` to tell that ack has come.

You should update `seqno_next` and  remove any that have now been fully acknowledged. `TCPSender` should fill the window again if new space has opened up.

#### Segment was lost

Upper service will call function `tick()` to tell that a certain number of milliseconds since the last time this method
was called.

**the `tick()` method is your only access to the passage of time.**

You should check if `TCPSender` need to retransmit the earliest (lowest sequence number) segment.

More detail: [lab3-3.1 How does the TCPSender know if a segment was lost](./lab3.pdf)

### 4. Send FIN

You can know whether `TCPSender` send the segment including FIN is true by check `_stream.eof()`

### 5. ACK FIN

You should promiss no byte is in flight.

### More Detail

[lab3.pdf](./lab3.pdf)

## Easily ignored in lab

* the SYN and FIN flags occupy a sequence number each, which means that they occupy space in the window but not in `TCPConfig::MAX_PAYLOAD_SIZE`
* The only way to increase the `RTO` and the number of consecutive retransmissions is the window size is nonzero when tick is called and the retransmission timer has expired.
* You should retransmit only the earliest segment and the reset the retransmission timer.
* When filling window, treat a '0' window size as equal to '1' but don't back off `RTO`

> Hint: create payload: `auto payload = Buffer(_stream.read(read_bytes));`
