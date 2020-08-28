<center><a href="https://summerofcode.withgoogle.com/projects/#6653942668197888"><img src="https://developers.google.com/open-source/gsoc/resources/downloads/GSoC-logo-horizontal.svg" alt="gsoc" height="50"/></a></center>

# Google Summer of Code 2020 - Websocket support for Ignite Realtime's Smack

* **Student:** Aditya Borikar
* **Mentors:** Florian Schmaus, Paul Schaub
* **Umbrella-Organisation:** XMPP Standards Foundation
* **Sub-Organisation:** Ignite Realtime

### Welcome to my GSoC 2020 project page.

XMPP protocols are the base protocols for instant messaging and presence. It stands for eXtensible Messaging and Presence Protocol. Applications using XMPP make use of either of the three transports: TCP, Bidirectional-streams Over Synchronous(BOSH) and websocket transport. Ignite Realtime's Smack already has support for TCP and BOSH based connections. And my job was to add websocket support to Smack.

## XEP-0156: Discovering Alternative XMPP Connection Methods

The XEP mentions two lookup processes, out of which we use the HTTP Web-host Metadata lookup for fetching websocket endpoints. Conceptually, the host-meta lookup process used for the Websocket binding is analogous to the DNS SRV lookup process used for the TCP binding.

### The process can be divided into two steps:

1) Send a request over secure HTTP to the path
   "/.well-known/host-meta" at an HTTP origin that matches the XMPP service domain (e.g., a URL of "https://im.example.org/.well-known/host-meta" if the XMPP service domain is "im.example.org").

2) Retrieve a host-meta document specifying a link relation type of "urn:xmpp:alt-connections:websocket", such as: 


	<XRD xmlns='http://docs.oasis-open.org/ns/xri/xrd-1.0'>
	    <Link rel="urn:xmpp:alt-connections:websocket" href="wss://im.example.org:443/ws" />
	</XRD>
       

To obtain a websocket endpoint we look for the hyperlink reference corresponding to the link relation "urn:xmpp:alt-connections:websocket". The implementation for http lookup can be found [here](https://github.com/igniterealtime/Smack/commit/dcb66eef592bf3959a3aaafae0802e0b35500e2d).

## Modular refinements

There is a significant difference in the stream opening and closing elements between TCP connections and websocket based connections.

A typical tcp stream open element is like,

	<stream:stream
		from='juliet@im.example.com'
		to='im.example.com'
		version='1.0'
		xml:lang='en'
		xmlns='jabber:client'
		xmlns:stream='http://etherx.jabber.org/streams'>


whereas a websocket stream open element is,

	<open xmlns="urn:ietf:params:xml:ns:xmpp-framing"
		to="example.com"
		version="1.0" />



This means that these stream elements are supposed to be transport specific and that Smack should take care of that. To solve this problem, Smack now uses StreamOpenAndCloseFactory. This change along with a few relevant changes can be found [here](https://github.com/igniterealtime/Smack/commit/0e49adff1d4d88359c3a0c2c2d60efdfc31677e8), [here](https://github.com/igniterealtime/Smack/commit/9fcc97836bf5bb8fb788dc44675bf4e5f50e6f25) and [here](https://github.com/igniterealtime/Smack/commit/648a1cfab1f69f9b00070182d55142d3d0f35965)!

## Current Finite State Machine of Smack's Modular Architecture

<center>
    <img src="https://adiaholic.github.io/GSOC2020/assets/images/websocketAndTcp.png">
</center>

As it is apparent from the diagram above, we have successfully plugged in EstablishingWebsocketConnection phase inside Smack's modular architecture. This implementation resides inside the smack-websocket module and can be found [here](https://github.com/igniterealtime/Smack/pull/399).

The use case for establishing a websocket connection can be found inside [smack-repl]().

To test Smack's transport against modular architecture, there is now a very simple integration test in place which can be used to transfer a message stanza from user to another. The integration test can be found [here](https://github.com/igniterealtime/Smack/commit/fcaeca48ec0eb3848c51ee778ce3626b06c9b7db).

Apart from these, I am especially happy about my [first ever contribution](https://github.com/xsf/xeps/commit/b5924b77908d6762345f95d2972169cc3f93c785) to an XEP!

### What more can be expected ahead

The websocket implementation is yet to be incorporated into Spark. This also means that Spark is unaware of Smack's modular architecture. Since the modular architecture itself is quite new, while working on Spark we might discover cases which are yet to be considered. Along with that, smack-websocket is prone to improvements as and when realised.


## Thanks

Over the period of past three months, I was exposed to innumerable difficult situations like imperfect timing, choosing unpropitious approach, and various technical frameworks. I however enjoyed tackling these scenarios. I was encouraged by my mentors to consume more information and think in the right direction. I loved the dynamic of the Ignite Realtime community, the exacting and collective environment helped me function at my best.

Thanks to [Florian Schmaus](https://github.com/Flowdalic) and [Paul Schaub](https://github.com/vanitasvitae) for pushing me forward when I got stuck and appreciating me when did things the right way. Special thanks to [Guus der Kinderen](https://github.com/guusdk) for going out out his way to guide me during my proposal and sticking with Paul and me during Ignite Realtime's weekly meet to make me feel welcome.
