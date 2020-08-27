<center><a href="https://summerofcode.withgoogle.com/projects/#6653942668197888"><img src="https://developers.google.com/open-source/gsoc/resources/downloads/GSoC-logo-horizontal.svg" alt="gsoc" height="50"/></a></center>

# Google Summer of Code 2020 - Websocket support for Ignite Realtime's Smack

* **Student:** Aditya Borikar
* **Mentors:** Florian Schmaus, Paul Schaub
* **Organisation:** XMPP Standards Foundation
* **Sub-Organisation:** Ignite Realtime

## Introduction

XMPP RFCs and Specifications define connection establishment over TCP, BOSH and websockets. Smack currently establishes connection between Server and Client using TCP and BOSH. BOSH suffers from high transport overhead as compared to TCP. Also various issues with long polling are suggested to have an impact upon BOSH based systems [RFC 6202 Section 2.2]. WebSocket provides an alternative to the limitation of inefficient communication between the server and the client by providing bi-directional, full-duplex, real-time client/server communications. The protocol consists of an opening handshake followed by basic message framing, layered over TCP [RFC 6455]. Adding WebSocket support to Smack will allow it to establish a continuous Client-Server connection with less overhead.


## Timeline
| Date                 | Description  |
|----------------------|--------------|
|Chapter 0<br>(16-05-2020)|[Introduction](https://adiaholic.github.io/gsoc2020/2020/05/16/Chapter-0-Introduction.html) |
|Chapter 1<br>(24-05-2020)| [Handshake](https://adiaholic.github.io/gsoc2020/2020/05/24/Chapter-1-Handshake.html)|
|Chapter 2<br>(31-05-2020)| [Modular Shift](https://adiaholic.github.io/gsoc2020/2020/05/31/Chapter-2-Modular-Shift.html)|
|Chapter 3<br>(21-06-2020)| [SASL Negotiations](https://adiaholic.github.io/gsoc2020/2020/06/07/Chapter-3-sasl-negotiations.html)|
|Chapter 4<br>(28-06-2020)| [Fixing loose endpoints](https://adiaholic.github.io/gsoc2020/2020/06/14/Chapter-4-fix-loose-endpoints.html)|
|Chapter 5<br>(05-07-2020)| [Discrete Http lookup method](https://adiaholic.github.io/gsoc2020/2020/06/21/Chapter-5-Discrete-Http-Lookup-Method.html)|
|Chapter 6<br>(12-07-2020)| [A part of the whole, merged](https://adiaholic.github.io/gsoc2020/2020/06/28/Chapter-6-Part-Of-The-Whole.html)|
|Chapter 7<br>(19-07-2020)| [The Bigger Picture](https://adiaholic.github.io/gsoc2020/2020/07/06/Chapter-7-The-Bigger-Picture.html)|
|Chapter 8<br>(26-07-2020)| [Reworking FSM](https://adiaholic.github.io/gsoc2020/2020/07/12/Chapter-8-Reworking-FSM.html)|
|Chapter 9<br>(02-08-2020)| [Bug fixation](https://adiaholic.github.io/gsoc2020/2020/07/19/Chapter-9-Fixing-Bugs.html)|
|Chapter 10<br>(09-08-2020)| [End of the second phase](https://adiaholic.github.io/gsoc2020/2020/07/26/Chapter-10-End-of-second-phase.html)|
|Chapter 11<br>(16-08-2020)| [TLS: The Last Stage](https://adiaholic.github.io/gsoc2020/2020/08/02/Chapter-11-TLS.html)|
|Chapter 12<br>(23-08-2020)| [Titbits](https://adiaholic.github.io/gsoc2020/2020/08/09/Chapter-12-Titbits.html)|
|Chapter 13<br>(16-08-2020)| [Testing](https://adiaholic.github.io/gsoc2020/2020/08/16/Chapter-13-Testing.html)|
|Chapter 14<br>(23-08-2020)| [Final Stage](https://adiaholic.github.io/gsoc2020/2020/08/23/Chapter-14-Final-Stages.html)|

