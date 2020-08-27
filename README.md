<center><a href="https://summerofcode.withgoogle.com/projects/#6653942668197888"><img src="https://developers.google.com/open-source/gsoc/resources/downloads/GSoC-logo-horizontal.svg" alt="gsoc" height="50"/></a></center>

# Google Summer of Code 2020 - Websocket support for Ignite Realtime's Smack

* **Student:** Aditya Borikar
* **Mentors:** Florian Schmaus, Paul Schaub
* **Organisation:** XMPP Standards Foundation
* **Sub-Organisation:** Ignite Realtime

### Welcome to my GSoC 2020 project page.

XMPP protocols are the base protocols for instant messaging and presence. Applications using XMPP make use of either of the three transports: TCP, Bidirectional-streams Over Synchronous(BOSH) and websocket transport. Smack already has support for TCP and BOSH based connections. And my job was to add websocket support to Smack.

## XEP-0156: Discovering Alternative XMPP Connection Methods

The XEP mentions two lookup processes, out of which we use the HTTP Web-host Metadata lookup. Conceptually, the host-meta lookup process used for the WebSocket binding is analogous to the DNS SRV lookup process used for the TCP binding.

### The process can be divided into two steps:

1) Send a request over secure HTTP to the path
   "/.well-known/host-meta" at an HTTP origin that matches the XMPP service domain (e.g., a URL of "https://im.example.org/.well-known/host-meta" if the XMPP service domain is "im.example.org").

2) Retrieve a host-meta document specifying a link relation type of "urn:xmpp:alt-connections:websocket", such as: 

	```xml
	<XRD xmlns='http://docs.oasis-open.org/ns/xri/xrd-1.0'>
         	<Link rel="urn:xmpp:alt-connections:websocket" href="wss://im.example.org:443/ws" />
       </XRD>
       ```

To obtain a websocket endpoint we look for the hyperlink reference corresponding to the link relation "urn:xmpp:alt-connections:websocket".

The implementation can be found [here](https://github.com/igniterealtime/Smack/commit/dcb66eef592bf3959a3aaafae0802e0b35500e2d).

## Finite State Machine of Smack's Modular Architecture

<center>
    <img src="https://adiaholic.github.io/gsoc2020/assets/images/websocketAndTcp.png">
</center>

As it is apparent from the diagram above, we have successfully plugged in EstablishingWebsocketConnection phase inside Smack's modular architecture.


## Commits made:

** [Add support for Http Lookup method through XEP-0156](https://github.com/igniterealtime/Smack/commit/dcb66eef592bf3959a3aaafae0802e0b35500e2d)

** [Remove unrequired assignment of value to connectionEndpoint variable](https://github.com/igniterealtime/Smack/commit/45f75d5ce0dcb4e8c68ea59109211dda8799565f)

** [Add simple XMPP connection integration test](https://github.com/igniterealtime/Smack/commit/fcaeca48ec0eb3848c51ee778ce3626b06c9b7db)

** [Position parser at START_ELEMENT before parsing](https://github.com/igniterealtime/Smack/commit/7796b367cc779a001a42c7313bbdaf5f50c325b6)

** [XmlEnvironment: Use correct method to obtain effective namespace.](https://github.com/igniterealtime/Smack/commit/c9cf4f15419be5a20bb7a046facfb664b0141f38)

** [Introduce AbstractStreamOpen and AbstractStreamClose](https://github.com/igniterealtime/Smack/commit/9fcc97836bf5bb8fb788dc44675bf4e5f50e6f25)

** [Introduce StreamOpenAndCloseFactory for modular architecture](https://github.com/igniterealtime/Smack/commit/0e49adff1d4d88359c3a0c2c2d60efdfc31677e8)

** [Make ModularXmppClientToServerConnectionConfiguration.addModule() public](https://github.com/igniterealtime/Smack/commit/db385e6595d02b95ce0c221e718780a8ee59fc89)

** [Use AbstractStreamOpen instead of StreamOpen to open stream](https://github.com/igniterealtime/Smack/commit/648a1cfab1f69f9b00070182d55142d3d0f35965)

** [Introduce websocket module into smack]()


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


Over the period of past three months, I was exposed to innumerable difficult situations like imperfect timing, choosing unpropitious approach, relying on bad information and various technical frameworks. I however enjoyed tackling these unfavourable scenarios. I was encouraged by my mentors to consume more information and think in the right direction. I loved the dynamic of open source community, the exacting and collective environment helped me function at my best.

