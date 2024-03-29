# Packet Switching

## Introdution

History: pass it.

Circuit Switching VS Packet Switching

Circuit Switching:

Each call has its own private, guaranteed, isolated data rate from end-to-end.

the problem:

* Inefficient: Internet communication is bursty.
* Diverse Rates
* State Management:

![circuitProblem](./assets/circuitProblem.png)

Packet Switching:

* Packets are routed individually.
* All packets share the full capacity of a link.
* The router maintain no per-communication state.

the advantage:

![Paketadvantage](./assets/Paketadvantage.png)

### Useful defination

1. Propagation delay:
$$
t_l = \frac{l}{v}
$$
It means the time spends a bit to traveling over link .

2. Packetization delay:
$$
t_p = \frac{p}{r}
$$
The time from when the first to the last bit of a packet is transmittd.
`p` is the size of packet. `r` is speed of packeting.bits/s

**Be careful:**

A 1kbit packet takes 1.024s to be transmitted onto a 1kb/s link.

`1kbit = 1024 bit` but `1kb/s = 1000 bit/s`

### End-to-end delay

![EndtoEndDelay](./assets/EndtoEndDelay.png)

**NOTE**: We don't send the packet until the whole packet is put on the link.

This picture is important. Try to think these cases:

1. if one packet is huge, what dose the image look like?
2. if we split a huge packet to be many small pakcter, what dose the image look like?

Generally, $t_p$ and $t_l$ are deciced, but $Q(t)$ queue dalay in swither is .

### Playback buffer

![PlaybackBuffers](./assets/PlaybackBuffers.png)

We will make buffer bigger that is called "Rebuffering" if buffer is dificit.

## Queue Model

it is for router queue.

![SimpleQueueModel](./assets/SimpleQueueModel.png)

![WhyNotSendEntire](./assets/WhyNotSendEntire.png)

### Statistical Multiplexing

3-5 waitting
TODO

### Useful Properties

Queues with Random Arrival Processes

1. Burstiness increases delay
2. Determinism minimizes delay
3. Little's Result
4. The M/M/1 queue

#### Little's Result

The Poisson process:
$$
P_k(t) = \frac{(\lambda t)^k}{k!} \exp{(-\lambda t)} $$

![BeWarned](./assets/BeWarned.png)

#### M/M/1 queue

![MM1Queue](./assets/MM1Queue.png)

Ref: <https://zhuanlan.zhihu.com/p/90923312>
Conclusion: we need $\lambda <  \mu$

## How work

![How work](./assets/HowWork.png)

![GenericPacketSwicth](./assets/GenericPacketSwicth.png)

![EthernetSwitch](./assets/EthernetSwitch.png)

![InternetRouter](./assets/InternetRouter.png)

### Forwarding Table

EthernetSwitch: hash table;

InternetRouter: Longest prefix match. Tree or TCAM

### Switch

1. Output queued packet switch
    Problem:如果有N个端口以速率R来到，在拥塞情况下，一个Buffer可能要承受(N+1)R读写速率。
2. Input queued packet switch
    每一个Buffer对应一个输入端口，所以即使在拥塞情况下，一个Buffer最多承受2R。会遇到Head of line blocking问题。解决Virtual output queues。

![VirtualOutputQueues.png](./assets/VirtualOutputQueues.png)

The property of Output queued packet switch:

* They are "work conserving".
* Throughput is maximized.
* Expected delay is minimized.

Which one we use

The simplest and slowest is output queueing, which **minimizes packet delay**.

The High performance switcher is input queueing, with virtual output queues to maximize throughput.

### Strict priorities and guaranteed flow rate

![FIFO](./assets/FIFO.png)

When we have congestion, we'll see whoever sends at the highest rate, in fact, will receive the highest usage of link.

![Strict priorities](./assets/StrictPriorities.png)

it run the danger of stavring out low priority traffic when there are lots of high prioroty flow.

![Weight priorities](./assets/WeightPriorities.png)

![Summary.png](./assets/Summary.png)

Delay guaranteed

to be continued.
