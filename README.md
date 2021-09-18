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
    - [Portal Users](#portal-users)
      - [Create Portal User](#create-portal-user)
      - [Enable or Disable Portal User](#enable-or-disable-portal-user)
      - [Edit Portal User](#edit-portal-user)
      - [Delete Portal User](#delete-portal-user)
    - [Service Users](#Service-users)
      - [Create Service User](#create-service-user)
      - [Enable or Disable Service User](#enable-or-disable-service-user)
      - [Edit Service User](#edit-service-user)
      - [Delete Service User](#delete-service-user)
    - [Linked WHOIS Handles](#linked-whois-handles)
      - [Link WHOIS Handle](#link-whois-handle)
      - [Create WHOIS Registrar Account Handle](#create-whois-handle)
      - [Merge WHOIS Handles](#mergewhois-handles)
      - [Unlink WHOIS Handle](#unlink-whois-handle)
    - [Set Management Model Default](#set-management-model-default)
    - [Set Renewal Policy Default](#set-renewal-policy-default)
  - [DNSSEC](#dnssec)
    - [Manage DNSSEC](#manage-dnssec)
  - [Domain Name](#domain-name)
    - [Domain Name Application](#domain-name-application)
      - [Management Choice](#management-choice)
      - [Waiting List](#waiting-list)
    - [Restore Domain Name](#restore-domain-name)
    - [Set auto-expire/renewal for domain name](#set-auto-expirerenewal-for-domain-name)
    - [Cancel/Delete Domain Name](#cancel-domain-name)
    - [Transfer Domain Name](#transfer-domain-name)
    - [Change Name Servers for Domain Name](#change-name-servers-for-domain-name)
    - [Change Registrant for Domain Name](#change-registrant-for-domain-name)
    - [Renew Domain Name](#renew-domain-name)
  - [Name Server](#name-server)
    - [Name Server Application](#name-server-application)
  - [Prepaid](#prepaid)
    - [Add funds to registrar account](#add-funds-to-registrar-account)
- [References](#references)
- [Resources](#resources)
  - [Mailing list](#mailing-list)
  - [Issue Reporting](#issue-reporting)
- [Appendices](#appendices)
  - [Feature and meta-role Matrix](#feature-and-meta-role-matrix)

<!-- /MarkdownTOC -->

<a id="introduction"></a>

## Introduction

This document describes the registrar self-service portal (RP) offered by DK Hostmaster.

The document is targeted at registrars as audience.

<a id="about-this-document"></a>

### About this Document

This specification describes version 2.X.X of the DK Hostmaster RP service. Future releases will be reflected in updates to this specification, please see the document history section below.

Screenshots for depicting features can be seen bu clicking the :eye_speech_bubble: icon. In the documentation the English versions are linked and used, equivalent versions in Danish are available in the screenshots directory of this repository, see also: [References](#references).

Do note that the specification describes the latest released service. Service version is listed in the Document History, so given changes implemented in the service are reflected in the specification. Do note that a service might be released to the sandbox environment prior to being released to production after a grace period.

Any future additions and changes to the implementation are not within the scope of this document and will not be discussed or mentioned throughout this document.

This document is owned and maintained by DK Hostmaster A/S and must not be distributed without this information.

All examples provided in the document are fabricated or changed from real data to demonstrate commands etc. any resemblance to actual data are coincidental.

This document is not the authoritative source for business and policy rules and possible discrepancies between this an any authoritative sources are regarded as errors in this document. This document is aimed at being the external technical specification and describes the implementation facing the users and is an interpretation of authoritative sources and can therefor be erroneous.

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

Please submit change requests including registrar handle information to via the regular support channels.

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

- Domain administration (the proxy meta-role)
- Domain registration (the registrar meta-role)
- Billing and finance administration (the payer meta-role)
- Name server administration (the name server administrator meta-role)
- Registrar account administration (the administrator meta-role)

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
| *Registrar*               | N/A                       | This role is an indication of the registrar account administering the domain name    |
|                           | *Registrar*               | This role allows for registration of domain names                                    |
| Name Server Administrator | Name Server Administrator |                                                                                      |
| *VID contact*             | N/A                       | This role is not available in the registrar portal                                   |
| N/A                       | Administrator             | This role is not available as a WHOIS role                                           |

<a id="portal-users"></a>

#### Portal Users

<a id="create-portal-user"></a>

##### Create Portal User

Portal users are intended for human users, for accounts for machine to machine interfaces: like EPP, DAS and DSU please use a [service user](#service-users).

Areas of responsibility can be controlled and divided using meta-roles.

The available meta-roles are:

- Proxy
- Registrar
- Payer
- Name Server Administrator
- Administrator

<a id="enable-or-disable-portal-user"></a>

##### Enable or Disable Portal User

<a id="edit-portal-user"></a>

##### Edit Portal User

<a id="delete-portal-user"></a>

##### Delete Portal User

If a portal user is not longer in use it can be deleted. Disabling the user is also an option.

<a id="service-users"></a>

#### Service Users

Service users are intended for machine to machine interfaces and currently the following types are available:

- DAS, for more information on the DAS service, please see the [DAS Service Specification][DKHMDAS]
- DSU, for more information on the DAS service, please see the [DSU Service Specification][DKHMDSU]
- EPP, for more information on the DAS service, please see the [EPP Service Specification][DKHMEPP]

A user is created for a specific service and it cannot be used for other services.

It is possible to use more than one service user at a time, which makes sense with service users for specific uses. This can be controlled by setting the relevant [Meta-Roles](#meta-roles).

The available meta-roles are:

- Proxy
- Registrar
- Payer
- Name Server Administrator

Creating a single account with all the meta-roles, the model is however flexible so you can specify all the service users you need to represent your own systems.

For example, if you have one system for domain registration and management, including DNSSEC and name servers, but another system for renewals.

1. Create a service user representing the administrative system and assign it the: `Proxy`, `Registrar` and `Name Server Administrator` meta-roles

1. Create a service user representing the billing system and assign it the `Payer` meta-role

This also holds the benefit of the credentials not having to be shared between the systems, because the service users are separate entities.

<a id="create-service-user"></a>

##### Create Service User

Service users are intended for machine to machine interaction, for accounts for people please use a [portal user](#portal-users).

<a id="enable-or-disable-service-user"></a>

##### Enable or Disable Service User

<a id="edit-service-user"></a>

##### Edit Service User

<a id="delete-service-user"></a>

##### Delete Service User

If a service user is not longer in use it can be deleted. Disabling the user is also an option.

<a id="linked_whois_handles"></a>

#### Linked WHOIS Handles

The feature is available in the tab: `Administration`, in the section: `Register account`, under the menu point: `Linked WHOIS handles`.

The features offers the following:

- List WHOIS handles linked to the account. Here you should be able to see the registrar account by default
- Link a WHOIS handle
- Create a WHOIS handle
- Unlink a WHOIS handle
- See details/settings per linked WHOIS handle, currently this is limited to associated e-mail addresses

<a id="link_whois_handle"></a>

##### Link WHOIS Handle

When using the feature to link WHOIS handles, meaning they are associated with a registrar account, a list of candidates are presented.

The requirements for linking are strict and if a certain WHOIS handle does not appear in the list, it might be due to data not matching the registrar account data.

:warning: When linking a WHOIS handle to a registrar account, it is no longer possible to log in to the self-service portal (SB) using this handle. Unlinking has the opposite effect and unlinked WHOIS handles have to use the self-service portal (SB).

<a id="create_whois_registrar_account_handle"></a>

##### Create WHOIS Registrar Account Handle

A new handle will be created with the same data as the registrar account and it will be automatically linked to the registrar account. You can of course [unlink the WHOIS handle](#unlink_whois_handle") from the account.

Creating WHOIS handles for end-users, is done using a another feature.

<a id="merge_whois_handles"></a>

##### Merge WHOIS Handles

Merging handles, is the ability to collapse several handles into one.

This can be useful if you have more than one billing contact, name server administrator or something and you want to collect all they activities on a single handle for easier administration.

<a id="unlink_whois_handle"></a>

##### Unlink WHOIS Handle

When unlinking a WHOIS handle from a registrar account, it is no longer possible to administer the assets associated with this handle via the registrar portal (RP) as portal users. Linking has the opposite effect.

Unlinked WHOIS handles have to use the self-service portal (SB) and are no longer formally associated with the registrar account.

<a id="set-management-model-default"></a>

#### Set Management Model Default

The default for the registrar account can be specified in the Registrar Portal.

The feature requires that the portal-user has the meta-role: `Administrator` to set the default, please see: [Meta-Roles](#meta-roles) for more details.

1. Log in to the Registrar Portal
1. Click on the "ADMINISTRATION" tab, if is not already displaying
1. Click "Contact information" on the administration tab under "Registrar account" [:eye_speech_bubble:](screenshots/RP-ADMINISTRATION.png)
1. Locate the ""Registration settings" section [:eye_speech_bubble:](screenshots/RP-CONTACT_INFORMATION.png)
1. Set default/account settings for your registrar account for: [:eye_speech_bubble:](screenshots/RP-REGISTRATION_SETTINGS.png)
    a. "Domain name management"
    b. "Domain name renewal"
1. Click "SAVE"

The changes are set instantly and will apply to:

- Domain name registrations
- Contact creations
- Transfers of domain names

Done after the setting has been changed.

<a id="set-renewal-policy-default"></a>

#### Set Renewal Policy Default

The default renewal policy for the registrar account can be specified in the Registrar Portal.

The feature requires that the portal-user has the meta-role: `Administrator` to set the default, please see: [Meta-Roles](#meta-roles) for more details.

Two options are available:

- Auto-renewal
- Auto-expire

The value unless changed by the registrar is auto-renewal, since this was the only available option prior to the introduction auto-expire.

Auto-renewal mean that upon expiration the domain name, if active, will be automatically renewed and the price will be deducted from the registrar account and the specified period will extend the lifespan of the domain name and the updated expiry date will reflect this.

Auto-expire does the opposite of auto-renewal, when the expiration date is due, the domain name will be suspended and will no longer be active.

Getting the suspension lifted requires a [restore domain operation](#restore-domain).

<a id="dnssec"></a>

### DNSSEC

<a id="manage-dnssec"></a>

#### Manage DNSSEC

The feature is available in the tab: `WHOIS search`, in the section: `Name server operations`.

If this section is not available, it is due to that no WHOIS-handles has been associated with the registrar account, which act as name server administrators.

As a name server administrator you can add and remove DSRECORDs to and from a domain name linked to your name servers.

<a id="domain-name"></a>

### Domain

This section describes the processes and features related to domain names.

<a id="domain-name-application"></a>

#### Domain Application

The feature is available in the tab: `WHOIS search`, in the section: `Register domain name`.

The feature requires that the portal-user has the meta-role: `Registrar`, please see: [Meta-Roles](#meta-roles) for more details.

As described in the ["Implementation guide for registration of .dk"][IMPLGUIDE] there are two methods for registration of domain names.

1. Method 1: Requires that the accept of terms and conditions is done at the registrar and this is communicated via the application
1. Method 2: Requires that the accept of terms and conditions is done at the registry (with DK Hostmaster)

The application for allows for specification of a timestamp in the field: `Date & time`, in the section `DK Hostmaster's agreement accepted`

The entered date has to match the date and time when the registrant accepted the presented terms and conditions.

The fields available in the application form are the following:

| Field                | Note                 |
|:---------------------|:---------------------|
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

##### Management Choice

When registering a domain name, the registrar has to decide between one of the two offered management methods:

- `Registrar management`
- `Registrant management`

The registrar management model extends the control of the registered domain name. Application wise, it has the following implications:

- The `Proxy` handle will not used and will implicitly be the registrar applying for the domain name
- The `Payer` handle (billing contact) will not be used and will implicitly be the registrar applying for the domain name

The specified `Registrant` will have to be under the same management choice as the domain name. It is not possible to register a domain name for registrar management with a registrar managed user and vice-versa.

<a id="waiting-list"></a>

##### Waiting List

DK Hostmaster offers [a waiting list service][WAITLIST], where end-users can sign up for a waiting list position for a given domain name of their interest.

When a domain name is deleted, potential waiting list positions are evaluated and the domain name in question is offered to the first position.

The offering process, starts by an email to the waiting list owner. The waiting list owner has 14 days to accept the offered domain name.

If the offer is accepted the user can take a unique token associated with the offering to a registrar and register the domain name.

If the domain name is going to be registered under registrant management, to the handle of the waiting list owner, the token is not required to authorize the operation.

If the domain name is going to be registrar managed or registered to another handle, the token is required to authorize the application.

<a id="restore-domain"></a>

#### Restore Domain

The restore domain feature can be used to restore domain names, which have been suspended, during the redemption period of 30 days. The suspension can be one of:

- When a domain name is suspended due to manual cancellation. See [Cancel domain name](#cancel-domain-name)
- When a domain name has exceeded its expiry date and it is set to auto-expire. See [Set auto-expire/renewal for domain name](#set-auto-expirerenewal-for-domain-name)

The operation will change the registrar account:

- A period fee for one year
- A restoration fee

See current prices at the DK Hostmaster website: [Products and Prices][DKHMPRICES]. Insufficient funds in the registrar account will not prohibit this operation.

<a id="set-auto-expirerenewal-for-domain-name"></a>

#### Set auto-expire/renewal for a domain name

The default setting for auto-expire and auto-renewal can be controlled on an account level and is set when a domain name is created.

It can also be set for a single domain name.

This can be done up to the expiration date of the specific domain name.

<a id="cancel-domain-name"></a>

#### Cancel Domain Name

A domain name can be cancelled manually if it is eligible for cancellation.

A manual cancellation cannot be performed on a domain name, which acts as superordinate for one or more name servers, which have delegated domain names.

An automatic cancellation however will be completed.

- Either due to automatic expiration
- Or by DK Hostmaster

In these situations, the subordinate name servers are not deleted, they are marked for deletion.

The domain names delegated to these name servers, might stop responding based on the way they are set up and a change of name servers will be required to get these working again. For the superordinate, the domain name matching the name servers, a restore operation would be required.

The domain name might might become available for registration upon deletion after the 30 day redemption period. It will not be possible to register or take over the name servers marked for deletion. They can only be recreated after successful deletion by the registry.

<a id="transfer-domain-name"></a>

#### Transfer Domain Name

The feature requires that the portal-user has the meta-role: `Registrar`, please see: [Meta-Roles](#meta-roles) for more details.

<a id="change-name-servers-for-domain-name"></a>

#### Change Name Servers for Domain Name

<a id="change-registrant-for-domain-name"></a>

The feature requires that the portal-user has the meta-role: `Name Server Administrator`, please see: [Meta-Roles](#meta-roles) for more details.

#### Change Registrant for Domain Name

Change of registrant is only possible for a registrar for a registrar managed domain name.

1. The domain name has to be eligible for the transfer
1. The transfer can only take place within the registrars own portfolio, so it is not possible to do this operation across portfolios. Meaning that the existing registrant and designated registrant both have to be created as uses in the registrars portfolio

Due to the registry requirements for ID-control and agreements to the registry terms and conditions the process might be asynchronous depending on the circumstances of the operation.

- If the request is accompanied by a order confirmation token, this is not requested by the registry
- If the designated registrant already has completed ID-control successfully or is not required to do so

The request will be instant and the change registrant fee will be deducted from the registrar account upon success

- If the request is not accompanied by an order confirmation token, an accept of the DK Hostmaster's terms and conditions by the registrant, will be requested by the registrar. This request is valid for 14 days

- If the designated registrant is required to complete ID-control, the registry will, as for accept of terms and conditions, contact the user directly are request the ID-control. The request expires after 14 days

The registrar is notified on all steps of the above process:

- Upon request for accept of terms and conditions
- Upon request for ID-control
- Upon expiration of request for accept of terms and conditions
- Upon expiration of request for ID-control
- Upon rejection of ID-control
- Success of operation

As for the immediate successful execution, the delayed process the change registrant fee will be deducted from the registrar account upon success.

See current prices at the DK Hostmaster website: [Products and Prices][DKHMPRICES]. Insufficient funds in the registrar account will not prohibit this operation.

<a id="renew-domain-name"></a>

#### Renew Domain Name

The feature requires that the portal-user has the meta-role: `Payer`, please see: [Meta-Roles](#meta-roles) for more details.

Domain name subscriptions can be renewed manually via the registrar portal. The feature applies to both:

- Registrant managed domain names, where the registrar is appointed as the billing contact
- Registrar managed domain names

This can be done up to the expiration date of the specific domain name. It does not influence auto-renew or auto-expiration apart from delaying there effective execution and automatic change to the domain name lifespan.

See current prices at the DK Hostmaster website: [Products and Prices][DKHMPRICES]. Insufficient funds in the registrar account will not prohibit this operation.

<a id="name-server"></a>

The feature requires that the portal-user has the meta-role: `Name Server Administrator`, please see: [Meta-Roles](#meta-roles) for more details.

### Name Server

This section describes the processes and features related to name servers.

<a id="name-server-application"></a>

#### Name Server Application

The feature is available in the tab: `WHOIS search`, in the section: `Name server operations`.

If this section is not available, it is possibly due to that no WHOIS-handles has been associated with the registrar account, which act as name server administrators.

In order to associate any name server administrators with the registrar account, please use the feature [Link WHOIS handles](#link_whois_handles).

In the case of a domain name cancellation and following deletion, any subordinate name servers are not deleted, they are marked for deletion.

The superordinate domain name might might become available for registration upon deletion after the 30 day redemption period. It will not be possible to register or take over the name servers marked for deletion. They can only be recreated after successful deletion by the registry.

#### Administer Name Servers

When name servers have been created they can be edited.

For name servers, which are subordinate, to a .dk domain in the registrars portfolio. glue records can be added and removed. Glue records are supported for both IP version 4 and 6. Please see the section on the [glue record policy][DKHMDNSGLUE] in the [DK Hostmaster Name Service Specification][DKHMDNS].

The administrator for the name server can be changed as follows:

- For a name server under registrar management, this can be done by the registrar and the existing name server administrator. There is not requirement that the handled appointed to the task is under the same management model
- For a name server under registrant management, this can be only be done by the existing name server administrator

#### Name Server Deletion

When a name server no longer is serving any domain names, it is eligible for deletion.

This operation can be performed as follows:

- For a name server under registrar management, this can be done by the registrar and the existing name server administrator
- For a name server under registrant management, this can be only be done by the existing name server administrator

<a id="prepaid"></a>

### Prepaid

The feature requires that the portal-user has the meta-role: `Payer`, please see: [Meta-Roles](#meta-roles) for more details.

The registrar account is a prepaid account, meaning the registrar holds the responsibility of keeping the account sufficiently funded.

A set of the billable operations will be declined in case of insufficient funds, they are:

- Create domain name
- Transfer domain name

The other billable operations, not limited by insufficient funding are:

- Automatic renewal
- Manual renewal
- Manual restoration
- Change registrant

Overall the following policies are in place currently.

- Expansion of portfolio requires sufficient funding
- Maintenance of existing portfolio is possible without sufficient funding

For more information on grace periods and handling of these please refer to the registrar agreement.

<a id="add-funds-to-registrar-account"></a>

#### Add funds to registrar account

Adding funds can to the registrar account can be accomplished in a few ways.

The registrar portal offers, transferring via credit card.

For Danish registrars a unique FIK code has been allocated, which identifies the registrar account

For non-Danish registrars it is possible to do a bank transfer. Handling of bank transfers are manual and are therefor as a minimum subject to registry opening hours and a manual processing time schedules.

The ensure the speediest and most successful processing of  bank transfers make sure to provide the required information:

- IBAN
- Your registrar account number

<a id="references"></a>

## References

List of references used in this document in alphabetical order.

1. [DK Hostmaster: Become a registrar][DKHMBEREG]
1. [DK Hostmaster: Implementation guide for registration of .dk][IMPLGUIDE]
1. [DK Hostmaster: Sandbox Environment Specification][DKHMSANDBOX]
1. [DK Hostmaster: EPP Service Specification][DKHMEPP]
1. [DK Hostmaster: Name Service Specification][DKHMDNS]
1. [DK Hostmaster: Products and Prices][DKHMPRICES]
1. [DK Hostmaster: Registrar Portal Service Specification Screenshots](screenshots/)

<a id="resources"></a>

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

<a id="feature-and-meta-role-matrix"></a>

### Feature and Meta-role Matrix

| Feature                                                                            | Meta-role     |
|:-----------------------------------------------------------------------------------|:--------------|
| [Create Portal User](#create-portal-user)                                          | Administrator |
| [Enable/Disable Portal User](#enable-or-disable-portal-user)                       | Administrator |
| [Edit Portal User](#edit-portal-user)                                              | Administrator |
| [Delete Portal User](#delete-portal-user)                                          | Administrator |
| [Create Service User](#create-service-user)                                        | Administrator |
| [Enable/Disable Service User](#enable-or-disable-service-user)                     | Administrator |
| [Edit Service User](#edit-service-user)                                            | Administrator |
| [Delete Service User](#delete-service-user)                                        | Administrator |
| [Link WHOIS Handle](#link-whois-handle)                                            | Administrator |
| [Unlink WHOIS Handle](#unlink-whois-handle)                                         | Administrator |
| [Merge WHOIS Handles](#mergewhois-handles)                                         | Administrator |
| [Create WHOIS Registrar Account Handle](#create-whois-handle)                      | Administrator |
| [Apply/Create domain name](#domain-name-application)                               | Registrar |
| [Transfer Domain Name](#transfer-domain-name)                                      | Registrar |
| Generate authorization for transfer                                                | |
| [Add funds to Registrar Account](#add-funds-to-registrar-account)                  | Payer |
| [Renew Domain Name](#renew-domain-name)                                            | Payer |
| Change Name Servers                                                                | Name Server Administrator |
| Generate authorization for change of name servers                                  | Name Server Administrator |
| Administer Name Servers                                                            | Name Server Administrator |
| Administer domain name                                                             | Proxy |
| Administer WHOIS user registrant                                                   | Proxy |
| [Restore Domain Name](#restore-domain-name)                                        | Proxy |
| [Cancel/Delete Domain Name](#cancel-domain-name)                                   | Proxy |
| [Set auto-expire/renewal for domain name](#set-auto-expirerenewal-for-domain-name) | |
| Set period for domain name                                                         | Proxy |

[DKHMLOGO]: https://www.dk-hostmaster.dk/sites/default/files/dk-logo_0.png
[GHAMKDBADGE]: https://github.com/DK-Hostmaster/rp-service-specification/workflows/Markdownlint%20Action/badge.svg
[GHASPLLBADGE]: https://github.com/DK-Hostmaster/rp-service-specification/workflows/Spellcheck%20Action/badge.svg
[IMPLGUIDE]: https://www.dk-hostmaster.dk/en/implementation-guide-registration-dk
[WAITLIST]: https://www.dk-hostmaster.dk/en/waiting-list
[DKHMMAIL]: https://www.dk-hostmaster.dk/en/mailing-lists
[DKHMBEREG]: https://www.dk-hostmaster.dk/en/become-registrar
[DKHMSANDBOX]: https://github.com/DK-Hostmaster/sandbox-environment-specification
[DKHMEPP]: https://github.com/DK-Hostmaster/epp-service-specification
[DKHMPRICES]: https://www.dk-hostmaster.dk/en/products-and-prices
[DKHMDNS]: https://github.com/DK-Hostmaster/dkhm-name-service-specification
[DKHMDNSGLUE]: https://github.com/DK-Hostmaster/dkhm-name-service-specification#glue-records
[DKHMDAS]: https://github.com/DK-Hostmaster/das-service-specification
[DKHMDSU]: https://github.com/DK-Hostmaster/dsu-service-specification
