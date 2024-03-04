---
title: "Use cases, Network Scenarios and gap analys for Packet Optical Integration (POI) with coherent plugables under ACTN Framework"
abbrev: "POI coherent pluggables"
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
    ins: O. G. de Dios
    fullname: Oscar Gonzalez de Dios
    org: Telefonica
    email: oscar.gonzalezdedios@telefonica.com

  -
    ins:  J. Bouquier
    name: Jean-Francois Bouquier
    org: Vodafone
    email: jeff.bouquier@vodafone.com

  -
    ins: J. Meuric
    name: Julien Meuric
    org: Orange
    email: julien.meuric@orange.com

  -
    ins: G. Mishra
    name: Gyan Mishra
    org: Verizon
    email: gyan.s.mishra@verizon.com

  -
    ins: G. Galimberti
    fullname: Gabriele Galimberti
    org: Individual
    email: ggalimbe56@gmail.com

contributor:

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
    ins: E. Echeverry
    fullname: Edward Echeverry
    org: Telefonica
    email: edward.echeverry@telefonica.com
  -
    ins: A. Guo
    fullname: Aihua Guo
    org: Futurewei Technologies
    email: aihuaguo.ietf@gmail.com
  -
    name: Brent Foster
    org: Cisco
    street: Research Triangle Park
    city: North Carolina
    country: UNITED STATES OF AMERICA
    email: brfoster@cisco.com

  -
    name: Daniele Ceccarelli
    org: Cisco
    email: daniele.ietf@gmail.com

  -
    ins: I. Busi
    fullname:  Italo Busi
    org: Huawei Technologies
    email: italo.busi@huawei.com

  -
    name: Ori Gerstel
    org: Cisco
    street: AMOT ATRIUM Tower 19th floor
    city: TEL AVIV-YAFO, TA
    country: Israel
    email: ogerstel@cisco.com



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

--- abstract

This document provides general overarching guidelines for control and management of packet over optical converged networks with coherent pluggables and focuses on operators' use cases and network scenarios. It provides a set of use cases which are needed for the control and management of the packet over optical networks which comprise devices with mixes of packet and optical functions where the optical functions may be provided on coherent pluggables. The document provides a gap analysis to solve the use cases.

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

## Scenario A - High capacity point to point connection over dedicated direct fiber

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

As shown in {{figure-topo3}}, this scenario considers a point-to-point optical service over a metro/regional network (e.g., up to 500 km). The metro/regional network contains DWDM filters, amplifiers and optical switching.

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

This scenario, shown in {{figure-topo5}}and extends network topologies {{figure-topo1}} to {{figure-topo3}} and covers a corner case, where one end of an optical service is terminated on a plug and the other end is terminated on a traditional xPonder (transponder or muxponder) with grey optics to a packet device. This scenario is encountered when one of the packet device does not support coherent plugables.

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

This section provides a set of packet over optical general use cases which are applicable to any network topologies in Section 4 and both for multi-layer networks using or not coherent pluggables in the routers. These use cases are presented following current operators’ priorities order.

The use cases a generally applicable for both the traditional packet over optical integration based on grey interfaces in the IP routers and use of transponders/muxponders in the optical domain and for the packet over optical integration considering coherent WDM pluggables in the IP routers over a media channel/Network Media channel in the optical domain. For clarification purposes, the mention ‘valid for both’ has been added in the name of each use case else ‘valid for coherent pluggable’ when the use case is specific to the coherent pluggable approach.

## 1.	End-to-end multi-layer visibility and management (valid for both)

### a.	End-to-end multi-layer network and service topology discovery
Target is to have a full end-to-end multi-layer view from all the layers and their inter-dependencies: service layer (e.g. L3VPN/L2VPN), transport layer (RSVP-TE, SR-TE), IP layer (IGP), Ethernet layer, OTN L1 layer (optional), photonic L0 layer (OCh, OMS, OTS and fibre).
The above discovery includes inventory discovery by each controller and exposure to the MDSC of the required information for a complete end-to-end multi-layer view of the network.

#### Coherent DWDM pluggable insertion in the router linecard port
Once a pluggable module is inserted in the proper linecard port, the host device must recognise the hardware component (ZR+ pluggable module) and expose its attributes and capabilities to the controller. For example, ZR+ modules can share the operational-mode that summarize the most important pluggable characteristics (such as FEC type, modulation format, baud rate, bit rate, etc.). If the hardware component has been successfully recognised, the host device is then ready to create and expose the necessary logical arrangements.

#### Inventory of Coherent DWDM pluggable (‘valid for coherent pluggable’).
The domain controller exposes to the MDSC hardware inventory information of the devices under its supervision. For full router inventory (linecards, ports, etc.) see draft-ietf-ivy-network-inventory-yang. In addition, it has to include the coherent pluggable transceiver capabilities. These include, for instance, operational-modes supported (ITU-T application codes, organizational modes), min/max central-frequency range supported, min/max output power supported, min/max received power supported etc. In case of discovery of any HW mismatch between coherent DWDM pluggable and router linecard port capabilities the controller shall report HW mismatch alarm to MDSC. An example is a linecard multi-rate port vs coherent DWDM pluggable with only one client/line rate (e.g. 1x400GE).

#### Coherent pluggable OTSi service discovery information (‘valid for coherent pluggable’).

Once a router-to-router connection with coherent pluggables has been created over a Network Media Channel in the optical Line system, then it is required to expose the OTSi service. The relevant OTSi information could be nominal-central-frequency, tx-output-power, operational-mode-ID, operational-status, admin-status etc.

#### Discovery of layer relationships

In case the operational mode has already been configured, the host device and the controlller need to create the nececessary arrangements to navigate from the interface where the router traffic is injected up the port connecting to the fiber. That is, the layer hierarchy from L0 to L3 needs to be completed and exposed.


### b.	End-to-end multi-layer event/fault management (valid for both)
The Target is this use case is to have a full end-to-end multi-layer correlation of events at different layers and domains (e.g. operational-status changes reported at OTS/OMS/OCh/ODUk (optional), IP link level, LSP level, L3VPN/L2VPN level etc.) so that final root cause can be quickly identified and fixed (e.g. fibre cut vs coherent DWDM pluggable  failure). This use case is divided in two:
* Correlation of ZR+ connection (OTSi service) operational-status with MC/NMC operational-status (‘valid for coherent pluggable)
In this case, the target is to expose to the MDSC both the events/faults from the ZR+ connection (OTSi service) and ZR+ pluggables as well as for the MC/NMC associated to this ZR+ connection (OTSi service) in the DWDM Line system so that proper correlation can be performed at MDSC level

* Correlation of coherent pluggable operational status, port status, Ethernet link operational status, IP link status


### c.	End-to-end multi-layer performance management (valid for both)
In this use case, the goal is to have the possibility to analyse through performance monitoring of the different layers mentioned above and be able, in case of end-to-end L2VPN/L3VPN service degradation, to identify the root cause of the degradation. For scaling purposes, the target should be, upon service fulfilment phase, to set up the right TCAs associated to each layer that can allow to meet the L2VPN/L3VPN service SLA (e.g. in terms of latency, jitter, BW, etc.). This use case is divided in two:

* Performance management of the ZR+ connection (OTSi service) (‘valid for coherent pluggable)
Target is to have the basic performance parameters of each OTSi service running between two pluggables exposed towards the MDSC. Best for operators could be to defined TCA (Threshold crossing alerts) from MDSC for each OTSI service and be notified only when the Thresholds defined are not met? Operator shall be able to decide which parameters and for which OTSi service. But all the parameters shall be visible if needed by operators.

Note: Router shall provide also all the possible performance counters not only for OTSi service/Ethernet service etc. but also for the pluggable itself

As an example operators should have the ability to get visibility on pre-FEC-BER for a given OTSi service and see the trend before post-FEC-BER is affected

* Performance management of the Ethernet link running over the OTSi service and also of the IP link running over this Ethernet link.

## 2.	Inter-domain link validation (valid for coherent pluggable)
Documenting the patch cord that connects the port of the coherent DWDM pluggable in the routers to the optical node (e.g. to the right Add/Drop filter of the ROADM) is performed. This manual operation is prone to human mistakes. It would be highly beneficial for operators to have a mean to check/discover that the right pluggable has been connected to the desired ROADM port. This use case requires the ability to expose to the MDSC the power levels at coherent DWDM pluggable side and at ROADM port side to perform the right correlation and validation.

## Pluggable to pluggable service Provisioning
The following specific coherent DWDM pluggable provisioning sub-cases are identified:
* Manual Day 1 configuration (‘valid for coherent pluggable)
Knowing the coherent pluggable characteristics (performance and optical impairments for a specific operational-mode-ID) optical planning and validation is performed and following parameters are communicated by optical team to IP team: nominal-central-frequency, tx-output-power, operational-mode-ID so that the coherent pluggables at both ends in the routers can be correctly configured (e.g. through P-PNC) in a manual way. As prerequisite before the coherent pluggable configuration, the optical team has properly configured the MC/NMC in the line system DWDM network through the O-PNC.
*	Semi-manual Day 1 configuration (‘valid for coherent pluggable’)
Same optical planning and validation is performed first by optical team and then parameters are provided to MDSC operations engineer so that they can be set-up at Hierarchical SDN controller level and provisioned by P-PNC in the corresponding router’s pluggables
* Semi-Automated Day 1 configuration with Path Computation API request from MDSC towards O-PNC (‘valid for coherent pluggable’) based on trial and error.
* Fully automated Day 1 configuration (For future discussions)


## 4.	End-to-end L3VPN/L2VPN service multi-layer provisioning with SLA constraints (TE constraints) (valid for both)
This use case is described in {{?I-D.draft-ietf-teas-actn-poi-applicability}} for the SR-TE case which is relevant as target use case for operators. If new connectivity is required between the routers and at optical level then full automation could be achieved. However considering PMO (Present Mode of Operation) in most operators, before an optical path is setup either between two native transponders or between two coherent pluggables in  routers, a detailed optical planning and validation is always required. So, the automation of this use case is considered more for future mode of operations (FMO) and has not the same priority as the previous two use cases.

## 5.	End-to-end L3VPN/L2VPN service multi-layer with SLA constraints (TE constraints) with optical restoration support (valid for both but here focusing on the coherent pluggable)
This use case has not the same priority as the previous ones as protection in multi-layer Core/Backhaul networks is usually implemented at IP layer (e.g. FRR with RSVP-TE, TI-LFA with SR and SR policies in SR-TE) to avoid proven protection races.
a.	ZR+ links over DWDM network can be considered out of the L0 control plane so that no restoration is applied to those links
b.	ZR+ links over DWDM network can be considered part of the L0 control plane but no restoration is enabled for those links
c.	ZR+ links over DWDM network can be considered as part of the L0 control plane with restoration enabled for those links but nominal-central-frequeny is maintained unchanged after L0 restoration. Only output-power could be tuned for the new restored path determined by the L0 control plane
d.	ZR+ links over DWDM network can be considered as part of the L0 control plane with restoration enabled for those links and nominal-central-frequency and output power need to be tuned for the new restored path determined by the L0 control plane.


# Security Considerations

TBD

# IANA Considerations

This document has no IANA actions.

--- back

# Acknowledgments

This document has been made with consensus and contributions coming from multiple drafts with different visions.

{:numbered="false"}
