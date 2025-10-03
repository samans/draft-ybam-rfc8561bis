---
coding: utf-8

title: "A YANG Data Model for Microwave Radio Link"
abbrev: "Microwave Radio Link YANG"
category: std
docname: draft-ybam-rfc8561bis-latest
obsoletes: 8561
ipr:  trust200902
submissiontype: IETF
consensus: true
v: 3
area: Routing
workgroup: CCAMP Working Group
keyword: Internet-Draft
venue:
  group: CCAMP
  type: Working Group
  mail: WG@example.com
  arch: https://example.com/WG
  github: USER/REPO
  latest: https://example.com/LATEST
pi: [toc, sortrefs, symrefs]

author:
 -
    fullname: Scott Mansfield
    organization: Ericsson
    email: scott.mansfield@ericsson.com
 -
    fullname: Jonas Ahlberg
    organization: Ericsson AB
    street: Lindholmspiren 11
    city: Goteborg
    code: 417 56
    country: Sweden
    email: jonas.ahlberg@ericsson.com
 -
    fullname: Min Ye
    organization: Huawei Technologies
    street: No.1899, Xiyuan Avenue
    city: Chengdu
    code: 611731
    country: China
    email: amy.yemin@huawei.com
 -
    fullname: Daniela Spreafico
    organization: Nokia - IT
    street: Via Energy Park, 14
    city: Vimercate (MI)
    code: 20871
    country: Italy
    email: daniela.spreafico@nokia.com
 -
    fullname: Danilo Pala
    organization: SIAE
    email: danilo.pala@saiemic.com

contributor:
 -
    fullname: Italo Busi
    organization: Huawei Technologies
    email: italo.busi@huawei.com
 -
    fullname: Koji Kawada
    organization: NEC Corporation
    street: 1753, Shimonumabe Nakahara-ku
    region: Kawasaki, Kanagawa
    code: 211-8666
    country: Japan
    email: k-kawada@ah.jp.nec.com
 -
    fullname: Carlos J. Bernardos
    organization: Universidad Carlos III de Madrid
    street: Av. Universidad, 30
    city: Leganes, Madrid
    code: 28911
    country: Spain
    email: cjbc@it.uc3m.es
 -
    fullname: Marko Vaupotic
    organization: Aviat Networks
    street: Motnica 9
    city: Trzin-Ljubljana
    code: 1236
    country: Slovenia
    email: Marko.Vaupotic@Aviatnet.com
 -
    fullname: Xi Li
    organization: NEC Laboratories Europe
    street: Kurfursten-Anlage 36
    city: Heidelberg
    code: 69115
    country: Germany
    email: Xi.Li@neclab.eu

normative:
informative:
  IANA-if-type-module:
    title: iana-if-type YANG Module
    author:
      organization: IANA
    date:  January 2023
    target: http://www.iana.or/assignments/iana-if-type
  EN301129:
    title: >
      Transmission and Multiplexing (TM); Digital Radio
      Relay Systems (DRRS); Synchronous Digital Hierarchy (SDH);
      System performance monitoring parameters of SDH DRRS
    author:
      organization: ETSI
    date:  May 1999
    seriesinfo: EN 301 129 V1.1.2
  EN302217-1:
    title: >
      Fixed Radio Systems; Characteristics and
      requirements for point-to-point equipment and antennas;
      Part 1: Overview, common characteristics and system-
      dependent requirements
    author:
      organization: ETSI
    date:  May 2017
    seriesinfo: EN 302 217-1 V3.1.0
  EN302217-2:
    title: >
      Fixed Radio Systems; Characteristics and
      requirements for point to-point equipment and antennas;
      Part 2: Digital systems operating in frequency bands from
      1 GHz to 86 GHz; Harmonised Standard covering the
      essential requirements of article 3.2 of Directive
      2014/53/EU
    author:
      organization: ETSI
    date:  May 2017
    seriesinfo: EN 302 217-2 V3.1.1
  G.808.1:
    title: >
      SERIES G: TRANSMISSION SYSTEMS AND MEDIA, DIGITAL
      SYSTEMS AND NETWORKS; Digital networks ; General aspects
      Generic protection switching ; Linear trail and subnetwork
      protection
    author:
      organization: ITU-T
    date:  May 2014
    seriesinfo: ITU-T Recommendation G.808.1
  G.826:
    title: >
      SERIES G: TRANSMISSION SYSTEMS AND MEDIA, DIGITAL
      SYSTEMS AND NETWORKS; Digital networks - Quality and
      availability targets; End-to-end error performance
      parameters and objectives for international, constant bit-
      rate digital paths and connections
    author:
      organization: ITU-T
    date:  December 2002
    seriesinfo: ITU-T Recommendation G.826
  ONF-model:
    title: Microwave Information Model
    author:
      organization: ONF
    date:  December 2016
    seriesinfo: TR-532, version 1.0
    target: https://www.opennetworking.org/images/stories/downloads/sdn-resources/technical-reports/TR-532-Microwave-Information-Model-V1.pdf
  TR102311:
    title: >
      Fixed Radio Systems; Point-to-point equipment;
      Specific aspects of the spatial frequency reuse method
    author:
      organization: ETSI
    date:  November 2015
    seriesinfo: ETSI TR 102 311 V1.2.1

--- abstract

This document defines a YANG data model for control and management of
radio link interfaces and their connectivity to packet (typically
Ethernet) interfaces in a microwave/millimeter wave node.  The data
nodes for management of the interface protection functionality is
broken out into a separate and generic YANG data model in order to
make it available for other interface types as well. This document obsoletes RFC 8561.

--- middle

# Introduction

This document defines a YANG data model for management and control of
the radio link interface(s) and the relationship to packet (typically
Ethernet) and/or Time-Division Multiplexing (TDM) interfaces in a
microwave/millimeter wave node.  The ETSI EN 302 217 series defines
the characteristics and requirements of microwave/millimeter wave
equipment and antennas.  Specifically, ETSI EN 302 217-2 {{EN302217-2}}
specifies the essential parameters for systems operating from 1.4 GHz
to 86 GHz.  The data model includes configuration and state data
according to the new Network Management Datastore Architecture
{{?RFC8342}}.

The design of the data model follows the framework for management and
control of microwave and millimeter wave interface parameters defined
in {{?RFC8432}}.  This framework identifies the need and the scope of
the YANG data model, use cases, and requirements that the model needs
to support.  Moreover, it provides a detailed gap analysis to
identify the missing parameters and functionalities of the existing
and established models to support the specified use cases and
requirements, and based on that, it recommends how the gaps should be
filled with the development of the new model.  According to the
conclusion of the gap analysis, the structure of the data model is
based on the structure defined in {{!RFC8561}}, and it
augments {{!RFC8343}} to align with the same structure for management of
the packet interfaces.  More specifically, the model will include
interface layering to manage the capacity provided by a radio link
terminal for the associated Ethernet and TDM interfaces, using the
principles for interface layering described in {{!RFC8343}} as a basis.

The data nodes for management of the interface protection
functionality is broken out into a separate and generic YANG data
module in order to make it also available for other interface types.

The designed YANG data model uses established microwave equipment and
radio standards, such as ETSI EN 302 217-2; the IETF Radio Link Model
{{!RFC8561}}; and the ONF Microwave Model {{ONF-model}}, as
the basis for the definition of the detailed leafs/parameters, and it
proposes new ones to cover identified gaps, which are analyzed in
{{?RFC8432}}.

## Terminology and Definitions

The following terms are used in this document:

Carrier Termination (CT) is an interface for the capacity provided
over the air by a single carrier.  It is typically defined by its
transmitting and receiving frequencies.

Radio Link Terminal (RLT) is an interface providing packet capacity
and/or TDM capacity to the associated Ethernet and/or TDM interfaces
in a node and is used for setting up a transport service over a
microwave/millimeter wave link.

The following acronyms are used in this document:

  ACM Adaptive Coding Modulation

  ATPC Automatic Transmitter Power Control

  BBE Background Block Error

  BER Bit Error Ratio

  BPSK Binary Phase-Shift Keying

  CM Coding Modulation

  CT Carrier Termination

  ES Errored Seconds

  IF Intermediate Frequency

  MIMO Multiple Input Multiple Output

  RF Radio Frequency

  RLT Radio Link Terminal

  QAM Quadrature Amplitude Modulation

  QPSK Quadrature Phase-Shift Keying

  RTPC Remote Transmit Power Control

  SES Severely Errored Seconds

  TDM Time-Division Multiplexing

  UAS Unavailable Seconds

  XPIC Cross Polarization Interference Cancellation

## Tree Structure

A simplified graphical representation of the data model is used in
{{tree}} of this document.  The meaning of the symbols in these
diagrams is defined in {{?RFC8340}}.

## Prefixes in Data Node Names
In this document, names of data nodes and other data model objects are prefixed using the standard prefix associated with the corresponding YANG imported modules, as shown in {{tab-prefix}}.

| Prefix   | YANG Module               | Reference
| mrl      | ietf-microwave-radio-link | This document
| yang     | ietf-yang-types           | {{!RFC6991}}
| ianaift  | iana-if-type              | {{IANA-if-type-module}}
| if       | ietf-interfaces           | {{!RFC8343}}
| ifprot   | ietf-interface-protection | This document
| mw-types | ietf-microwave-types      | This document
{: #tab-prefix title="Prefixes for imported YANG modules"}
# Microwave Radio Link YANG Data Model

{: #tree}

## YANG Tree

~~~~ ascii-art
{::include ./trees/ietf-microwave-radio-link.tree}
~~~~
{: artwork-name="ietf-microwave-radio-link.tree"}

## Explanation of the Microwave Data Model

The leafs in the Interface Management Module augmented by RLT and CT
are not always applicable.

"/interfaces/interface/enabled" is not applicable for RLT.  Enable
and disable of an interface is done in the constituent CTs.

The packet-related measurements "in-octets", "in-unicast-pkts",
"in-broadcast-pkts", "in-multicast-pkts", "in-discards", "in-errors",
"in-unknown-protos", "out-octets", "out-unicast-pkts", "out-
broadcast-pkts", "out-multicast-pkts", "out-discards", and "out-
errors" are not within the scope of the microwave radio link domain
and therefore are not applicable for RLT and CT.

# Microwave Radio Link YANG Data Model

This module imports typedefs and modules from {{!RFC6991}}, {{!RFC8343}}
and {{!RFC7224}}, and it references {{TR102311}}, {{EN302217-1}},
{{EN301129}}, and {{G.826}}.

~~~~ yang
{::include ./ietf-microwave-radio-link.yang}
~~~~
{: sourcecode-markers="true" sourcecode-name="ietf-microwave-radio-link@2025-10-03.yang"}

# Interface Protection YANG Data Model

The data nodes for management of the interface protection
functionality is broken out from the Microwave Radio Link Module into
a separate and generic YANG data model in order to make it also
available for other interface types.

This module imports modules from {{!RFC8343}}, and it references
{{G.808.1}}.

~~~~ yang
{::include ./ietf-interface-protection.yang}
~~~~
{: sourcecode-markers="true" sourcecode-name="ietf-interface-protection@2025-10-03.yang"}

# Microwave Types YANG Data Model

This module defines a collection of common data types using the YANG
data modeling language.  These common types are designed to be
imported by other modules defined in the microwave area.

~~~~ yang
{::include ./ietf-microwave-types.yang}
~~~~
{: sourcecode-markers="true" sourcecode-name="ietf-microwave-types@2025-10-03.yang"}

# Security Considerations

The YANG data models specified in this document define schemas for
data that is designed to be accessed via network management protocols
such as NETCONF {{!RFC6241}} or RESTCONF {{!RFC8040}}.  The lowest NETCONF
layer is the secure transport layer, and the mandatory-to-implement
secure transport is Secure Shell (SSH) {{!RFC6242}}.  The lowest
RESTCONF layer is HTTPS, and the mandatory-to-implement secure
transport is TLS {{!RFC8446}}.

The Network Configuration Access Control Model (NACM) {{!RFC8341}}
provides the means to restrict access for particular NETCONF or
RESTCONF users to a preconfigured subset of all available NETCONF or
RESTCONF protocol operations and content.

There are a number of data nodes defined in these YANG data models
that are writable/creatable/deletable (i.e., config true, which is
the default).  These data nodes may be considered sensitive or
vulnerable in some network environments.  Write operations (e.g.,
edit-config) to these data nodes without proper protection can have a
negative effect on network operations.  These are the subtrees and
data nodes and their sensitivity/vulnerability:

Interfaces of type microwaveRadioLinkTerminal:

~~~~
      /if:interfaces/if:interface/mode,
      /if:interfaces/if:interface/carrier-terminations,
      /if:interfaces/if:interface/rlp-groups,
      /if:interfaces/if:interface/xpic-pairs,
      /if:interfaces/if:interface/mimo-groups, and
      /if:interfaces/if:interface/tdm-connections:
~~~~

These data nodes represent the configuration of the radio link
terminal, and they need to match the configuration of the radio link
terminal on the other side of the radio link.  Unauthorized access to
these data nodes could interrupt the ability to forward traffic.

Interfaces of type microwaveCarrierTermination:

~~~~
      /if:interfaces/if:interface/carrier-id,
      /if:interfaces/if:interface/tx-enabled,
      /if:interfaces/if:interface/tx-frequency,
      /if:interfaces/if:interface/rx-frequency,
      /if:interfaces/if:interface/duplex-distance,
      /if:interfaces/if:interface/channel-separation,
      /if:interfaces/if:interface/rtpc/maximum-nominal-power,
      /if:interfaces/if:interface/atpc/maximum-nominal-power,
      /if:interfaces/if:interface/atpc/atpc-lower-threshold,
      /if:interfaces/if:interface/atpc/atpc-upper-threshold,
      /if:interfaces/if:interface/single/selected-cm,
      /if:interfaces/if:interface/adaptive/selected-min-acm,
      /if:interfaces/if:interface/adaptive/selected-max-acm,
      /if:interfaces/if:interface/if-loop, and
      /if:interfaces/if:interface/rf-loop:
~~~~

These data nodes represent the configuration of the carrier
termination, and they need to match the configuration of the carrier
termination on the other side of the carrier.  Unauthorized access to
these data nodes could interrupt the ability to forward traffic.

Radio link protection:

~~~~
      /radio-link-protection-groups/protection-group:
~~~~

This data node represents the configuration of the protection of
carrier terminations.  Unauthorized access to this data node could
interrupt the ability to forward traffic or remove the ability to
perform a necessary protection switch.

XPIC:

~~~~
      /xpic-pairs:
~~~~

This data node represents the XPIC configuration of a pair of
carriers.  Unauthorized access to this data node could interrupt the
ability to forward traffic.

MIMO:

~~~~
      /mimo-groups:
~~~~

This data node represents the MIMO configuration of multiple
carriers.  Unauthorized access to this data node could interrupt the
ability to forward traffic.

Some of the RPC operations in this YANG data model may be considered
sensitive or vulnerable in some network environments.  It is thus
important to control access to these operations.  These are the
operations and their sensitivity/vulnerability:

Radio link protection:

~~~~
  /radio-link-protection-groups/protection-group/
                                          manual-switch-working,
  /radio-link-protection-groups/protection-group/
                                          manual-switch-protection,
  /radio-link-protection-groups/protection-group/forced-switch,
  /radio-link-protection-groups/protection-group/
                                          lockout-of-protection,
  /radio-link-protection-groups/protection-group/freeze,
  /radio-link-protection-groups/protection-group/exercise, and
  /radio-link-protection-groups/protection-group/clear
~~~~

These data nodes represent actions that might have an impact on the
configuration of the protection of carrier terminations.
Unauthorized access to these data nodes could interrupt the ability
to forward traffic or remove the ability to perform a necessary
protection switch.

The security considerations of {{!RFC8343}} also apply to this document.

# IANA Considerations

No IANA Considerations in this update.

--- back

{: #changes-bis}

# Changes from RFC 8561

To be added in a future revision of this draft.

# Example: 1+0 and 2+0 Configuration Instances

   This section gives simple examples of 1+0 and 2+0 instances using the
   YANG data model defined in this document.  The examples are not
   intended as a complete module for 1+0 and 2+0 configuration.

## 1+0 Instance

~~~~ ascii-art
{::include ./figures/1+0-example.txt}
~~~~
{: #fig-1-plus-0-example title="1+0 Example"
artwork-name="1+0-example.txt"}

{{fig-1-plus-0-example}} shows a 1+0 example.  The following instance shows the 1+0 configuration of the Near End node.

~~~~ ascii-art
{::include ./json/1+0-example.json}
~~~~
{: artwork-name="1+0-example.json"}


## 2+0 Instance

{{fig-2-plus-0-example}} shows a 2+0 example.

~~~~ ascii-art
{::include ./figures/2+0-example.txt}
~~~~
{: #fig-2-plus-0-example title="2+0 Example"
artwork-name="2+0-example.txt"}

The following instance shows the 2+0 configuration of the Near End
node.

~~~~ ascii-art
{::include ./json/2+0-example.json}
~~~~
{: artwork-name="2+0-example.json"}

## 2+0 XPIC Instance

The following instance shows the XPIC configuration of the Near End
node.

~~~~ ascii-art
{::include ./json/2+0-xpic-example.json}
~~~~
{: artwork-name="2+0-xpic-example.json"}
~~~~

# Acknowledgments
   This document was prepared using the kramdown RFC tool written and maintained by Carsten Bormann. Thanks to Martin Thomson for the github integration of the kramdown RFC tool and for the aasvg tool which is used for the ascii to SVG conversion.
