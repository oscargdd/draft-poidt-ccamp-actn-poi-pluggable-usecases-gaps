---
title: "Use cases, Network Scenarios and gap analys for Packet Optical Integration (POI) with coherent plugables under ACTN Framework"
abbrev: "POI coherent plugables"
docname: draft-poidt-ccamp-actn-poi-pluggable-usecases-gaps-latest

stand_alone: true
ipr: trust200902
area: "Routing"
wg: ccamp
cat: info
submissiontype: IETF  # also: "independent", "IAB", or "IRTF"

keyword:
 - coherent
 - photonic
 - pluggable
 - plugs
 - CMIS
 - I2C
 - OpenConfig
 - Optical
 - Packet

author:
  -
    ins: O. G. de. Dios
    fullname: Oscar Gonzalez de Dios
    role: editor
    org: Telefonica
    email: oscar.gonzalezdedios@telefonica.com

 -
    ins: J. Bouquier
    name: Jean-Francois Bouquier
    org: Vodafone
    email: jeff.bouquier@vodafone.com

  -
    ins: J. M.
    name: Julien Meuric
    org: Orange
    email: julien.meuric@orange.com

  -
    ins: G. M.
    name: Gyan Mishra
    org: Ciena
    email: gyan.s.mishra@verizon.com

  -
    ins: G. G.
    fullname: Gabriele Galimberti
    organization: Individual
    email: ggalimbe56@gmail.com

contributor:
  -
    ins: A. Guo
    fullname: Aihua Guo
    organization: Futurewei Technologies
    email: aihuaguo.ietf@gmail.com
  -
    name: Brent Foster
    role: editor
    org: Cisco
    street: Research Triangle Park
    city: North Carolina
    country: UNITED STATES OF AMERICA
    email: brfoster@cisco.com

  -
    name: Daniele Ceccarelli
    role: editor
    org: Cisco
    email: daniele.ietf@gmail.com
  -
    ins: I. Busi
    fullname:  Italo Busi
    organization: Huawei Technologies
    email: italo.busi@huawei.com

  -
    name: Ori Gerstel
    role: editor
    org: Cisco
    street: AMOT ATRIUM Tower 19th floor
    city: TEL AVIV-YAFO, TA
    country: Israel
    email: ogerstel@cisco.com
 -
    ins: N. Davis
    name: Nigel Davis
    org: Ciena
    email: ndavis@ciena.com
 -
    ins: R. Rokui
    name: Reza Rokui
    org: Ciena
    email: rrokui@ciena.com
-
    ins: P. Maheshwari
    fullname: Praveen Maheshwari
    organization: Airtel
    email: Praveen.Maheshwari@airtel.com


normative:

   OIF-CMIS:
              title: "OIF Implementation Agreement (IA) Common Management Interface Specification (CMIS))"
              date: 2022-04-27
              target: https://www.oiforum.com/wp-content/uploads/OIF-CMIS-05.2.pdf

informative:

   actn-rfc:
              title: "Framework for Abstraction and Control of TE Networks ACTN"
              date: 2018-12-19
              target: https://datatracker.ietf.org/doc/rfc8453/

   MANTRA-whitepaper-IPoWDM-convergent-SDN-architecture:
              title: "IPoWDM convergent SDN architecture - Motivation, technical definition & challenges"
              date: 2022-08-31
              target: https://telecominfraproject.com/wp-content/uploads/TIP_OOPT_MANTRA_IP_over_DWDM_Whitepaper-Final-Version3.pdf

   ITU-T G.sup39:
              title: "ITU-T Recommendation G.Sup39 (02/16): Optical system design and engineering considerations"
              date: 2016-02-26
              target: https://www.itu.int/rec/T-REC-G.Sup39-201602-I/en

--- abstract

This document provides general overarching guidelines for control and management of packet over optical converged networks with coherent pluggables and focuses on operators' use cases and network scenarios. It provides a set of use cases which are needed for the control and management of the packet over optical networks which comprise devices with mixes of packet and optical functions where the optical functions may be provided on coherent pluggables. The document provides a gap analysis of the data models and protocols to solve the use cases.

--- middle

# Terminology
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT"
"SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in the
document are to be interpreted as described in {{!RFC2119}}.

The following terms abbreviations are used in this document:

* Coherent plug/pluggable: A small form factor coherent optical module
* O-PNC: The control functions specializing in management/control of optical and photonic functions (virtual or physical). See {{actn-rfc}}
* P-PNC: The control functions specializing in management/control of packet functions (virtual or physical). See {{actn-rfc}}
* xPonder: Short for Transponder and/or Muxponder

# Introduction

Packet traffic has been transferred over optical networks for many years blending the benefits of optical transmission and switching with packet switching. Optical systems have been separated from packet systems, both of which have had specific dedicated devices. In many existing network deployments, the packet and the optical networks are engineered, operated and controlled independently. The operation of these packet and optical networks is often siloed which results in non-optimal and inefficient networking. Both packet and optical systems have had relatively independent evolution. Optical systems have been developed with increasing capacity especially with the emergence of coherent optical techniques.

Optical component design has continued to improve density to the point where a whole coherent optical terminal system that use to require many circuit packs can now fit onto a single small form factor "coherent plug". Placing coherent plugs in a device with packet functions can reduce network cost, power consumption and footprint as well as improve data transfer rates, reduce latency and expand capacity (note that in some cases, other engineering and deployment considerations still lead to separate packet and optical solutions).

Optical transmission/switching is analogue and requires complex and holistic control. Consequently, coordination of control of the coherent plugs (in a device with packet functions) with the control of the rest of the optical network is highly desirable as this best enables robust network functionality and simplifies network operations.

The combination of these above trends along with the desire to select best in breed components has led to the emergence of open optical plugs that offer a standard bus for traffic and that use CMIS {{OIF-CMIS}}, extended with Coherent CMIS, between coherent pluggables and host device. These plugs are such that a plug from vendor X can be installed in vendor Y's device with packet functions etc.

An architecture analysis has been carried out by the MANTRA sub-group in the OOPT / TIP group (Open Optical & Packet Transport / Telecom Infra Project) {{MANTRA-whitepaper-IPoWDM-convergent-SDN-architecture}}.

This document provides guidellines for control and management of packet over optical converged networks and it is divided into following sections:

* Section 3 Packet over optical converged network context
* Section 4 Network Scenarios
* Section 5 Use cases for the control and management of Packet over Optical Converged Networks
* Section 5 Gap analysis



# Packet over Optical Converged Network Context

A packet over optical network represents an efficient paradigm that harnesses the power of both packet-switching and optical technologies. In this approach, the overlay IP or MPLS packets are transmitted through an underlying optical network. The fusion of packet and optical networks offer a host of advantages, including accelerated data transfer rates, diminished latency, and expanded network capacity.

In general, two deployment models can be used to deploy the packet over optical networks:

* Traditional architecture deployment model
* Deployment model with coherent pluggables

## Traditional Architecture Deployment Model

The traditional architecture involves separation of the packet network from the optical network as shown in {{figure-traditional}}. In traditional approach, the packet layer responsible for routing and forwarding is decoupled from the underlying optical transport layer. This approach offers several benefits, including the ability to scale each layer independently, optimize resource utilization, and simplify network management through centralized software control.

Disaggregation enables network operators to choose best-of-breed components for each layer, fostering innovation and competition in the networking industry. However, implementing and managing a disaggregated network also comes with challenges related to interoperability, integration, and maintaining end-to-end performance across the various layers.

~~~
      |----------|                                   |----------|
      |  Packet  |           IP Link                 |  Packet  |
      |  Device  |===================================|  Device  |
      |    1     |\                                 /|     2    |
      |----------| \   Grey                        / |----------|
                    \  Optics                     /
                     |                           |
        ............ | ......................... | ............
        .            |                           |            .
        .    |---------|     |-----------|     |---------|    .
        .    | xPonder |-----| Photonics |-----| xPonder |    .
        .    |---------|     |-----------|     |---------|    .
        .......................................................

        Optical Network = Photonics + xPonder

  Legend:
    ====       IP Link
    ----       Optical fibers
    ++++       Coherent pluggables
    xPonder:   Muxponder or transponder
    Photonics: ROADM + Amp + Regen
~~~
{: #figure-traditional title="Packet over Optics Traditional Architecture Deployment Model"}

## Deployment Model with Coherent Pluggables

The second approach is to take advantage of the small implementation footprint of the xPonder functions and to deploy these functions on a single small form factor plug (aka Coherent pluggables) and then place plugs directly into the packet devices as shown in {{figure-with-plug}}(A). Placing this small form factor pluggable in a device with packet functions can reduce network cost, power consumption and footprint (when these benefits are not outweighed by other engineering considerations). Depending on the application, distance between packet devices, quality of fibers and so on it might be that there is no need for a ROADM network, i.e., direct connectivity between packet devices via plugs is possible.

By incorporating coherent plugs into routers, network operators can achieve higher data rates, greater spectral efficiency, and improved tolerance to optical impairments. This is especially valuable in scenarios where traditional electronic signaling might encounter limitations. Coherent plugs enable routers to leverage advanced modulation schemes, digital signal processing, and error correction techniques, enhancing their ability to handle complex optical signals.

One of the key advantages of using coherent plugs in routers is the potential to bridge the gap between long-haul and metro networks, providing a seamless and efficient transition of data across various network segments. This technology can contribute to the evolution of high-speed data centers, interconnection between data centers, and the overall growth of data-intensive applications.

as noted above, for some use-cases when the distance between packet devices is short and optical power of pluggables are enough, the photonics devices might not be needed as shown in {{figure-with-plug}}(B).

~~~
      |-----------|                               |-----------|
      |  Packet   |           IP Link             |   Packet  |
      |  Device  +++++ ======================= +++++  Device  |
      |    1      |\                             /|     2     |
      |-----------| \                           / |-----------|
                     \  DWDM Optics            /
                      |                       |
                      |     |-----------|     |
                      |-----| Photonics |-----|
                            |-----------|

                                 (A)

      |-----------|                               |-----------|
      |  Packet   |           IP Link             |   Packet  |
      |  Device  +++++ ======================= +++++  Device  |
      |    1      |\                             /|     2     |
      |-----------| \                           / |-----------|
                     |                         |
                     |-------------------------|

                                (B)

  Legend:
    ====       IP Link
    ----       Optical fibers
    ++++       Coherent pluggables
    xPonder:   Muxponder or transponder
    Photonics: ROADM + Amp + Regen
    Optical Network: Photonics + pluggables
~~~
{: #figure-with-plug title="Packet over Optics Deployment Model with Coherent Plugs"}

In reality, the operators' packet over optical networks will most likely be a combination of networks shown in {{figure-traditional}} and {{figure-with-plug}} where the optical network contains both coherent pluggables and xPonders as shown in {{figure-with-plug-and-xponder}}.

~~~
      |-----------|                                   |-----------|
      |  Packet   |              IP Link              |   Packet  |
      |  Device  +++++ =========================== +++++  Device  |
      |    1      |\                                 /|     2     |
      |-----------| \                               / |-----------|
                     \----------|     |------------/
                                |     |
             |---------|     |-----------|      |---------|
             |         |     |           |      |         |
             | xPonder |-----| Photonics |------| xPonder |
             |         |     |           |      |         |
             |---------|     |-----------|      |---------|
                    |                              |
                    |                              |
      |----------| /                                \ |----------|
      |  Packet  |/             IP Link              \|  Packet  |
      |  Device  |====================================|  Device  |
      |    3     |                                    |     4    |
      |----------|                                    |----------|

      Optical Network: Photonics + pluggables + xPonder

  Legend:
    ====       IP Link
    ----       Optical fibers
    ++++       Coherent pluggables
    xPonder:   Muxponder or transponder
    Photonics: ROADM + Amp + Regen
~~~
{: #figure-with-plug-and-xponder title="Packet over Optics Deployment Model with Coherent Plugs and xPonders"}


# Network Scenarios

This section provides a set of packet over optical network scenarios, starting with the most common ones.

## Scenario 1 - High capacity point to point connection over dedicated direct fiber

As depicted in {{figure-topo1}}, this scenario considers a point-to-point optical service over a short distance (e.g., up to 100 km) using dedicated fiber.

Note that there is no amplification and no protection in this scenario.

~~~
    Packet                                                             Packet
    Device A                                                           Device B
    +----+             IP Link (between Router Ports)                  +----+
    |    |.............................................................|    |
    |    |                                                             |    |
    |    |             Optical Service (Plug-to-Plug)                  |    |
    |    |    .....................................................    |    |
    |  |------|                                                   |------|  |
    |  |      |                                                   |      |  |
    |  |Plug A|===================================================|Plug B|  |
    |  |      |                                                   |      |  |
    |  |------|                                                   |------|  |
    |    |                                                             |    |
    +----+                                                             +----+
~~~
{: #figure-topo1 title="Network topology with dedicated direct fiber"}

## Scenario B- High capacity point to point over shared fiber

This scenario extends {{figure-topo1}} by making more efficient use of the deployed fiber infrastructure.

As shown in {{figure-topo2}}, this scenario considers a point-to-point optical service over a short distance (e.g., up to 100 km) using a physical optical network with DWDM filters and amplifiers. Several point-to-point connections can be multiplexed from the same packet devices.

Note that there is no protection in this scenario.

~~~
    Packet                                                             Packet
    Device A                                                           Device B
    +----+             IP Link (between Router Ports)                  +----+
    |    |.............................................................|    |
    |    |                                                             |    |
    |    |             Optical Service (Plug-to-Plug)                  |    |
    |    |    .....................................................    |    |
    |  |------|                                                   |------|  |
    |  |      |      |-------|      |-------|      |-------|      |      |  |
    |  |Plug A|======| Filter|======|  AMP  |======| Filter|======|Plug B|  |
    |  |      |  ||==|       |      |       |      |       |==||  |      |  |
    |  |------|  ||  |-------|      |-------|      |-------|  ||  |------|  |
    |    |       ||                                           ||       |    |
    +----+       ||                                           ||       +----+
                 ||                                           ||
       |------|  ||                                           ||  |------|
       |      |==||                                           ||==|      |
       |Plug C|                                                   |Plug D|
       |      |                                                   |      |
       |------|                                                   |------|
~~~
{: #figure-topo2 title="Network topology with shared direct fiber network"}

## Scenario 3 - High capacity point to point over metro-regional shared meshed network

This scenario extends {{figure-topo2}} by making more flexible use of the fiber network infrastructure.

As shown in {{figure-topo3}}, this scenario considers a point-to-point optical service over a metro/regional network (e.g., up to 500 km). The metro/regional network contains DWDM filters, amplifiers and optical switching. ({{pluggables-operators-requirements}}, Page 4, "Point to point connection over metro/regional areas").

Note that there is no resilience in this scenario. (CHECK AS RESTORATION COULD BE A CHOICE)

~~~
    Packet                                                             Packet
    Device A                                                           Device B
    +----+              IP Link (between Router Ports)                 +----+
    |    |.............................................................|    |
    |    |                                                             |    |
    |    |              Optical Service (Plug-to-Plug)                 |    |
    |    |    .....................................................    |    |
    |  |------|                                                   |------|  |
    |  |      |      |-------|      |-------|      |-------|      |      |  |
    |  |Plug A|======| ROADM |======| ROADM |======| ROADM |======|Plug B|  |
    |  |      |      | + Amp |      |       |      | + Amp |      |      |  |
    |  |------|      |-------|      |-------|      |-------|      |------|  |
    |    |                                                             |    |
    +----+                                                             +----+
~~~
{: #figure-topo3 title="Network topology with shared switched fiber network"}



## Sceanrio D- High capacity point to point optical connection between plug and xPonder

This scenario, shown in {{figure-topo5}}and extends network topologies {{figure-topo1}} to {{figure-topo4}} and covers a corner case, where one end of an optical service is terminated on a plug and the other end is terminated on a traditional xPonder (transponder or muxponder) with grey optics to a packet device. This scenario is encountered when one of the packet device does not support coherent plugables.

~~~
    Packet                                                             Packet
    Device A                                                           Device B
    +----+             IP Link (between Router Ports)                  +----+
    |    |.............................................................|    |
    |    |                                                             |    |
    |    |     Optical Service (Plug-to-xPonder) |-------|             |    |
    |    |    ...................................|       |             |    |
    |  |------|                                  |       |             |    |
    |  |      |    |-----------------------|     |       | Grey Optics |    |
    |  |Plug A|====|        Photonics      |=====|xPonder|=============|    |
    |  |      |    |-----------------------|     |       |             |    |
    |  |------|                                  |-------|             |    |
    |    |                                                             |    |
    +----+                                                             +----+

~~~
{: #figure-topo5 title="Network topology with symmetric plug and transponder"}

## Topo6 - Other Network scenarios.

* Network topology with shared switched fiber network with regenerators: This is extension of topology Topo-3 {{figure-topo3}} when the photonic network has regenerator.
* Asymmetric interconnect Network topology where the protection open at one end but both protection legs are terminated on separate xPonder or coherent pluggables.
* IP Lag Network topology where the IP link between two packet devices are provided by multiple coherent plugs
* Practical network deployments which includes the mix of many network topologies explained above.

# Operators' Use cases


This section provides a set of packet over optical use cases which are applicable to any network topologies in Section 5.

# Security Considerations


# IANA Considerations

This document has no IANA actions.

--- back

# Acknowledgments

This document has been made with consensus and contributions coming from multiple drafts with different visions.

{:numbered="false"}
