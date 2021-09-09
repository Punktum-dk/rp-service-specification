![DK Hostmaster Logo][DKHMLOGO]

# DK Hostmaster Registrar Portal Service specification

![Markdownlint Action][GHAMKDBADGE]
![Spellcheck Action][GHASPLLBADGE]

2.0 2021-05-13
Revision 2.0

## Table of Contents

<!-- MarkdownTOC bracket=round levels="1,2,3,4,5" indent="  " autolink="true" autoanchor="true" -->

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
- [Features](#features)
  - [Account](#account)
    - [Registrar Account Group](#registrar-account-group)
    - [Meta-Roles](#meta-roles)
    - [Linked WHOIS Handles](#linked-whois-handles)
      - [Link WHOIS Handle](#link-whois-handle)
      - [Create WHOIS Handles](#create-whois-handle)
      - [Merge WHOIS Handles](#mergewhois-handles)
      - [Unlinked WHOIS Handles](#unlink-whois-handle)
    - [Set Management Model Default](#set-management-model-default)
    - [Set Renewal Policy Default](#set-renewal-policy-default)
  - [DNSSEC](#dnssec)
    - [Manage DNSSEC](#manage-dnssec)
  - [Domain Name](#domain-name)
    - [Domain Name Application](#domain-name-application)
      - [Management Choice](#management-choice)
      - [Waiting List](#waiting-list)
  - [Name Server](#name-server)
    - [Name Server Application](#name-server-application)
  - [Prepaid](#prepaid)
- [References](#references)
- [Resources](#resources)
  - [Mailing list](#mailing-list)
  - [Issue Reporting](#issue-reporting)
- [Appendices](#appendices)

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

2.0 2021-05-13

- Describes service version 3.X.X
- Added new section on features, the initial features described are:
  - [Registrar Account Group](#registrar-account-group)
  - [Meta-Roles](#meta-roles)
  - [Linked WHOIS Handles](#linked-whois-handles)
  - [Manage DNSSEC](#manage-dnssec)
  - [Domain Application](#domain-application)
  - [Name Server Application](#name-server-application)

1.0 2018-11-28

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

DK Hostmaster offers the following two environments:

- production
- sandbox

Updates to both environments are announced via the tech-announce mailing list.

Please see the [information page][DKHMMAIL] for details on subscribing etc.

<a id="production"></a>
#### production

- `https://rp.dk-hostmaster.dk/`

<a id="sandbox"></a>
#### sandbox

- `https://rp-sandbox.dk-hostmaster.dk/`

<a id="implementation-requirements"></a>
## Implementation Requirements

<a id="active-registrar-account"></a>
### Active Registrar Account

Access to the RP service requires an active registrar account, please see the information on [the process for becoming a registrar][DKHMBEREG].

<a id="ip-whitelisting"></a>
## IP Whitelisting

DK Hostmaster requires whitelisting of IPs for access to the RP service.

Additions and removals of IP addresses can be handled by the registrar itself, but initial setup is currently a manual process handled by DK Hostmaster.

Please submit change requests including registrar handle information to:

- tech@dk-hostmaster.dk

<a id="features"></a>
## Features

<a id="account"></a>
### Account

This section describes the registrar account. The term account is used in general sense and does not describe the financial account exclusively unless specified.

<a id="registrar-account-group"></a>
#### Registrar Account Group

The registrar account group is representing the registrar account and consist initially of:

- A registrar handle, representing the account, not used as an operational account
- An administrative account

Additional accounts can be added for specific and general purpose, such as:

- Domain administration
- Domain registration
- Billing and finance administration
- Name server administration
- Registrar account administration

The accounts are all represented towards the system using an email.

<a id="meta-roles"></a>
#### Meta-Roles

The WHOIS system within the DK Hostmaster registry is based on a set of roles (WHOIS roles), used to resolve privileges and permissions.

For domain names these roles are:

- Registrant contact
- Admin/proxy contact
- Billing contact
- Registrar contact
- VID contact

For name servers:

- Name server administrator

The inhabitants of the roles are identified by a handle, generated and issued by the registry.

Registrar portal users created for the [Registrar Account Group](#registrar-account-group) can be assigned meta-roles, which give the specific registrar portal user access to certain features.

The meta-roles are mapped to the WHOIS roles.

| WHOIS Role                | Meta-role                 | Note |
|:-------------------------:|:-------------------------:|--------------------------------------------------------------------------------------|
| Registrant                | *Registrant*              | This role planned deprecated with the introduction of the registrar management model |
| Admin/Proxy               | Proxy                     |                                                                                      |
| Billing                   | Payer                     |                                                                                      |
| *Registrar*               |                           | This role is an indication of the registrar account administering the domain name    |
|                           | *Registrar*               | This role allows for registration of domain names                                    |
| Name Server Administrator | Name server manager       |                                                                                      |
| *VID contact*             |                           | This role is not available in the registrar portal                                   |

<a id="linked_whois_handles"></a>
### Linked WHOIS Handles

The feature is available in the tab: `Administration`, in the section: `Register account`, under the menu point: `Linked WHOIS handles`.

The features offers the following:

- List WHOIS handles linked to the account. Here you should be able to see the registrar account by default
- Link a WHOIS handle
- Create a WHOIS handle
- Unlink a WHOIS handle
- See details/settings per linked WHOIS handle, currently this is limited to associated e-mail addresses

<a id="link_whois_handle"></a>
#### Link WHOIS Handle

When using the feature to link WHOIS handles, meaning they are associated with a registrar account, a list of candidates are presented.

The requirements for linking are strict and if a certain WHOIS handle does not appear in the list, it might be due to data not matching the registrar account.

When linking a WHOIS handle to a registrar account, it is no longer possible to log in to the self-service portal (SB) using this handle. Unlinking has the opposite effect and unlinked WHOIS handles have to use the self-service portal (SB).

<a id="create_whois_handle"></a>
#### Create WHOIS Handle

A new handle will be created with the same data as the registrar account and it will be automatically linked to the registrar account. You can of course unlink the WHOIS handle from the account.

<a id="merge_whois_handles"></a>
#### Merge WHOIS Handles

Merging handles, is the ability to collapse several handles into one.

This can be useful if you have more than one billing contact, name server administrator or something and you want to collect all they activities on a single handle for easier administration.

<a id="unlink_whois_handle"></a>
#### Unlink WHOIS Handle

When unlinking a WHOIS handle from a registrar account, it is no longer possible to administer the assets associated with this handle via the registrar portal (RP) as portal users. Linking has the opposite effect.

Unlinked WHOIS handles have to use the self-service portal (SB) and are no longer formally associated with the registrar account.

<a id="set-management-model-default"></a>
### Set Management Model Default

The default for the registrar account can be specified in the Registrar Portal.

The feature requires that the portal-user has the meta-role: `Administrator` to set the default, please see: [Meta-Roles](#meta-roles) for more details.

<a id="set-renewal-policy-default"></a>
### Set Renewal Policy Default

The default renewal policy for the registrar account can be specified in the Registrar Portal.

The feature requires that the portal-user has the meta-role: `Administrator` to set the default, please see: [Meta-Roles](#meta-roles) for more details.

Two options are available:

- Auto-renewal
- Auto-expire

The value unless changed by the registrar is `Auto-renewal`, since this was the setting prior to the introduction the option of changing it.

Auto-renewal mean that upon expiration the domain name, if active, will be automatically renewed and the price will be deducted from the registrar account and the specified period will extend the lifespan of the domain name and the updated expiry date will reflect this.

Auto-expire does the opposite of auto-renewal, when the expiration date is due, the domain name will be suspended and will no longer be active.

<a id="dnssec"></a>
## DNSSEC

<a id="manage-dnssec"></a>
### Manage DNSSEC

The feature is available in the tab: `WHOIS search`, in the section: `Name server operations`.

If this section is not available, it is due to that no WHOIS-handles has been associated with the registrar account, which act as name server administrators.

<a id="domain-name"></a>
### Domain

This section describes the processes and features related to domain names.

<a id="domain-name-application"></a>
### Domain Application

The feature is available in the tab: `WHOIS search`, in the section: `Register domain name`.

The feature requires that the portal-user has the meta-role: `Registrar`, please see: [Meta-Roles](#meta-roles) for more details.

As described in the ["Implementation guide for registration of .dk"][IMPLGUIDE] there are two methods for registration of domain names.

1. Method 1: Requires that the accept of terms and conditions is done at the registrar and this is communicated via the application
1. Method 2: Requires that the accept of terms and conditions is done at the registry (with DK Hostmaster)

The application for allows for specification of a timestamp in the field: `Date & time`, in the section `DK Hostmaster's agreement accepted`

The entered date has to match the date and time when the registrant accepted the presented terms and conditions.

The fields available in the application form are the following:

| Field                | Note                 |
|:--------------------:|:---------------------|
| Registrar | This is pre-filled with the registrar account handle and cannot be changed, it does not influence the management model directly, it only to handle the application process |
| Reference | This is a registrar reference with can be used to identify and track an application |
| Domain name | This is the domain name to be applied for |
| Authorization code | This is an optional authorization code is for registering domain names offered for a waiting list position. Please see the details on [waiting list](#waiting-list) handling below
| Registration period | This is the period of the subscription from 1-10 years |
| Management | Choice of management model, either: `Registrar Management` or `Registrant Management`. Please see details below on [Management Choice](#mangement-choice) |
| Renewal | Choice of renewal policy, either: `Auto-renewal` or `Auto-expire`, Please see section on [Prepaid](#prepaid) |
| PO no. | This is an optional end-customer purchase order number with can be used to identify and track an order |
| Account code | This is an optional end-customer reference number with can be used to identify and track an order |
| Registrant handle | This is the mandatory handle of the designated registrant. Please see details below on [Management Choice](#mangement-choice) |
| Proxy handle | This is the optional handle of the designated proxy contact. Please see details below on [Management Choice](#mangement-choice) |
| Payer handle | This is the optional handle of the designated billing contact. Please see details below on [Management Choice](#mangement-choice) |
| Name servers | These are the mandatory name servers. At least two have to be specified and 7 as a maximum. |
| DK Hostmaster's agreement accepted | This is for manually entering the timestamp for an end-user agreement to the Terms and Condition of DK Hostmaster |

<a id="management-choice"></a>
#### Management Choice

When registering a domain name, the registrar has to decide between one of the two offered management methods:

- `Registrar management`
- `Registrant management`

The registrar management model extends the control of the registered domain name. Application wise, it has the following implications:

- The `Proxy` handle will not used and will implicitly be the registrar applying for the domain name
- The `Payer` handle (billing contact) will not be used and will implicitly be the registrar applying for the domain name

The specified `Registrant` will have to be under the same management choice as the domain name. It is not possible to register a domain name for registrar management with a registrar managed user and vice-versa.

<a id="waiting-list"></a>
#### Waiting

DK Hostmaster offers [a waiting list service][WAITLIST], where end-users can sign up for a waiting list position for a given domain name of their interest.

When a domain name is deleted, potential waiting list positions are evaluated and the domain name in question is offered to the first position.

The offering process, starts by an email to the waiting list owner. The waiting list owner has 14 days to accept the offered domain name.

If the offer is accepted the user can take a unique token associated with the offering to a registrar and register the domain name.

If the domain name is going to be registered under registrant management, to the handle of the waiting list owner, the token is not required to authorize the operation.

If the domain name is going to be registrar managed or registered to another handle, the token is required to authorize the application.

<a id="name-server"></a>

### Name Server

This section describes the processes and features related to name servers.

<a id="name-server-application"></a>

#### Name Server Application

The feature is available in the tab: `WHOIS search`, in the section: `Name server operations`.

If this section is not available, it is possibly due to that no WHOIS-handles has been associated with the registrar account, which act as name server administrators.

In order to associate any name server administrators with the registrar account, please use the feature [Link WHOIS handles](#link_whois_handles).

<a id="prepaid"></a>

### Prepaid

<a id="references></a>

## References

List of references used in this document in alphabetical order.

1. [DK Hostmaster: Become a registrar][DKHMBEREG]
1. [DK Hostmaster: Implementation guide for registration of .dk][IMPLGUIDE]
1. [DK Hostmaster: Sandbox Environment Specification][DKHMSANDBOX]
1. [DK Hostmaster: EPP Service Specification][DKHMEPP]

<a id="resources></a>

## Resources

A list of resources for DK Hostmaster Registrar Portal service support is located below.

<a id="mailing-list"></a>

### Mailing list

DK Hostmaster operates a mailing list for discussion and inquiries  about the DK Hostmaster EPP implementation. To subscribe to this list, write to the address below and follow the instructions. Please note that the list is for technical discussion only, any issues beyond the technical scope will not be responded to, please send these to the contact issue reporting address below and they will be passed on to the appropriate entities within DK Hostmaster.

- tech-discuss+subscribe@liste.dk-hostmaster.dk

<a id="issue-reporting"></a>

### Issue Reporting

For issue reporting related to this specification, the RP implementation or test, sandbox or production environments, please contact us. You are of course welcome to post these to the mailing list mentioned above, otherwise use the regular support channels.

<a id="appendices"></a>

## Appendices

### Feature and Meta-role Matrix

| Feature                | Meta-role                 |
|:----------------------:|:-------------------------:|
| Create portal user | Administrator |
| Enable/Disable portal user | Administrator |
| Edit portal user | Administrator |
| Delete portal user | Administrator |
| Create service user | Administrator |
| Enable/Disable service user | Administrator |
| Edit service user | Administrator |
| Delete service user | Administrator |
| Link/Unlink WHOIS handles | Administrator |
| Merge WHOIS handles | Administrator |
| Create Registrar account WHOIS handles | Administrator |
| Apply/Create domain name | Registrar |
| Transfer domain name | Registrar |
| Add funds | Billing |

[DKHMLOGO]: https://www.dk-hostmaster.dk/sites/default/files/dk-logo_0.png
[GHAMKDBADGE]: https://github.com/DK-Hostmaster/rp-service-specification/workflows/Markdownlint%20Action/badge.svg
[GHASPLLBADGE]: https://github.com/DK-Hostmaster/rp-service-specification/workflows/Spellcheck%20Action/badge.svg
[IMPLGUIDE]: https://www.dk-hostmaster.dk/en/implementation-guide-registration-dk
[WAITLIST]: https://www.dk-hostmaster.dk/en/waiting-list
[DKHMMAIL]: https://www.dk-hostmaster.dk/en/mailing-lists
[DKHMBEREG]: https://www.dk-hostmaster.dk/en/become-registrar
[DKHMSANDBOX]: https://github.com/DK-Hostmaster/sandbox-environment-specification
[DKHMEPP]: https://github.com/DK-Hostmaster/epp-service-specification
