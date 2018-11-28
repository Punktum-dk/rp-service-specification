# DK Hostmaster Registrar Portal Service specification

2018-11-28 Revision 1.00

## Table of Contents

<!-- MarkdownTOC bracket=round levels="1,2,3,4,5" indent="  " -->

- [Introduction](#introduction)
  - [About this Document](#about-this-document)
  - [License](#license)
  - [Document History](#document-history)
  - [The .dk Registry in Brief](#the-dk-registry-in-brief)
- [RP in Brief](#rp-in-brief)
- [RP Service](#rp-service)
  - [SSL/TLS Support](#ssltls-support)
  - [Available Environments](#available-environments)
    - [production](#production)
    - [sandbox](#sandbox)
- [Implementation Requirements](#implementation-requirements)
- [Active Registrar Account](#active-registrar-account)
- [IP Whitelisting](#ip-whitelisting)

<!-- /MarkdownTOC -->

<a id="introduction"></a>
## Introduction

This document describes the registrar self-service portal (RP) offered by DK Hostmaster.

The document is targeted at registrars as audience.

<a id="about-this-document"></a>
### About this Document

This specification describes version 2.X.X of the DK Hostmaster RP service. Future releases will be reflected in updates to this specification, please see the document history section below.

Do note that the specification describes the latest released service. Service version is listed in the Document History, so given changes implemented in the service are reflected in the specification. Do note that a service might be released to the sandbox environment prior to being released to production after a grace period.

Any future additions and changes to the implementation are not within the scope of this document and will not be discussed or mentioned throughout this document.

This document is owned and maintained by DK Hostmaster A/S and must not be distributed without this information.

All examples provided in the document are fabricated or changed from real data to demonstrate commands etc. any resemblance to actual data are coincidental.

<a id="license"></a>
### License

This document is copyright by DK Hostmaster A/S and is licensed under the MIT License, please see the separate LICENSE file for details.

<a id="document-history"></a>
### Document History

1.00 2018-11-28

- Initial revision
- Describes service version 2.3.X

<a id="the-dk-registry-in-brief"></a>
### The .dk Registry in Brief

DK Hostmaster is the registry for the ccTLD for Denmark (dk). The current model used in Denmark is based on a sole registry, with DK Hostmaster maintaining the central DNS registry.

<a id="rp-in-brief"></a>
## RP in Brief

RP is a web based service aimed at registrars and supporting their business and processed towards the DK Hostmaster registry.

<a id="rp-service"></a>
## RP Service

<a id="ssltls-support"></a>
### SSL/TLS Support

The RP service supports the following protocols for transport security:

- TLSv1.2

<a id="available-environments"></a>
### Available Environments

DK Hostmaster offers the following environments for RP:

<a id="production"></a>
#### production

- `https://rp.dk-hostmaster.dk/`

<a id="sandbox"></a>
#### sandbox

- `https://rp-sandbox.dk-hostmaster.dk/`

<a id="implementation-requirements"></a>
## Implementation Requirements

<a id="active-registrar-account"></a>
## Active Registrar Account

Access to the RP service requires an active registrar account, please see the information on [the process for becoming a registrar](https://www.dk-hostmaster.dk/en/become-registrar).

<a id="ip-whitelisting"></a>
## IP Whitelisting

DK Hostmaster requires whitelisting of IPs for access to the RP service.

Additions and removals of IP addresses can be handled by the registrar itself, but initial setup is currently a manual process handled by DK Hostmaster.

Please submit change requests including registrar handle information to:

- tech@dk-hostmaster.dk
