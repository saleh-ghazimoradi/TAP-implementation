GSM Association Confidential - Full, Rapporteur, and Associate Members
Official Document TD.58 - TAP3.12 Implementation
Handbook<img src="./fwccxo2z.png"
style="width:1.83333in;height:1.88889in" />

> **TAP3.12** **Implementation** **Handbook** **Version** **2.5**
>
> **26** **May** **2014**

*This* *is* *a* *Non-binding* *Non-binding* *Permanent* *Reference*
*Document* *of* *the* *GSMA*

**Security** **Classification:** **Confidential** **-** **Full,**
**Rapporteur,** **and** **Associate** **Members**

Access to and distribution of this document is restricted to the persons
permitted by the security classification. This document is confidential
to the Association and is subject to copyright protection. This document
is to be used only for the purposes for which it has been supplied and
information contained in it must not be disclosed or in any other way
made available, in whole or in part, to persons other than those
permitted under the security classification without the prior written
approval of the Association.

**Copyright** **Notice** Copyright © 2014 GSM Association

**Disclaimer**

The GSM Association (“Association”) makes no representation, warranty or
undertaking (express or implied) with respect to and does not accept any
responsibility for, and hereby disclaims liability for the accuracy or
completeness or timeliness of the information contained in this
document. The information contained in this document may be subject to
change without prior notice.

**Antitrust** **Notice**

The information contain herein is in full compliance with the GSM
Association’s antitrust compliance policy.

V2.5 Page 1 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook **Table**
**of** **Contents**

**1** **Introduction** **5** 1.1 Overview 5 1.2 Scope 5 1.3 Definition
of Terms 5 1.4 Document Cross-References 6

**2** **Physical** **Implementation** **6** 2.1 How to decode a TAP file
6 2.1.1 Identifying the TAP release 6 2.2 Physical Implementation
Considerations 6 2.2.1 Zero Length Elements 6 2.2.2 Elements filled with
spaces (blanks) 7 2.2.3 Integer size for specific elements 7 2.2.4 ASN.1
extension markers 7 2.2.5 Empty Choice Elements Encoding 9

**3** **Service** **Implementation** **9** 3.1 GPRS 9 3.1.1 General 9
3.1.2 Principles of GPRS Partial Handling 9 3.1.3 Multiple SGSN IP
Addresses 11 3.1.4 Data Volume Size Definitions 11 3.1.5 GPRS Partials
relevant to CAMEL usage 11

> 3.1.6 Population of Access Point Name (APN) Information for GPRS call
> event relevant to CAMEL usage 11
>
> 3.1.7 Call Type Levels in GPRS Event 12 3.1.8 Presence of Both Charged
> Item ‘X’ and ‘V/W’ Within the Same GPRS
>
> Event 13 3.2 SMS 15 3.2.1 SMS over GPRS 15 3.2.2 SMS over IP (VoLTE)
> 15 3.2.3 SMS-MO 16 3.2.4 SMS-MT 16 3.3 CAMEL 16 3.3.1 Camel Invocation
> Fee 16 3.3.2 CAMEL in case of Call Forwarding (CF) 17 3.3.3 Validation
> of CAMEL destination presence in case of number or APN
>
> modification 17 3.3.4 The importance of CAMEL Destination Number 17
> 3.3.5 CAMEL for Video Telephony usage 17 3.4 Services implementation
> on top of a Bearer 17 3.5 National Mobile Number Portability (MNP) 17
> 3.5.1 Subscriber Identification 17 3.5.2 Charge Differentiation 18 3.6
> Optimal Routing 19

V2.5 Page 2 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook

> 3.7 WLAN 20
>
> 3.7.1 Identification of WLAN in TAP 21 3.7.2 Charging ID 21 3.7.3 Some
> other topics to observe for WLAN 21 3.7.4 Differences to GPRS 21 3.7.5
> Similarities to GPRS 21 3.8 Satellite Destinations 21 3.9 Video
> Telephony 21 3.10 UMTS 22 3.10.1 UMTS Circuit Switched Bearer Services
> 22 3.10.2 UMTS Packet Switched / GPRS Handover 22 3.11 Intelligent
> Call Assistance Service 23 3.12 Voice Messaging Service 24 3.13
> Universal Service Fund 25 3.14 Supplementary Services 26 3.15
> Teleservice Category Codes 26 3.16 Long Term Evolution (LTE) 27 3.16.1
> Voice and SMS over LTE (VoLTE) 27 3.17 LTE / 2G-3G Packet Switched
> Handover 29 3.18 CS Voice Partials Aggregation 31

**4** **Common** **Elements** **Implementation** **33** 4.1 General
Rules 33 4.2 Taxation 33 4.2.1 General 33 4.2.2 Handling of tax on tax
33 4.2.3 Tax Breakdown 33 4.2.4 Fixed tax based on duration 37 4.2.5 Tax
and Charge break down per Charge Type 38 4.3 Separation of charges
within a call 39 4.4 Dialled Digits 42 4.4.1 Dialled Digits definition
42

> 4.4.2 Population of Called Number, Dialled Digits and CAMEL
> Destination
>
> Number 42 4.5 Population of Calling Number on MTCs within TAP 52 4.6
> Population of call duration and timestamps for charging (MOCs and
> MTCs) 52 4.7 Population and Validation of Exchange Rates 56 4.7.1
> Exchange Rates Quoted by the International Monetary Fund (IMF) 56
> 4.7.2 Exchange Rates Not Quoted by the IMF 57 4.7.3 Significant Digits
> and Decimal Places 58 4.8 Updating the Local Currency in TAP 59 4.9
> Population of high and low values in Charge and Total Charge elements
> 60 4.10 Discrepancy of Calculated Tax values between TAP and Invoice
> 60 4.11 IOT Validation Examples 60 4.12 Network Node Sharing 63 4.12.1
> MSC Sharing for MOC/MTC Voice Calls and SMS Events 63

V2.5 Page 3 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook

> 4.12.2 SGSN Sharing between two or more Network Operators 65
>
> 4.12.3 IR.21 Information Required 66 4.12.4 Usage of Location
> Information for Serving Network Identification 67 4.12.5
> Identification of Host/Network Extension for Retail Billing Process 67

**5** **Change** **Request** **Impact** **Classification** **68** 5.1
Impact class 4 68 5.2 Impact class 3 69 5.3 Impact class 2 69 5.4 Impact
class 1 69

**Annex** **A** **Document** **Management** **70** A.1 Document History
70

> Other Information

V2.5

> 72

Page 4 of 72

> GSM Association Confidential - Full, Rapporteur, and Associate Members
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> **1** **Introduction**
>
> **1.1** **Overview**
>
> The purpose of this document is to provide additional information for
> implementing Transferred Accounts Procedure version 3 (TAP3). The TAP3
> Implementation Handbook serves as a description manual, which supports
> TAP3 implementation based on TD.57.
>
> **1.2** **Scope**
>
> The document is intended to provide implementation guidance for
> Transferred Account Procedure (TAP).For detailed examples, see TD.60.
>
> Note: The current version of this document supports TAP version 3
> release 12 only.
>
> **1.3** **Definition** **of** **Terms**

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> V2.5 Page 5 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook **1.4**
> **Document** **Cross-References**

||
||
||
||
||
||
||
||

> **2** **Physical** **Implementation**
>
> **2.1** **How** **to** **decode** **a** **TAP** **file**
>
> It is good practice to decode a TAP file in the following order:
>
> 1\. Firstly, decode the Batch Control Information, Accounting
> Information, Network Information and Audit Control Information.
>
> 2\. Secondly, decode the Call Events Details; each element (Mobile
> Originated Call (MOC), Mobile Terminated Call (MTC) and so forth).
> These should be decoded one after the other.
>
> **2.1.1** **Identifying** **the** **TAP** **release**
>
> As specified in TD.57, the ASN.1 definition and tag numbers for the
> data items Specification Version Number and Release Version Number
> remain the same in all TAP releases from TAP3 onwards. A program with
> the sole purpose to identify the TAP release of an input TAP file
> (TAP3 and higher) is therefore feasible. This program must be able to
> read a sequence of BER encoded TAP3 elements until it has read the
> ASN.1 elements representing the Release Version Number and the
> Specification Version Number. This makes it possible to identify these
> two data items and thereby the applicable TAP release and release
> version prior to decoding the TAP file.
>
> **2.2** **Physical** **Implementation** **Considerations** **2.2.1**
> **Zero** **Length** **Elements**
>
> The ASN.1 syntax allows production of elements with a size (length) of
> zero bytes. This is valid according to BER but all parties creating
> TAP must take measures to avoid such implementations. When such errors
> are encountered in a TAP file, it is allowed to raise either of the
> following errors:
>
> • Syntax error for the element that is zero length
>
> • Group structure error applicable to the group that contains the
> element (this treats it as though the zero length elements were not
> present in the group)
>
> Note: The severity of the error must be according to the severity of
> the applicable syntax or group structure error. The group structure
> error may not always be applicable.
>
> A VPMN cannot treat an element with length zero as an invalid BER
> encoding, that is Fatal error code 53 (file not encoded according to
> ASN.1 BER) must not be applied.
>
> V2.5 Page 6 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook

For example, where the element Tax Value in Tax Information is present
but has no content (length is zero) the HPMN can only raise one of the
following errors (no other validation rule

is applicable):

> • Severe error code 10 (syntax error) on element Tax Value in the
> Calls context • Severe error code 31 (tax value missing) on group Tax
> Information in the Calls
>
> context

**2.2.2** **Elements** **filled** **with** **spaces** **(blanks)**

Like the zero length elements, (see section 2.2.1) elements must not be
filled with spaces. Such space filled elements can actually be treated
as zero-length when all spaces have been discarded, and the rules in
section 2.2.1 must be followed.

**2.2.3** **Integer** **size** **for** **specific** **elements**

ASN.1 allows the creation of integers with an unlimited size. This
means, that the length of an ASN.1 encoded integer value can vary
between one and X bytes depending on the containing value. The
representation has to be the minimal possible length that is the nine
most significant bits of the encoded value must not be identical.

For TAP, there is only the differentiation between the maximum size of
four bytes/octets and maximum of eight bytes depending on the element.
TD.57 contains a list of elements to be encoded with a maximum size of
eight bytes (see TD.57 chapter 6.1 Abstract Syntax).

**2.2.4** **ASN.1** **extension** **markers**

Extension markers (‘…’) are added at the group or list levels where
possible (within all Choice and Sequence elements). Extension markers
must not be used to introduce elements outside of the normal TAP release
procedure. All bi-lateral sending of additional elements must use the
Operator Specific Information.

Examples:

CallEventDetail::= CHOICE

{ mobileOriginatedCall mobileTerminatedCall supplServiceEvent
serviceCentreUsage valueAddedService gprsCall contentTransaction
locationService newInsertedField ...

}

MobileOriginatedCall, MobileTerminatedCall, SupplServiceEvent,
ServiceCentreUsage, ValueAddedService, GprsCall, ContentTransaction,
LocationService ,

NewInsertedField,

In case of a sequence, the three dots for the extension marker may be
before any new added element.

V2.5 Page 7 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members
Official Document TD.58 - TAP3.12 Implementation Handbook

First extended release:

TransferBatch ::= \[APPLICATION 1\] SEQUENCE {

> batchControlInfo BatchControlInfo OPTIONAL, -- \*m.m. accountingInfo
> AccountingInfo OPTIONAL, networkInfo NetworkInfo OPTIONAL, -- \*m.m.
> messageDescriptionInfo MessageDescriptionInfoList OPTIONAL,
> callEventDetails CallEventDetailList OPTIONAL, -- \*m.m.
> auditControlInfo AuditControlInfo OPTIONAL, -- \*m.m. ...,

firstInsertedField FirstInsertedField OPTIONAL }

Second further extended release:

TransferBatch ::= \[APPLICATION 1\] SEQUENCE

{ batchControlInfo accountingInfo

> networkInfo

BatchControlInfo AccountingInfo NetworkInfo

OPTIONAL, -- \*m.m. OPTIONAL, OPTIONAL, -- \*m.m.

> messageDescriptionInfo MessageDescriptionInfoList OPTIONAL,
>
> callEventDetails auditControlInfo ..., firstInsertedField
> secondInsertedField

}

CallEventDetailList AuditControlInfo

FirstInsertedField

SecondInsertedField

OPTIONAL, -- \*m.m. OPTIONAL, -- \*m.m.

> OPTIONAL,

OPTIONAL

With this syntax, you are able to support different releases of TAP3
definitions. It allows systems built for the first version (not
extended) of the grammar to silently ignore ‘firstInsertedField’and
‘secondInsertedField’. A system built to support the first extended
release of the grammar will silently ignore the element
‘secondInsertedField’.

Decoding of extension marker information:

If a TAP decoding application identifies that a valid (as per the ITU
ASN1 standard) and unknown ASN1 data block is present at an extension
marker position, all the data contained in this block must be ignored.
Further processing of the data contained in this block must not be
attempted. The decoder should resume standard processing at the next
item following the extension marker data block. For example, let us
assume that the following information is received in a TAP3.11 file in
the Call Type Group of a MOC event:

{CallTypeGroup {CallTypeLevel1} {CallTypeLevel2} {CallTypeLevel3}
{CalledCountryCode}

}

The data item Called Country Code does not exist in TAP 3.11 and
therefore the tag of this item will be unknown to a TAP 3.11 decoder;
however, the ASN1 grammar contains the extension marker just after item
Call Type Level 3 data item. As a result, data item
{CalledCountryCode}must be ignored by the decoder and processing must
continue with the next data item present in the file.

V2.5 Page 8 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members
Official Document TD.58 - TAP3.12 Implementation Handbook

Notes:

> • In this example, warning error 57 can be raised however not fatal
> error 50.
>
> • The version of ITU ASN.1 standards referenced detailed in TD.57 (ITU
> Rec. X.680) supports the extension markers.

**2.2.5** **Empty** **Choice** **Elements** **Encoding**

The tagging type for a tagged choice type is always EXPLICIT.

ASN1 encoded TAP 3.11 file having just the tag and zero length contents
is “Incomplete" and will be considered as invalid BER encoding.

Therefore, files with such TAG errors can be rejected using error code
53.

For example:

> ImeiOrEsn ::= \[APPLICATION 429\] CHOICE {
>
> imei Imei, esn Esn, ...
>
> }

could be encoded as

> ImeiOrEsn \[ TAG "7F832D"H (429) LEN "00"H (0) \] {
>
> }

In other words 0x7F832D00 (encoded)

In case none of the choice elements are present – the whole ‘choice’
construction (tag id and length) should not be present in the encoded
TAP3 file.

**3** **Service** **Implementation**

**3.1** **GPRS**

**3.1.1** **General**

It is not allowed to send S-CDR and G-CDR separately for the same PDP
context. If information from both the S-CDR and the G-CDR is used within
the same PDP context and time period, they must be combined into one TAP
GPRS Call event.

**3.1.2** **Principles** **of** **GPRS** **Partial** **Handling**

This chapter provides information on how to create and handle partial
GPRS call events within TAP files. For information on GPRS partials
limits (partial time interval /number of partials) see BA.12.

When handling / creating GPRS partials please note that the following
applies:

> • TAP file partials must not be mistaken for being network-generated
> partials. In some cases a network partial may be forwarded at the TAP
> interface as a single GPRS partial. However, since there is a limit of
> partials (per PDP context per day) that must

V2.5 Page 9 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook

> not be exceeded on the TAP interface, in most cases GPRS partials will
> be the result of network partials aggregation. A one to one relation
> between the network and
>
> GPRS partial records cannot be expected.
>
> • To allow the HPMN to bill its subscriber based not only on volume,
> all GPRS partials must be forwarded to the HPMN (for example time
> generated partials which may carry no charge in the case of
> operator-to-operator volume charging, must still be transferred in the
> TAP files as the HPMN may need these for re-rating and/or customer
> care purposes).
>
> • Only consecutive network partials can be aggregated to a GPRS
> partial. For example if the VPMN has partials 1, 2, 3 and 5, with
> partial 4 missing/not available for TAP transfer, then only partials
> 1, 2 and 3 can be aggregated in an aggregated GPRS Call and a separate
> GPRS Call for partial 5 made available in the TAP file.
>
> • The HPMN should have in mind that partials may not be received in
> the correct order (for example because partials were not received in
> the correct order from the network or because a TAP file has been
> delayed/rejected).
>
> • An intermediate partial may be received well after the last partial
> for the same PDP context has been received.
>
> • The only way, to sort GPRS partials in the correct sequence, is by
> using the date & time information present in each partial (in some
> cases of course switch manufacturers may offer proprietary data items
> to assist in partial sequencing). Please note that in case of
> multi-SGSN partials, clocks on different SGSNs may not be synchronized
> up to the second.
>
> • Where partial GPRS records are issued on TAP, the partial type
> indicator must be populated correctly. This data item is vital for the
> HPMN aggregation of partials for end user billing. In some cases,
> values in this data item are also necessary to validate charges in TAP
> records.
>
> • The VPMN must aggregate the GPRS network partials to meet the limit
> of number of TAP GPRS partials per context and day defined in BA.12.
>
> •     Inter Operator Tariff (IOT) check for GPRS Partials: GPRS
> partials in many cases need to be validated independently as not all
> the partials are always available.

Note: it is not always possible to perform a guaranteed charge
validation on GPRS partials. As a general rule, a GPRS partial can only
be rejected if it can be guaranteed that it does not meet the IOT.

The first partial can always be validated. However, it is not always
possible to validate intermediates or last partials (for example, as for
many GPRS IOTs one needs to know the data volume transferred before the
intermediate or last partial was generated in order to determine the
charge). Intermediate partials and last partials can be rejected if the
associated charge is greater than the maximum according to the
applicable IOT.

The Partial Type Indicator relates to the creation of the CDR (first
partial created, intermediate and last) and does not relate in any
manner to the charging method.

Any applicable IOT steps are totally independent from the usage of the
Partial Type Indicator.

V2.5 Page 10 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook

Please note there are currently no TADIG test cases defined that would
allow verification of correct GPRS partials generation for GPRS (for
example, a long term GPRS session with

duration greater than 24 hours).

**3.1.3** **Multiple** **SGSN** **IP** **Addresses**

There can be multiple IP addresses for a single SGSN.

**3.1.4** **Data** **Volume** **Size** **Definitions**

To prevent invalid calculations and charging the following clarification
is made:

> • One kByte is not 1000 Bytes, but 1024 Bytes.

The same goes for one MByte, which are 1024 kBytes and not 1000 kBytes.

In the case of rounding up to the nearest kByte, a call with a volume of
1019 Bytes is only one kByte and not two kBytes, whereas a call of 1025
Bytes should be two kBytes.

**3.1.5** **GPRS** **Partials** **relevant** **to** **CAMEL** **usage**

VPMN must supply CAMEL information in each GPRS partial on transferring
Partial GPRS Events relevant to CAMEL usage in TAP files. The mandatory
presence is to ensure successful Tariff validation and HPMN re-pricing.
Please see below the example scenario A in section 3.1.6.

**3.1.6** **Population** **of** **Access** **Point** **Name** **(APN)**
**Information** **for** **GPRS** **call** **event** **relevant** **to**
**CAMEL** **usage**

Mapping rules between network level CDR (S-CDR) and TAP CDR in regards
to the actual connected/original APN NI & OI relevant to CAMEL usage
should be handled according to the description provided in the data
dictionary for “GPRS Destination” in TD.57.

APN Information (APN NI & APN OI) is mapped one to one between the
network CDR (S-CDR) and TAP CDR.

> a\) APN NI & APN OI from S-CDR:

The Actual connected/or modified APN NI & APN OI are used to populate
GPRS Basic Call Information group in TAP. It is mandatory for each GPRS
partial call record.

> b\) CAMEL APN NI & CAMEL APN OI from S-CDR:

The Original APN NI & APN OI as entered by the subscriber are used to
populate CAMEL Service Used group in TAP. They are conditional for GPRS
partial call records. Thus, they may be available on the first partial
but not guaranteed on subsequent partial call records as it will be
subject to availability from the network.

Example A: GPRS relevant to CAMEL usage (first partial)

> • Actual APN NI as typed in by the subscriber: digitalforum.com
>
> • Modified APN NI as returned by the CAMEL server:
> corporate.digitalforum.com

The following table shows the contents of the relevant TAP elements:

V2.5 Page 11 of 72

> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **1:** **Example** **A:** **Relevant** **TAP** **elements**
> **(first** **partial)**
>
> Example A: GPRS relevant to CAMEL usage (second partial)
>
> • Actual APN NI as typed in by the subscriber: digitalforum.com
>
> • Modified APN NI as returned by the CAMEL server:
> corporate.digitalforum.com
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **2:** **Example** **A:** **Relevant** **TAP** **elements**
> **(second** **partial)**
>
> **3.1.7** **Call** **Type** **Levels** **in** **GPRS** **Event**
>
> Call Type Levels (1, 2, 3) are used to identify the IOT tariff defined
> by the VPMN to charge for GPRS usage in TAP. It is important that
> Operators populate Call Type Levels with the correct values that
> reflect the roaming subscriber usage in terms of the access method to
> GPRS services, the QoS Type provided and any detailed qualifications
> of the QoS Type as per the VPMN’s IOT.
>
> **3.1.7.1** **Access** **to** **GPRS** **Services**
>
> Call Type Level1 values describe the different GPRS access methods
> that could be used:
>
> V2.5 Page 12 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> • Call Type Level 1 = 10(HGGSN) means that the roaming subscriber has
> access to
>
> the GPRS Services through the GGSN located at the HPMN side. This
> currently represents the common implementation access method to GPRS
> Services by the Operators.
>
> • Call Type Level 1 = 11(VGGSN) means that the roaming subscriber has
> access to GPRS Services through the GGSN located at the VPMN side as
> such, indicates Local Access to GPRS Services. This is currently not
> in use due to the lack of technical feasibility which enables the
> identification of the service used by the subscriber at the VPMN side.
>
> • Call Type Level 1 = 12(Other GGSN) means that the roaming subscriber
> has access to GPRS Services through a GGSN which belongs to a third
> party vendor typically operated on behalf of the HPMN. The GGSN
> belongs to neither VPMN nor HPMN in this case.

**3.1.7.2** **QoS** **Type** **Attributes**

> Call Type Level 2 values describes the QoS attributes provided to
> distinguish the level of the service used and the resources consumed
> to provide the selected service.
>
> The appropriate value corresponding to the QoS Type provided should be
> populated in Call Type Level 2 upon the availability of the relevant
> information from the VPMN’s network.
>
> Call Type Level 3 provides the means for the VPMN to further specify
> any detailed qualification of the QoS Type already set in Call Type
> Level 2.The data item is populated with the appropriate value as
> defined in the VPMN’s IOT.

**3.1.7.3** **Differentiated** **data** **charging** **by** **Call**
**Type** **Level**

> Where QoS is not an applicable IOT differentiator the value ‘0’
> (unknown/not applicable) is used for Call Type Level 2. If the VPMN
> then wants to further differentiate rates, for example for different
> rates applicable to 3G and LTE, Call Type Level 3 can be used. If this
> is done then the full rate plus Call Type Levels 1/2/3 combinations
> must be defined in the VPMN’s IOT and the CTL 1/2/3 values used in the
> TAP record Charge Information must match those defined in the IOT.
>
> **3.1.8** **Presence** **of** **Both** **Charged** **Item** **‘X’**
> **and** **‘V/W’** **Within** **the** **Same** **GPRS** **Event**
>
> Telecom operators are advised not to provide more than one occurrence
> of Charge Information Group where one occurrence has Charged Item
> value ‘X’ and another one has Charged Item value ‘V’ or ‘W’.
>
> Although this is not strictly forbidden from a commercial perspective
> due to freedom of charging principles granted to telecom operators, it
> is, however, advised that such occurrence of more than one Charge
> Information, especially where the Charge is greater than zero, in both
> Charge Information Groups has a severe impact on the majority of the
> receiving HPMNs’ billing systems. This is due to the fact that the
> HPMN is not able to process the GPRS charges associated with both
> Charge Items ‘X’ and ‘V’ or ‘W’, so the billing system may consider
> that the same data volume is double charged within the GPRS Event.
>
> V2.5 Page 13 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> It is more likely that the occurence of more than one Charge
> Information Group within the same GPRS Event has happened due to an
> incorrect TAP implementation or a technical
>
> error on providing the GPRS Event on the TAP Interface.
>
> The following example scenario shows an illustration of an erroneous
> GPRS Event provided in the TAP file:
>
> • IOT Charge for data volume is: 5 SDR per 1 MB
>
> • Charge Information group 1: Charged Item ‘X’ and the Total Volume is
> 2 MB
>
> • Charge Information group 2: Charged Item ‘V’ and the Data volume
> Outgoing is 1 MB
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **3:** **Two** **Charge** **Information** **Groups**
> **with** **Charged** **Item** **‘X’** **&** **‘V’**
>
> Note: As shown in the example scenario above, the Data Volume Outgoing
> has been double charged. The first time in association with Charged
> Item ‘X’ and the second time in association with Charged Item ‘V’.
>
> V2.5 Page 14 of 72

GSM Association Confidential - Full, Rapporteur, and Associate
Members<img src="./fh5qxy3d.png"
style="width:6.26792in;height:1.21944in" />

Official Document TD.58 - TAP3.12 Implementation Handbook **3.2**
**SMS**

The Short Message Service is independent of the transport mechanism,
circuit switched (CS) or packet switched (GPRS), and in TAP, it is
reported in a MOC or MTC call event in the case of SMS over CS or GPRS.

In case of SMS over IP (VoLTE), the Messaging Event is used to support
SMS Events (SMS-MO & SMS-MT) in TAP.

**3.2.1** **SMS** **over** **GPRS**

Because SMS over GPRS does not require an active PDP context, it is not
a GPRS call.

The recording entity type distinguishes SMS over GPRS from SMS over CS.

> • SMS over GPRS: • SMS over CS:

Recording Entity Type = SGSN

Recording Entity Type = MSC

Inspection of the SMS records raised at the SGSN shows that all the
necessary data items are present to populate a MOC or MTC call event in
TAP.

**3.2.2** **SMS** **over** **IP** **(VoLTE)**

IP-SM-GW (IP Short Message Gateway) is a SIP based application server
which is used in the delivery of the SMS over IP bearer. The IP-SM-GW
provides protocol interworking between the IP-based UE and the SMSC
which uses MAP (Mobile Application Part).The SMS is routed to the SMSC
for delivery to the SMS Destination or the SMS is received from the SMSC
for delivery to an IP-based UE.

The successful submission of the SMS will follow the following steps:

> • The submitted SMS by the roaming subscriber will use SIP Message
> method to route the SMS from the visited P-CSCF to the Home S-CSCF in
> the IMS domain.
>
> • The IP-SM-GW located in the HPMN extracts the submitted SMS from the
> SIP Protocol and relay it to the Home SMSC using MAP.
>
> • The Home SMSC submits the SMS to the SMS Destination.

The submission of the SMS can be shown in the following diagram:

> **Figure** **1:** **Submission** **of** **SMS-MO** **over** **LTE**

V2.5 Page 15 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook **3.2.3**
**SMS-MO**

Due to the fact that the SMSC may be necessary for billing, the data
item Called Number is mandatory and must contain the SMSC address in
case of SMS usage. If available, the SMS recipient (destination),
exactly as dialled by the subscriber, must be filled in the data item
SMS Destination Number.

It should be noted that it is expected to have more than one SMS-MO
event created for a long SMS where it exceeds 160 characters. The value
of the Call Reference element available in TAP will uniquely identify
each SMS-MO event. There is no technical means to enable the aggregation
of the SMS-MO events created for the long SMS.

**3.2.4** **SMS-MT**

The data item Calling Number is mandatory and must contain the SMSC
address in case of SMS usage. If available, the SMS sender
(origination), in international format, must be filled in the data item
SMS Originator.

**3.3** **CAMEL**

Currently there are 4 phases of CAMEL implementations with different
features. Each phase supports the features of the previous phase plus
some additional features. One of the main applications supported by
CAMEL service is prepaid billing.

Note that CAMEL Service Level and CAMEL Phases are not directly related
to each other. CAMEL Service Level describes the service logic employed
(Service Type) by the HPMN, for example, VPN Roaming. CAMEL Phases
describe the CAMEL features being used by such services.

**3.3.1** **Camel** **Invocation** **Fee**

The CAMEL charging construct was simplified in TAP3.11, as no additional
Charge Information details were required apart from the CAMEL Invocation
Fee, and possible tax, discount and exchange rate information.
Therefore, within CAMEL Service Used, the Charge Information has been
replaced with Camel Invocation Fee.

The CAMEL Invocation Fee contains the charge (if greater than zero) for
the CAMEL invocation after discounts have been deducted (if applicable,
see Discount Information) but before any tax is added (if applicable,
see Tax Information) and must not contain a negative value.

The charge is in the same currency as all other charges in the TAP file
with the number of decimal places from the data item TAP Decimal Places.

All CAMEL Invocation Fees are to be included in the total charge for the
file (Audit Control Information) but not in the total charge within the
Charge Information associated with each TAP call / event.

Note: The Basic Service Used group is used to charge for the non-CAMEL
related charges.

V2.5 Page 16 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook **3.3.2**
**CAMEL** **in** **case** **of** **Call** **Forwarding** **(CF)**

The tariff of the call and the content of the Call Type group, in case
of a CAMEL modification of the destination, cannot be determined using
the Called Number element. In this case, this information depends on the
CAMEL Destination Number.

**3.3.3** **Validation** **of** **CAMEL** **destination** **presence**
**in** **case** **of** **number** **or** **APN** **modification**

In TAP3.11, the Camel Service Used structure was simplified. Camel
modification information is not provided. In case Camel Destination
Number for MOC or GPRS Destination for GPRS call event is missing, the
validation cannot be carried out based on the information in TAP by the
VPMN. Only the HPMN can perform this validation and such validation
could be based on the knowledge of the applicable CAMEL logic.

**3.3.4** **The** **importance** **of** **CAMEL** **Destination**
**Number**

CAMEL Destination Number must be represented in the International format
on TAP. Where the CAMEL server does not return an international
representation, VPMN is obliged to modify the number to be in
international format because it represents a billing parameter for inter
operator charging. On the other hand CAMEL server implementations should
be done in a way that when the dialled number has been modified, the
server always returns a number in international format. Failure to
provide the number with a valid country code increases the risk of
incorrect charging and it is considered bad practise.

Please see Examples P, Q and R for further illustration in section 4.4.2
“Population of Called Number, Dialled Digits & CAMEL Destination
Number”.

**3.3.5** **CAMEL** **for** **Video** **Telephony** **usage**

CAMEL Phase1 supports all Tele Service Codes and Bearer Services Codes
related to MOC and MTC activities. Video Telephony can use either the
Synchronous Bearer Service code 30 or 37, which depends on the
implementation. Thus, Video Telephony can be supported at CAMEL Phase1.
Therefore, mobile networks will have the capability to implement Video
Telephony in their networks for CAMEL upon launching a 3G network using
Bearer Service code 30 or 37.

**3.4** **Services** **implementation** **on** **top** **of** **a**
**Bearer**

Currently, all services implemented on top of the same bearer (GPRS,
UMTS, CSD) are technically indistinguishable from each other in the
visited network. MMS, IM, PoC services are examples of such services
where their usage will not be differentiated at the bearer level and
hence the VPMN will be able to charge the Home network only for the
underlying bearer resources usage. For example, in TAP a GPRS Call is
raised for a MMS.

**3.5** **National** **Mobile** **Number** **Portability** **(MNP)**
**3.5.1** **Subscriber** **Identification**

Mobile Number Portability allows a subscriber to change from one network
operator to another taking their phone number with them to the new
network.

V2.5 Page 17 of 72

> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> Identification by IMSI will ensure the correct identification of the
> home network operator. If a subscriber switches from one operator, to
> another he may use his old MSISDN but he uses
>
> a new IMSI related to his new operator.
>
> Only for services, which do not use an IMSI for the subscriber
> identification, there may be a problem (for example WLAN which uses
> the realm for identification or SMS based on MSISDN only). This will
> have impact on billing.
>
> **3.5.2** **Charge** **Differentiation**
>
> VPMNs can have different IOT tariffs for destination networks with-in
> the same country. In the case of Mobile Number Portability from one
> network to another network, Call Events charges will be based on the
> IOT tariff for the destination network which has terminated the Call
> Event
>
> The IOT Tariff must be clearly identified through the correct
> population of Call Type Level data items for the destination number as
> shown below in Example scenarios A and B
>
> The following examples illustrate two calls towards numbers within the
> same numbering range. In these examples the calls are terminated on
> different networks due to number portability.
>
> Example A: MOC Call to a ported national number •     Actual dialled
> digits 01732975235
>
> • VPMN Country Code (CC) 49
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||

> **Table** **4:** **Example** **A:** **Relevant** **TAP** **elements**
> **(MOC** **to** **ported** **national** **number)**
>
> Example B: MOC Call to a non-ported national number • Actual dialled
> digits 01735146245
>
> • VPMN CC 49
>
> V2.5 Page 18 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||

> **Table** **5:** **Example** **B:** **Relevant** **TAP** **elements**
> **(MOC** **to** **non-ported** **national** **number)**
>
> **3.6** **Optimal** **Routing**
>
> The following diagram should explain the scenario for “optimal
> routing”.
>
> A subscriber, roaming in network B, makes a call to a subscriber of
> network A, who is
>
> roaming in the network C. Instead of routing the call through the
> network A to the destination network C, it will be routed directly to
> the network C.
>
> Note: Network B and C could be the same network.
>
> <img src="./2o2swcld.png"
> style="width:1.94245in;height:1.6191in" /><img src="./2jybawft.png"
> style="width:2.10448in;height:1.55439in" /><img src="./delrycws.png"
> style="width:1.94235in;height:1.6191in" /><img src="./mpxpzyj1.png"
> style="width:0.20255in;height:0.64764in" /><img src="./2xz2mcvz.png"
> style="width:0.20232in;height:0.64764in" />Network B MOC MTC Network C
> Optimally Routed Call
>
> Roaming Subscriber Roaming Subscriber
>
> Network A
>
> **Figure** **2:** **Optimal** **Routing**
>
> MOC:
>
> The element Destination Network must be used in case of optimal
> routing. It contains the five characters TADIG code (for example EUR01
> for Eurognet) and has to be different from the HPMN code of the
> destination subscriber for optimal routing. In this example, it would
> be network C. When the optimally routed calls have different charging,
> the call type levels should be used to indicate the specific rates
> applied.
>
> V2.5 Page 19 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook MTC:
>
> The element Originating Network must be filled with the 5-character
> TADIG code of the VPMN that originated the call (in the above example
> this is network B).
>
> In order to enable the Home Network to validate the TAP charge and/or
> re-rate the TAP record for retail purposes, they will need to be able
> to identify optimal routing and the originating and destination
> networks involved.
>
> Example: Optimal Routing
>
> Assumptions:
>
> • Network A: French Network
>
> •     Network B: •     Network C:
>
> • Actual dialled digits
>
> • VPMN International Access Code (IAC) • VPMN Country Code (CC)

German Network Belgian Network +331711234567890 00

49

> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||
||

> **Table** **6:** **Relevant** **TAP** **elements** **(Optimal**
> **Routing)** **3.7** **WLAN**
>
> WLANs are based on the IEEE 802.11 standard series, and can provide
> very high data speeds.
>
> Starting from TAP3.10 the billing of WLAN has been defined in TD.57
> specification. Non-GSM WLAN operators can also use TAP3 to exchange
> the charging information. In case a non-GSM operator wants to exchange
> TAP files, a TADIG code must be requested from the GSM Association.
> The GPRS Call Event Detail in TAP is to be used to cater for the WLAN
> scenario.
>
> The user of the WLAN service can be identified by IMSI, MSISDN or
> Network Access Identifier. When using username/password
> authentication, Network Access Identifier is the commonly used method
> to provide user identification, however in EAP methods the RADIUS
> User-Name attribute is not reliable for generating a TAP3 chargeable
> user identity meaning that only IMSI and/or MSISDN might be available
> for chargeable user identification.
>
> V2.5 Page 20 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook

In a WLAN environment, the primary source of event information is
created by a so-called RADIUS (Remote Access Dial-in User Service)
Server. How to map between RADIUS and

TAP3 is explained in the Data Dictionary of TD.57.

**3.7.1** **Identification** **of** **WLAN** **in** **TAP**

Call Type Level 1 is used to distinguish WLAN from normal GPRS.

**3.7.2** **Charging** **ID**

For WLAN networks, the derivation is at the discretion of the Sender.

Note: The Charging Id must remain unique (together with the recording
entity) for a

significant amount of time. A definition of the amount of time must be
seen in the normal TAP context, where no call event should be older than
30 days. It is therefore recommended to use a timeframe of 60 days
before the Charging ID is repeated.

Currently, there is no standard way to use APNs in the WLAN environment.
In the future, APNs will be used in a standardised way as defined by
3GPP Release 6.

**3.7.3** **Some** **other** **topics** **to** **observe** **for**
**WLAN** The following are general observations for WLAN:

> • The Recording Entity will contain the identity of the WLAN billing
> information recording entity.
>
> • Charging Id will contain the needed reference from the WLAN billing
> information recording entity.
>
> • Serving Location Description will contain a textual description of
> the Hot Spot. • Only minor Data Dictionary changes.

**3.7.4** **Differences** **to** **GPRS**

The following are differences between WLAN and GPRS events within TAP:

> • SGSN and GGSN are not available; instead, only one WLAN Recording
> Entity is
>
> present.
>
> • PDP address will not always be available.
>
> • Use of APN data item is at the discretion of the serving operator.

**3.7.5** **Similarities** **to** **GPRS**

GPRS partial rules apply also to WLAN.

**3.8** **Satellite** **Destinations**

TAP3.11 introduced a new value, “5”, for the Call Type Level 2 element.
This value can be used to represent calls to satellite destinations.
This makes it possible for the HPMN to verify or recalculate the price
for satellite calls.

**3.9** **Video** **Telephony**

The H.324 protocol is used to identify circuit switched (CS) video
telephony, which uses H.223 and H.245 settings at the user protocol
level. This means you must set the User Protocol Indicator to 4 (H.223 &
H.245), in order to identify the usage of video telephony. Please refer
to TD.57 Data Dictionary for more detail on how to derive the values.

V2.5 Page 21 of 72

> GSM Association Confidential - Full, Rapporteur, and Associate
> Members<img src="./vls3i35h.png" style="width:4.95in;height:1.125in" />
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> The element Bearer Service Code contains the values ‘30’ or ‘37’
> (depending on the implementation) in the case of video telephony.
>
> **3.10** **UMTS**
>
> Radio access technology cannot be used as a price differentiator.
>
> **3.10.1** **UMTS** **Circuit** **Switched** **Bearer** **Services**
>
> For UMTS CS Bearer Services the following elements must be filled
> (where available from the network):
>
> • Bearer Service Code
>
> • Fixed Network User Rate (FNUR) – (see TD.57)
>
> • The Guaranteed Bit Rate and Maximum Bit Rate from group Basic
> Service Group are used to specify the usage of UMTS circuit switched
> bearer service. These data items were added in the TAP 3.11 release.
>
> • The element User Protocol Indicator will identify the protocol used.
>
> Note: In addition to the 2G bearer service codes the following values
> can be used to identify UMTS service usage:
>
> • 27 - used for asynchronous services (also used with HSCSD) • 37 -
> used for synchronous services, implicates video telephony
>
> **3.10.2** **UMTS** **Packet** **Switched** **/** **GPRS**
> **Handover**
>
> The following time line shows a possible handover scenario between a
> UMTS packet switched and a GPRS network:
>
> **Figure** **3:** **Example:** **UMTS** **Packet** **Switched** **/**
> **GPRS** **handover**
>
> In order to follow the GPRS partial record rules, the different
> network call detail records (CDRs) need to be aggregated into one GPRS
> Call. In the example, there are different charges for UMTS and GPRS
> (different level of Quality of Service), which is illustrated by the
> Call Type Levels.

||
||
||
||
||
||
||

> V2.5 Page 22 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **7:** **Example:** **UMTS** **Packet** **Switched** **/**
> **GPRS** **handover** **(differential** **charging)**
>
> If there is no difference between the Call Type Level 1/2/3, the
> individual Charge Information groups can be aggregated into one single
> occurrence of Charge Information.
>
> Operators can choose to aggregate cross over GPRS and UMTS partials
> (handovers) in one session or not, as long as the rules for GPRS
> partials are followed (see section 3.1.2 Principles of GPRS Partial
> Handling).
>
> Note: The aggregation of network partials corresponds to the TAP
> standard.
>
> **3.11** **Intelligent** **Call** **Assistance** **Service**
>
> A few percent of calls end up as unsuccessful calls because customers
> do not dial correctly while being abroad, for example the dialled
> number without the country code. The intelligent call assistance
> services is able to identify most of these incorrectly dialled numbers
> by analysing the called number on certain number patterns and applying
> specific number translation rules for routing the call to the
> destination desired by the customer. Consequently, the routing of an
> incorrectly dialled number can be corrected and the call will be
> connected.
>
> One example of call assistance services is the usage of IN service to
> correct an incorrectly dialled number automatically. There can be two
> cases:
>
> Example A: IN service usage for a visitor who is a non-CAMEL
> Subscriber
>
> The visited non-CAMEL Subscriber has dialled his home national number
> without the country code in front of it. The connection of this number
> failed due to an invalid number in the visited country. The IN service
> corrects the dialled number by adding the visitor’s country code and
> the connection is now successful. The TAP record will be as in the
> following table:
>
> V2.5 Page 23 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||

> **Table** **8:** **Example** **A:** **Relevant** **TAP** **elements**
> **(non-CAMEL** **subscriber)**
>
> Example B: IN service usage for own subscribers roaming in VPMN where
> CAMEL Phase II has been supported
>
> The subscriber will be enabled in the HLR for IN availability by
> assigning a special CAMEL Service Key for the purpose of Call
> Assistance Service. If a subscriber visits a VPMN (where CAMEL II is
> available) and incorrectly dials a home phone number (for example
> International Access Code and Country Code forgotten or one zero
> forgotten in the International Access Code, etc.) the call assistance
> service will correct the dialled digits and the call can be connected
> successfully. The TAP record will be as in the following table:

||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **9:** **Example** **B:** **Relevant** **TAP** **elements**
> **(CAMEL** **subscriber)**
>
> **3.12** **Voice** **Messaging** **Service**
>
> Voice Messaging (VM) is a deferred message service (store-and-forward
> messaging), which allows the originator to send a voice message of
> limited duration to the recipient. The service employs voice circuit
> switched resources and is represented in TAP by a MOC or MTC event
> with the Tele Service Code ‘11’ – Telephony. To this extent, the
> Charged Item value ‘E’ – Event Based charge cannot be used for the
> Voice Messaging service due to existing validation rules. Instead, the
> Charged Item ‘F’– Fixed (one-off) Charge will be used for Voice
> Messaging Call Events
>
> V2.5 Page 24 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> The unique values of Call Type Levels (as defined in the VPMN’s IOT
> for Voice Messaging service) represent the only means to identify and
> validate the Charge associated with Voice
>
> Messaging events in TAP. This is important especially in the case
> where the VPMN is charging differently between Voice Messaging and
> telephony services.
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||

> **Table** **10:** **Relevant** **TAP** **elements** **(Voice**
> **Messaging** **service)** **3.13** **Universal** **Service** **Fund**
>
> The Universal Service Fund (USF) is applicable to operators in the
> USA, and is defined as follows by the US regulator (FCC):
>
> Because telephones provide a vital link to emergency services, to
> government services and to surrounding communities, it has been our
> nation’s policy to promote telephone service to all households since
> this service began in the 1930s. The USF helps to make phone service
> affordable and available to all Americans, including consumers with
> low incomes, those living in areas where the costs of providing
> telephone service is high, schools and libraries and rural health care
> providers. Congress has mandated that all telephone companies
> providing interstate service must contribute to the USF. Although not
> required to do so by the government, many carriers choose to pass
> their contribution costs on to their customers in the form of a line
> item, often called the “Federal Universal Service Fee” or “Universal
> Connectivity Fee”.
>
> If an operator via TAP wants to recover its contribution to the
> federal Universal Service Fund (USF) on services that are not exempt
> from USF assessment, this is done by specifying a charge in relation
> to a Charge Type value of 21 (VPMN Surcharge).
>
> The following example lists the relevant TAP data items within Charge
> Information.

||
||
||
||
||
||
||
||
||
||
||

> V2.5 Page 25 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||

> **Table** **11:** **Relevant** **TAP** **elements** **(Universal**
> **Service** **Fund)**
>
> Note: The calculated charge for USF is determined by the charging
> operator, as specified in its IOT. In the example, a duration-based
> charge is used however that is not meant to be excluding other ways of
> charging.
>
> **3.14** **Supplementary** **Services**
>
> A Supplementary Service (SS) can occur in conjunction with a MOC/MTC
> event or separately in a non-call related event. Invocation of a
> supplementary service, for example Call Forwarding, represents an
> example of a SS occurrence in conjunction with a MOC/MTC while the
> administration of SS, for example activation or de-activation,
> represents a separate non-call related SS event.
>
> Where a SS has been invoked in conjunction with a MOC/MTC, it will be
> recorded depending on the network configuration either “in-line” in
> the appropriate MOC/MTC network CDR or in a separate SS event. A
> non-call related SS transaction is recorded in a SS event.
>
> A Call Forwarding invocation is invoked in conjunction with a MOC
> event. The inline Supplementary Service Code data item in the MOC will
> be used to record Call Forwarding SS invocation codes/values for CFB,
> CFNRc and CFNRy in TAP.
>
> In case several SSs have been invoked in conjunction with a MOC/MTC
> during a single call, for example Multi Party, it is recommended that
> each SS invocation be recorded in an individual SS event on TAP.
>
> **3.15** **Teleservice** **Category** **Codes**
>
> Teleservice category codes having a description starting with “All”
> (T10, T20, T60) represent attributes which describe the type of
> information and technical features of the Teleservice (Telephony, SMS,
> etc…) being offered to the user through the Telecommunication system.
>
> For example All Speech transmission services (T10) represents the
> Teleservice category for transmission of the following:
>
> •     Telephony (T11) •     Emergency Call (T12)
>
> Teleservice category codes are potentially provided where either the
> network was not able to obtain sufficient information about the
> employed Teleservice or where the Teleservice used was not available
> from the network.
>
> V2.5 Page 26 of 72

GSM Association Confidential - Full, Rapporteur, and Associate
Members<img src="./wwknaqsh.png"
style="width:5.375in;height:2.24167in" />

Official Document TD.58 - TAP3.12 Implementation Handbook **3.16**
**Long** **Term** **Evolution** **(LTE)**

The term LTE has been used to describe the evolution of the radio access
network (RAN) into the Evolved Universal Terrestrial Radio Access
Network (E-UTRAN). On the other hand, SAE (System Architecture
Evolution) has been used to describe the evolution of the core network
into the Evolved Packet Core (EPC) as such, the term Evolved Packet
System (EPS) has been used to describe the combined E-UTRAN and EPC.

The Evolved Packet System represents an all-IP-Network with more
flattened, simple and flexible Network Architecture in comparison with
predecessor networks like 3G UMTS networks.

The EPC consists mainly of five Network Nodes: S-GW, P-GW, MME, PCRF and
HSS.

**3.16.1** **Voice** **and** **SMS** **over** **LTE** **(VoLTE)**

IP Multimedia Subsystem (IMS) has been employed to deliver VoLTE
Services. The EPS needs to communicate with the IMS in order to access
and control VoLTE services delivered by the IMS.

With the endorsed GSMA VoLTE architecture, IMS consists of a whole suite
of network entities which are realised mainly in the HPMN with the
exception of the P-CSCF which resides at the VPMN side as shown in the
below diagram:

> **Figure** **4:** **GSMA** **VoLTE** **Architecture**

On TAP3.12, two new TAP events have been introduced to support VoLTE
traffic:

Mobile Session

> • Messaging Event

Mobile Session is used to support voice traffic over LTE (mobile
originating & mobile termination) and the Messaging Event is used to
support SMS events over LTE (SMS-MO & SMS-MT).

**3.16.2** **Support** **of** **Voice** **on** **CS** **and** **LTE**

V2.5 Page 27 of 72

> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> VoLTE charging information will not be available from a single network
> CDR (like the case with the network MOC CDR on the CS domain) instead
> it has to be correlated from different
>
> network CDRs like the S-GW, P-GW and P-CSCF.
>
> The Charging Id is used for the correlation of the network CDRs as it
> represents a unique identifier which is present on the SGSN, S-GW,
> P-GW and P-CSCF.
>
> The Access Correlation Id element on the P-CSCF CDR shall hold the
> Charging Id generated by the P-GW in case LTE has been used as the
> access network which is being connected to the IMS domain.
>
> To illustrate the support for voice on CS versus LTE, the below table
> shows the existing TAP fields for voice over CS and the equivalent TAP
> fields for voice over LTE.

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> V2.5 Page 28 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate
> Members<img src="./0bkda1cs.png"
> style="width:5.63333in;height:1.03333in" />
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||
||
||

> **Table** **12:** **Voice** **over** **LTE** **compared** **to**
> **Voice** **over** **CS**
>
> **3.17** **LTE** **/** **2G-3G** **Packet** **Switched** **Handover**
>
> In case a data bearer session handover scenario has taken place
> between LTE / 2G-3G Packet Switched network technologies, the
> different network call detail records (CDRs) generated for the data
> bearer session needs to be aggregated into one TAP GPRS Call.
>
> The following time line shows a possible handover scenario between LTE
> and 2G-3G Packet switched network:
>
> Example: LTE / 2G-3G PS handover
>
> In the below example, there are different charges for LTE and 2G/3G PS
> (for example for the different bearer technologies, or for different
> level of Quality of Service), which is illustrated by the Call Type
> Levels as follows (wherever it says “Bearer” in this section, that
> could for example be “Technology” or “QoS”):
>
> • Bearer1 with CTL 1,2,3 (10/0/1) is charged at a lower rate • Bearer2
> with CTL 1,2,3 (10/0/2) is charged at a higher rate
>
> Rounding is to 100 KB.
>
> V2.5 Page 29 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> In addition, it is assumed that there are four network CDRs provided
> for the bearer data session which has traversed between LTE and 2G/3G
> with different QoS/technology and
>
> data volumes as follows:
>
> • Partial 1 contains Bearer1: 345kB • Partial 2 contains Bearer2:
> 267kB • Partial 3 contains Bearer1: 987kB • Partial 4 contains
> Bearer2: 123kB
>
> On the aggregation of the four network CDRs, the VPMN can implement
> any of the following two allowed options on the representation of the
> network CDRs on TAP in terms of correlation of the data volumes and
> charging for those data volumes.
>
> Option 1: Chargeable volume total 1722 kB for Bearer1 (that is charged
> at the lower rate, and rounded up to 1800 kB)

||
||
||
||
||
||
||
||
||
||

> **Table** **13;** **Option** **1** **LTE** **/** **2G-3G** **Packet**
> **Switched** **handover** **(Total** **Volume** **for** **Bearer1)**
>
> **<u>Note:</u>** It is important to be noted that the charging for the
> total volume of 1800 KB on the higher rate for Bearer 2 is not allowed
> according to the Charging Principles in BA.27.
>
> Option 2: Population of two Charge Information groups:
>
> • Charge Information group 1: Charge the volume 1400 KB for Bearer1 at
> the lower rate
>
> • Charge Information group 2: Charge the volume 400 KB for Bearer2 at
> the higher rate

||
||
||
||
||
||
||
||
||
||
||

> V2.5 Page 30 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||

> **Table** **14:** **Option** **2** **LTE** **/** **2G-3G** **Packet**
> **Switched** **handover** **(population** **of** **two** **Charge**
> **Information** **groups)**
>
> **Note:** This option 2 could be complicated both for the VPMN to
> implement and for the HPMN to validate.
>
> **3.18** **CS** **Voice** **Partials** **Aggregation**
>
> Network Partial Voice Calls are not allowed to be provided as separate
> MOC Events on TAP. The Network Partial CDRs must always be aggregated
> and provided in a single MOC Event with the complete duration of the
> customer’s call before submitting it on TAP.
>
> Due to the possible occurrence of various types of network activities
> or actions by the network during an ongoing voice call connection;
> Voice Network Partial CDRs can be generated as the result of such
> network activities.
>
> The following represents some examples of network activities or
> actions which can occur during a voice call connection:
>
> • expiry of the partial record timer
>
> • change of location during a connection
>
> • radio link failure and subsequent call re-establishment
>
> The generated Network Partial CDRs belonging to the same call
> connection are identified by the same Call Reference Identifier.
>
> The same principle also applies to all the Network Partial CDRs
> resulting from radio link failure with subsequent call
> re-establishment activity. This is due to the fact that such call
> re-establishment is transparent to the subscriber and the call is not
> considered ended in this case.
>
> The radio link failure may occur due to poor coverage, overloaded site
> or signal quality issues. Further radio link failures during the
> re-establishment of the call may result in generation of additional
> partial records.
>
> Since the Call Reference Identifier is a mandatory field on the
> Network Partial CDR as per the standard 3GPP Specifications; the Call
> Reference Identifier shall always be present on all Network Partial
> CDRs generated as a result of all types of network activities or
> actions.
>
> On the termination of Network Partial CDR ,the table below shows some
> case scenarios on the Cause for Termination value which can be
> presented on a Network Partial CDR as follows:
>
> V2.5 Page 31 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||

> **Table** **15:** **Cause** **of** **Termination** **Values**
>
> Based on the above mentioned, the VPMN shall aggregate any network
> partial records belonging to the same call connection into a single
> TAP CDR based on the Call Reference Identifier.
>
> An example scenario has been described in the following table for the
> establishment of a single call connection to the destination number
> (+4524576831) where six Network Partial CDRs have been generated by
> the network due to the intervention of the following two different
> types of network activities:
>
> • expiry of the partial record timer for CDR Sequences \# 1,2:
>
> • radio link failure with subsequent call re-establishment for CDR
> Sequences \# 3,4,5:

||
||
||
||
||
||
||
||
||

> **Table** **16:** **An** **Example** **scenario** **of** **Network**
> **Partials** **CDRs**
>
> **Notes:**
>
> • As shown in the table above, the Call Reference value remains the
> same unique
>
> identifier on the generated Network Partials CDRs \# 4 ,5 & 6 (due to
> radio link failure with subsequent call re-establishment) because the
> call is not considered ended in such a case.
>
> V2.5 Page 32 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> • Where a new Call Reference identifier value is provided per each of
> the generated
>
> Network Partial CDRs \#4,5,6, or where the Call Reference identifier
> is absent, this would not be considered inline with the 3GPP technical
> specifications. In addition, it would lead to non-compliance with
> BA.12 rules as the Network Partial CDRs would be presented as single
> and separate MOC Events on TAP without aggregation in such a case.
>
> All the six Network Partial CDRS generated from the described example
> scenario shall be aggregated and presented in a single MOC Event on
> TAP as follows:

||
||
||
||

> **Table** **17:** **TAP** **MOC** **Event**
>
> **4** **Common** **Elements** **Implementation**
>
> **4.1** **General** **Rules**
>
> The following are a collection of general implementation rules:
>
> • Only the rules of the TAP release exchanged over the public
> interface apply.
>
> • TD.57 defines the maximum level of validation. Regarding the
> implementation phase and bilateral agreements it is not necessary to
> implement all existing validations.
>
> • Use a tolerant validation for those TAP elements where there is no
> impact to your billing system. Use a strong validation when creating a
> TAP file.
>
> **4.2** **Taxation** **4.2.1** **General**
>
> Tax Information is a group detailing the applicable tax elements for
> the associated Charge. Where there is no tax associated with the
> charge then there should be no group Tax Information present within
> the Charge Information group. For example, TAP files and invoices
> between members of the European Community do not contain VAT by treaty
> agreement and, therefore, any tax information can only reference a
> ‘non tax’ zero (either rate or fixed value), this is obviously
> redundant data which can be misleading and is wasteful both in
> implementation efficiency and TAP file volumes.
>
> **4.2.2** **Handling** **of** **tax** **on** **tax**
>
> The taxable amount in some cases can be larger than the charge amount
> due to some operators applying tax on a charge that already includes
> additional tax (tax on tax). This means that in order to validate the
> taxable amounts within TAP, external data detailing the tax rules of
> the PMN is required. For an example, see section 4.2.3 Tax breakdown,
> Example E.
>
> **4.2.3** **Tax** **Breakdown**
>
> Tax Information is a repeating group containing the Tax Rate Code and
> the Tax Value and, where applicable Taxable Amount. Each occurrence of
> Charge Information may have several tax elements associated with it,
> for example national tax, regional tax, local tax.
>
> V2.5 Page 33 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> There must be one occurrence within Charge Information for each tax
> element associated with the Charge Information.
>
> The total Tax Value for a call is the sum of all the Tax Values
> specified in the Tax Information group. Please note that a summary
> element shall not be present.
>
> Taxable Amount shall not be specified if it is equal to the Total
> Charge, however it is not a severe error to do so.
>
> The below examples will clarify the rules on a call having the
> following Charge Details:
>
> • 00 (Summary Total) • 01 (Airtime)
>
> • 03 (Toll)
>
> There is no differentiation between multiple rate periods. It also
> assumes that the Tax Rate Codes present in the file are as follows:
>
> • 1 (for example VAT @ 17%) • 2 (for example VAT @ 20%) • 3 (for
> example VAT @ 18%) • 4 (for example VAT @ 21%)
>
> **Note**: The examples below show different ‘valid’ ways to breakdown
> the tax details to different taxable amounts. The detail level
> provided for tax breakdown is at the discretion of the sender. The
> only requirement is that the tax value must reconcile with the taxable
> amount and applicable tax rate and that no redundant tax information
> is provided so that the sum of all tax values, irrespectively of the
> charge type, gives the total (invoiceable) tax amount for the whole
> record.
>
> The Charge Type mentioned in the examples is specified under Taxation
> and referred to by the Tax Rate Code.
>
> Example A - Air and Toll subject to the same tax (Tax Rate code 1)
>
> The corresponding tax breakdown section would be as follows:

||
||
||
||
||
||

> **Table** **18:** **Example** **A:** **Relevant** **Tax**
> **Information** **section** **(AIR** **&** **Toll** **subject** **to**
> **same** **tax)**
>
> The Charge Type element is not required, as the tax is not being
> applied to a particular Charge Type. Similarly, the Taxable Amount
> element is not required, as the associated Tax Value and Tax Rate Code
> relate to the total Charge within Charge Information.
>
> Example B - Air and Toll subject to different taxes
>
> V2.5 Page 34 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook The
> corresponding tax breakdown section would be as follows:

||
||
||
||
||
||
||
||
||
||
||

> **Table** **19:** **Example** **B:** **Relevant** **Tax**
> **Information** **section** **(Air** **&** **toll** **subject** **to**
> **different** **taxes)**
>
> Example C - Air and toll subject to different taxes, and different
> rate periods of the call are subject to different tax rates
>
> This could happen, for example, on a long call that crossed midnight
> on a day when tax rates change.
>
> The corresponding tax breakdown section would be as follows:

||
||
||
||
||
||
||
||
||
||

> V2.5 Page 35 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **20:** **Example** **C:** **Relevant** **Tax**
> **Information** **section** **(Air** **&** **toll** **subject** **to**
> **different** **taxes** **&** **rate** **periods** **also**
> **subject** **to** **different** **taxes)**
>
> Example D - Air and toll is not specified, the rate is independent of
> time of day. However, After Midnight calls have no tax applied.
>
> The corresponding tax breakdown section would be as follows:

||
||
||
||
||
||
||

> **Table** **21:** **Example** **D:** **Relevant** **Tax**
> **Information** **section** **(Rate** **independent** **of** **time**
> **of** **day.** **Tax** **not** **applicable** **after** **midnight)**
>
> Example E – Tax on tax
>
> The corresponding tax breakdown section would be as follows:
>
> V2.5 Page 36 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||
||
||

> **Table** **22:** **Example** **E:** **Relevant** **Tax**
> **Information** **section** **(Tax** **on** **tax)** **4.2.4**
> **Fixed** **tax** **based** **on** **duration**
>
> Some countries’ tax legislations require a fixed tax based on the
> duration of the call, instead of being based on the Charge of the
> call. This rare situation is not directly supported by TAP; however, a
> workaround can be used.
>
> This should be done by defining a fixed tax and then specify a tax
> value at the call detail level. As the Tax Value for fixed taxes is
> only specified within Tax Information at the call event level, there
> can be no cross validation of this Tax Value with the Accounting
> Information. There is also no validation of the Tax Value in relation
> to the Taxable Amount for fixed taxes.
>
> Example: Fixed tax based on duration
>
> 5 minute call with 0.1 SDR tax per minute, charged at 0.50 SDR per
> minute. TAP Decimal Places = 3.
>
> The following would result in TAP:

||
||
||
||
||
||
||
||

> V2.5 Page 37 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||
||

> **Table** **23:** **Relevant** **TAP** **elements** **(Fixed** **tax**
> **based** **on** **duration)** **4.2.5** **Tax** **and** **Charge**
> **break** **down** **per** **Charge** **Type**
>
> There are Telecom Operators which breakdown taxes per charge Type in
> TAP to be inline with the Tax regulation in their countries. In this
> case, Taxation information will consist of Tax Rate code, Tax Type,
> Tax Rate and Charge Type. A breakdown of the Charge Detail information
> per Charge Type should be implemented in a similar manner within Call
> Events in order for the HPMN to achieve a successful Tax validation
> based on the applicable Charge Detail information with in Charge
> Information Group.
>
> An example of Taxation breakdown and the corresponding Charge Detail
> breakdown would be as follows:

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> V2.5 Page 38 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **24:** **Relevant** **TAP** **elements** **(Tax** **and**
> **Charge** **per** **Charge** **Type)**
>
> Note: Sufficient information needs to be provided to support
> validation of the Tax Value. The Tax Value must correspond to the Tax
> Rate and Taxable Amount (or Total Charge where no Taxable Amount is
> present). For the purpose of tax validation, there is no
> cross-validation between Taxation, Charge Detail and Tax Information.
>
> **4.3** **Separation** **of** **charges** **within** **a** **call**
>
> The Charge Information group is used to provide the details of the
> charges relating to Basic Service usage within a call. Charges related
> to CAMEL must be separately represented using the CAMEL Invocation Fee
> and related tax, exchange rate and discount groups and elements.
>
> The aim of this section is to provide examples demonstrating the
> separation of charges within call events where CAMEL is used. To avoid
> confusion on how to provide the CAMEL charges, the following examples
> clarify that the charge within the CAMEL Service Used group relates to
> the CAMEL invocation fee only. Where the CAMEL invocation fee is
> charged within mobile originated or mobile terminated calls, the
> charge for the basic service used must not include the CAMEL
> invocation fee. The same applies for CAMEL services used within a GPRS
> call, for example, CAMEL invocation fee must not be included within
> the charge of the GPRS service used and vice versa.
>
> Example A
>
> V2.5 Page 39 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> Visitor subscriber dials short code ‘1122’. CAMEL translates the
> called party number to 352000001 and the call lasts 2 minutes. The
> applicable charge according to the VPMN’s IOT
>
> is 2 SDR. The VPMN operator charges 0.1 SDR per CAMEL invocation
> regardless of the 'level of CAMEL service'.
>
> The VPMN operator will create a MOC event including the following TAP
> elements to separate the IOT and CAMEL charges:

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **25:** **Example** **A:** **Relevant** **TAP** **elements**
>
> Example B
>
> Visitor subscriber calls a number dialling the short code '2510'.
> CAMEL translates the called party number to 352000001. The call is
> answered and lasts for 2 minutes. The called party
>
> then releases the call and a follow on call is made for the visitor
> subscriber to the number 352000002. The call lasts for 1 minute. The
> applicable charge according to the VPMN’s IOT for the two minutes call
> to 352000001 is 2 SDR. The applicable charge for the one-minute call
> to 352000002 is 1 SDR. In addition, the VPMN operator charges 0.1 SDR
> per CAMEL invocation regardless of the 'level of CAMEL service'.
>
> The VPMN operator will create two MOC events in the TAP File. The
> first MOC will include a basic service used group for the telephony
> service and a CAMEL service used group for the CAMEL service and the
> called party number modification. The second MOC will include a basic
> service used group for the telephony service and a CAMEL service used
> group for the CAMEL service and the initiated call forward.
>
> It is important to note that each basic service used group will
> include the charge information for the telephony service used but as
> it is one single CAMEL call, only one occurrence of the CAMEL service
> used will include a CAMEL Invocation Fee.
>
> The VPMN operator will create a first MOC event including the
> following TAP elements to separate the basic service and the CAMEL
> service used and the corresponding charges:
>
> V2.5 Page 40 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **26:** **Example** **B:** **Relevant** **TAP** **elements**
> **(first** **MOC)**
>
> The VPMN operator will create a second MOC event including the
> following TAP elements to separate the basic service and the CAMEL
> service used and the corresponding charges:

||
||
||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **27:** **Example** **B:** **Relevant** **TAP** **elements**
> **(second** **MOC)**
>
> As explained earlier, the second CAMEL service used does not include a
> charge as it is the same CAMEL call and that the invocation fee is
> included in the CAMEL service used within the first MOC event.
>
> V2.5 Page 41 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook **4.4**
> **Dialled** **Digits**
>
> **4.4.1** **Dialled** **Digits** **definition**
>
> The element Dialled Digits is used to identify the real numbers the
> user has pressed on his mobile to make a call before pressing the send
> key. This means that all characters from ‘0’ -‘9’, ‘+’, ‘#’ and ‘\*’
> can be transferred in this element. It is not allowed to modify this
> number during transfer or TAP conversion. Dialled Digits can be used
> to identify the usage of short numbers.
>
> **4.4.2** **Population** **of** **Called** **Number,** **Dialled**
> **Digits** **and** **CAMEL** **Destination** **Number**
>
> The Called Number, Dialled Digits and CAMEL Destination Number are
> crucial for the proper identification of the called party in a mobile
> originated call. Where the VPMN does not populate these data elements
> or populates them incorrectly, the HPMN could not be able to re-rate
> the call accurately.
>
> As in some instances, (hopefully rare) the Called Number and Dialled
> Digits may not be available from the network, TD.57 provides
> corresponding conditionality rules.
>
> In the case of an unsuccessful call attempt, it is allowed to omit the
> Called Number if the Dialled Digits are filled correctly.
>
> In the case of CAMEL Call Forwarding, Dialled Digits data item is
> omitted. The called number has to contain the forwarded number in
> international format (that is the international representation of the
> forwarded number as keyed in by the subscriber). In the CAMEL general
> case, the camel destination has to contain the ‘connected number’
> provided by the CAMEL server represented in international format.
>
> For HPMN re-pricing purposes it is important the VPMN populates the
> CAMEL Destination Number on TAP3 as received from the CAMEL server. In
> particular, this implies:
>
> • The VPMN shall not exchange the CAMEL Destination Number by default
> with the CAMEL Server address for TAP3 creation
>
> • The CAMEL server address will rarely represent the number actually
> connected. For widely spread prepaid roaming implementations based
> upon CAMEL phase 1 which re-route the call at call set-up back to the
> home network, for example, the connected number typically will be the
> address of a gateway MSC in the home network.
>
> International format number
>
> TD.57 references international format number. An ISDN number is said
> to be in international format where its format is as follows:

||
||
||
||

> **Table** **28:** **International** **format**
>
> V2.5 Page 42 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> For example, “33” is the country code for France. “6” is a national
> destination for mobiles in France. “33600120045” is a number
> represented in international format to call a mobile in
>
> France.
>
> Dialled Digits
>
> The Dialled Digits are the digits as dialled on the roamer's mobile.
> The Dialled Digits must always be present where available from the
> network.
>
> **4.4.2.1** **Examples**
>
> Below are some examples, please note that this is not an exhaustive
> set but they are demonstrating population of the various elements. The
> examples assume that the actual dialled digits are available from the
> network.
>
> Example A: MO call to international number (not known whether mobile
> or PSTN)
>
> • Actual dialled digits = +441234123456
>
> • VPMN International Access Code (IAC) = 00 • VPMN Country Code (CC) =
> 33
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||

> **Table** **29:** **Example** **A:** **Relevant** **TAP** **elements**
> **(MOC** **to** **international** **number)**
>
> • Example B: MO call to international number (known to be a mobile
> number) • Actual dialled digits = 00436641234567
>
> •     VPMN IAC = 00 •     VPMN CC = 33
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||

> **Table** **30:** **Example** **B:** **Relevant** **TAP** **elements**
> **(MOC** **to** **international** **mobile** **number)**
>
> V2.5 Page 43 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook Example C:
> MO call to national number (known to be a PSTN number)
>
> • Actual dialled digits = +421249551234 • VPMN IAC = 00
>
> • VPMN CC = 421
>
> The following table shows the contents of the relevant TAP Elements:

||
||
||
||
||
||
||
||
||

> **Table** **31:** **Example** **C:** **Relevant** **TAP** **elements**
> **(MOC** **to** **national** **PSTN** **number)** Example D: MO call
> to national number (known to be a mobile number)
>
> • Actual dialled digits = 0011614141234 • VPMN IAC = 0011
>
> • VPMN CC = 61
>
> The following table shows the contents of the relevant TAP Elements:

||
||
||
||
||
||
||
||
||

> **Table** **32:** **Example** **D:** **Relevant** **TAP** **elements**
> **(MOC** **to** **national** **mobile** **number)** Example E: MO call
> to national number (known to be non geographic number)
>
> • Actual dialled digits = 08001234123456 • VPMN IAC = 00
>
> • VPMN CC = 45
>
> The following table shows the contents of the relevant TAP Elements:

||
||
||
||
||
||

> V2.5 Page 44 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||

> **Table** **33:** **Example** **E:** **Relevant** **TAP** **elements**
> **(MOC** **to** **non-geographic** **national** **number)**
>
> Example F: MO call to national short code (no CAMEL redirection, long
> number equivalent not known)
>
> • Actual dialled digits = 111
>
> •     VPMN IAC = 00 •     VPMN CC = 41
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||

> **Table** **34:** **Example** **F:** **Relevant** **TAP** **elements**
> **(MOC** **to** **national** **short** **code)**
>
> Example G: MO call to international short code (CAMEL redirection to
> long number of unknown type)
>
> • Actual dialled digits = 121 • VPMN IAC = 00
>
> • VPMN CC = 39
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||
||

> **Table** **35:** **Example** **G:** **Relevant** **TAP** **elements**
> **(MOC** **to** **international** **short** **code)**
>
> Example H: MO call to national short code (no CAMEL redirection, long
> number equivalent known, of type non geographic)
>
> V2.5 Page 45 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook • Actual
> dialled digits = 100
>
> •     VPMN IAC = 00 •     VPMN CC = 44
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||

> **Table** **36:** **Example** **H:** **Relevant** **TAP** **elements**
> **(MOC** **to** **national** **short** **code** **&** **long**
> **number** **known)**
>
> Example I: MO call to emergency services (using local access code)
>
> • Actual dialled digits = 911 • VPMN IAC = 011
>
> • VPMN CC = 1
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||

> **Table** **37:** **Example** **I:** **Relevant** **TAP** **elements**
> **(MOC** **to** **emergency** **services** **via** **local**
> **access** **code)**
>
> Example J: MO call to emergency services (using GSM standard access
> code)
>
> • Actual dialled digits = 112 • VPMN IAC = 001, 008
>
> • VPMN CC = 62
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||

> V2.5 Page 46 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||

> **Table** **38:** **Example** **J:** **Relevant** **TAP** **elements**
> **(MOC** **to** **emergency** **services** **via** **GSM**
> **standard** **access** **code)**
>
> Example K: MO call with CAMEL re-direction
>
> • Actual dialled digits = +447879706543
>
> • Number returned by the CAMEL server = 436641234020 • VPMN IAC = 00
>
> •     VPMN CC = 44 •     HPMN CC = 43
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||
||

> **Table** **39:** **Example** **K:** **Relevant** **TAP** **elements**
> **(MOC** **with** **CAMEL** **re-direction)**
>
> Note: the CAMEL Destination Number is the relevant element for
> charging and billing even when the called number is available here.
>
> Example L: MO international call with special characters
>
> • Actual dialled digits = 0039\*3492222 • VPMN IAC = 00
>
> • VPMN CC = 44
>
> The following table shows the contents of the relevant TAP elements:
>
> V2.5 Page 47 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||

> **Table** **40:** **Example** **L:** **Relevant** **TAP** **elements**
> **(International** **MOC** **with** **special** **characters)**
>
> Note: In the above case it is allowed to send the called number only
> with the country code or with the number from the dialled digits
> international format without the ‘\*’ and/or ‘#’.
>
> Example M: MO call with CAMEL international format conversion
>
> • Actual dialled digits = 0664331354 (National numbering plan of home
> operator - no short code)
>
> •     VPMN IAC = 00 •     VPMN CC = 44 •     HPMN CC = 43
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||
||

> **Table** **41:** **Example** **M:** **Relevant** **TAP** **elements**
> **(MOC** **with** **CAMEL** **international** **format**
> **conversion)**
>
> Note: In the above case, the subscriber dials a national numbering
> plan of the HPMN without the HPMN’s CC. The CAMEL Service allows the
> subscriber to dial any national numbering plan without HPMN’s CC
> (CAMEL Destination Number is the translation of dialled digits to
> international format - translation made by the HPMN and International
> format of Camel Destination Number Returned by CAMEL Server). The
> CAMEL Destination Number is the relevant element for charging and
> billing even when the called number is available and same as the CAMEL
> Destination Number.
>
> V2.5 Page 48 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook Example N:
> MO Call Forwarding with CAMEL re-direction
>
> • Actual number keyed in by subscriber for call forwarding = 087543412
> (National numbering plan of visited Operator - no short code)
>
> • VPMN IAC = 00
>
> • VPMN City Dial Prefix = 0 • VPMN CC = 44
>
> • HPMN CC = 43
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||
||

> **Table** **42:** **Example** **N:** **Relevant** **TAP** **elements**
> **(MO** **Call** **Forwarding** **with** **CAMEL** **re-direction)**
>
> Note: In the above case (CAMEL Call Forward), only the Called Number
> will be present and not the Dialled Digits. The Called Number will
> contain the number before modification by CAMEL and the CAMEL
> Destination Number will contain the modified number. This makes it
> clear that CAMEL has modified the called number. The CAMEL Destination
> Number is the relevant element for charging and billing even when the
> called number is available here.
>
> Example O: MO call to local short code not accessible by dialling in
> international format
>
> • Actual number keyed in by subscriber 123 (National numbering plan of
> visited Operator - short code)
>
> •     VPMN IAC = 00 •     VPMN CC = 44
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||

> **Table** **43:** **Example** **O:** **Relevant** **TAP** **elements**
> **(MOC** **to** **local** **short** **code** **not** **accessible**
> **in** **international** **format)**
>
> V2.5 Page 49 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> Example P: MO call with CAMEL Home Routing
>
> • Actual number keyed in by subscriber = 004487543123 • Number
> returned by the CAMEL server = 436641234020 • HPMN IAC = 00
>
> •     HPMN CC = 43 •     VPMN CC = 44
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||
||

> **Table** **44:** **Example** **P:** **Relevant** **TAP** **elements**
> **(MOC** **with** **CAMEL** **Home** **Routing)**
>
> Note: CAMEL server’s implementations should return 436641234020. If it
> would return 6641234020 and the call was successfully routed by the
> VPMN locally and the VPMN does not format the number in international
> representation in TAP, there is the danger that HPMN will assume that
> the call was routed to a country with destination code 66. In other
> words, the VPMN has to support the formatting of the CAMEL destination
> in the international format. The CAMEL Rerouting Number should be
> available in RAEX IR21 of HPMN.
>
> Example Q: MO call with VPN Service
>
> • Actual number keyed in by subscriber = 837031
>
> • Number returned by the CAMEL server = 393356337031 • VPMN IAC = 00
>
> •     VPMN CC = 44 •     HPMN CC = 39
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||
||

> V2.5 Page 50 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> **Table** **45:** **Example** **Q:** **Relevant** **TAP** **elements**
> **(MOC** **with** **VPN** **service)**
>
> Note: Should the VPMN populate the Camel Destination Number with
> 39837031, the call can be rejected because the number is different
> from what the HPMN Camel Server returned even if the Charge is
> correct.
>
> Example R: MO call to international short code with CAMEL re-direction
>
> • Actual number keyed in by subscriber = 2267 • Number returned by the
> CAMEL server = 2267 • VPMN IAC = 00
>
> •     VPMN CC = 44 •     HPMN CC = 39
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||
||

> **Table** **46:** **Example** **R:** **Relevant** **TAP** **elements**
> **(MOC** **to** **international** **short** **code** **with**
> **CAMEL** **re-direction)**
>
> Example S: MO call to international short code that has experienced
> ‘Default Handling’ by the Visited Network due to inability to
> establish the Call Event through the CAMEL Server in the Home Network
>
> • Actual number keyed in by subscriber = 2241
>
> • Number returned by the CAMEL server = No routed number returned by
> the HPMN’s CAMEL Server.
>
> •     VPMN IAC = 00 •     VPMN CC = 44 •     HPMN CC = 39
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||

> V2.5 Page 51 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||

> **Table** **47:** **Example** **S:** **Relevant** **TAP** **elements**
> **(MOC** **to** **international** **short** **code** **with**
> **‘Default** **Handling’)**
>
> Note: CAMEL Destination Number data item will not be present in case
> the Call Event has experienced ‘Default Handling’ as indicated by the
> presence of the Default Call Handling Indicator in the TAP record.
>
> **4.5** **Population** **of** **Calling** **Number** **on** **MTCs**
> **within** **TAP**
>
> The calling number is the number from which the call was originated in
> the case of mobile terminated calls. For SMS MT this item must contain
> the SMSC address. The calling number must be presented in
> international format within group Call Originator where available from
> the network. For technical reasons the calling number is sometimes not
> available from the network. In this case the calling number must not
> be populated with a default number. In some other cases the calling
> number can be delivered by the network or carriers incorrectly. The
> HPMN may opt to use a home CDR for retail billing purposes and not use
> the TAP MTC record.
>
> **4.6** **Population** **of** **call** **duration** **and**
> **timestamps** **for** **charging** **(MOCs** **and** **MTCs)**
>
> Where call charges only relate to the call answer time then the Call
> Event Start Timestamp will normally be populated with the call answer
> time and not the channel seizure time.
>
> Due to certain technical constraints this may not always be possible
> or cost effective to implement so, to support these exceptional cases,
> TAP has been configured to allow for the population of Call Event
> Start Timestamp with channel seizure time even where this does not
> relate to the start of charging. It should be noted that this usage
> could lead to some TADIG testing completion difficulties with a few
> potential roaming partners where they may not be able to accommodate
> this exception in TAP files received.
>
> Where a call has any charges relating to the channel seizure time then
> the Call Event Start Timestamp must contain the channel seizure time.
> This is true even where there are other charges within the call that
> relate to the call answer time, for example where a call set up charge
> is made for channel seizure and then duration is charged from call
> answer.
>
> The Total Call Event Duration must always contain the call duration
> calculated from the call end time (channel release) minus the Call
> Event Start Timestamp.
>
> For the same call scenario it is the charging model (IOT) that will
> determine which values are valid for which data items.
>
> Example A:
>
> VPMN X charges for duration from call answer to the end of the call.
> There is no other charge for the call. The duration is chargeable at 2
> SDR per minute, unitised per 30 seconds.
>
> • Channel Seizure Timestamp • Call Answer Timestamp

20090517152130

20090517152141

> V2.5 Page 52 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook • Call End
> Timestamp 20090517152703
>
> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **48:** **Example** **A:** **Relevant** **TAP** **elements**
> **(Duration** **charged** **from** **call** **answer** **to** **end**
> **of** **call)**
>
> Example B:
>
> VPMN X charges for duration from call answer to the end of the call.
> There is no other charge for the call. The duration is chargeable at 2
> SDR per minute, unitised per 30 seconds.
>
> • Channel Seizure Timestamp • Call Answer Timestamp
>
> • Call End Timestamp

20090517152130 20090517152141

20090517152703

> VPMN X implementation uses the exceptional case (see above)
>
> The following table shows the contents of the relevant TAP elements

||
||
||
||
||
||
||
||
||
||

> V2.5 Page 53 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||

> **Table** **49:** **Example** **B:** **Relevant** **TAP** **elements**
> **(Duration** **charged** **from** **call** **answer** **to** **end**
> **of** **call)**
>
> Example C:
>
> VPMN X charges for duration from channel seizure to the end of the
> call. There is no other charge for the call. The duration is
> chargeable at 2 SDR per minute, unitised per 30 seconds.
>
> • Channel Seizure Timestamp • Call Answer Timestamp
>
> • Call End Timestamp

20090517152130 20090517152141

20090517152703

> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **50:** **Example** **C:** **Relevant** **TAP** **elements**
> **(Duration** **charged** **from** **channel** **seizure** **to**
> **end** **of** **call)**
>
> Example D:
>
> VPMN X charges a fixed charge for call set up and duration from call
> answer to the end of the call. The call set up is charged at 0.50 SDR,
> fixed charge. The duration is chargeable at 2 SDR per minute, unitised
> per 30 seconds.
>
> V2.5 Page 54 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook • Channel
> Seizure Timestamp 20090517152130
>
> • Call Answer Timestamp • Call End Timestamp

20090517152141

20090517152703

> The following table shows the contents of the relevant TAP elements:

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **51:** **Example** **D:** **Relevant** **TAP** **elements**
> **(Fixed** **charge** **for** **call** **set** **up** **and**
> **duration** **charged** **from** **call** **answer** **to** **the**
> **end** **of** **the** **call)**
>
> Example E:
>
> VPMN X charges a fixed charge for call set up attempt when the call is
> not answered. The call set up attempt is charged at 0.25 SDR, fixed
> charge.
>
> • Channel Seizure Timestamp • Call Answer Timestamp
>
> • Call End Timestamp
>
> the channel release time

20090517152130

not applicable, call not answered

20090517152204 where Call End Timestamp is

> The following table shows the contents of the relevant TAP elements:
>
> V2.5 Page 55 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> **Table** **52:** **Example** **E:** **Relevant** **TAP** **elements**
> **(Fixed** **charge** **for** **call** **set** **up** **when**
> **call** **not** **answered)**
>
> **4.7** **Population** **and** **Validation** **of** **Exchange**
> **Rates**
>
> Exchange rate information is populated in the TAP file to document the
> exchange rate used to convert monetary amounts from the Sender’s local
> (IOT) currency to the currency used in the TAP file. BA.11, Billing
> and Accounting Information – Treatment of Exchange Rates, specifies
> detailed rules for determining the exchange rate to be used. TD.57
> includes a validation rule to confirm the exchange rate applied to the
> call event is correct. In the TAP, the exchange rate is expressed as
> the number of units of Local Currency to one unit of the currency used
> in the TAP file.
>
> **4.7.1** **Exchange** **Rates** **Quoted** **by** **the**
> **International** **Monetary** **Fund** **(IMF)**
>
> The International Monetary Fund (IMF) quotes exchange rates between
> several currencies and the Special Drawing Right (SDR). For those
> currencies for which exchange rates are quoted, the rate used in the
> TAP must be to the same level of accuracy as that quoted by the IMF.
> For example, if the IMF quotes an exchange rate to six significant
> digits, the rate used and populated in the TAP must be expressed to
> six significant digits. It is this level of accuracy that will be used
> when performing the TD.57 validation on the exchange rate. The
> exchange rate in the TAP must match the exchange rate quoted by IMF.
>
> Note: The IMF currently adds zeroes wherever required after the six
> significant digits to show all exchange rates with 6 decimal places.
> Those trailing zeroes are not significant, and are only there for
> presentation purposes. For example:
>
> Colombian Peso: 2,938.570000. The exchange rate has been calculated to
> six significant digits and then four zeroes have been added to make it
> six decimal places. These last four zeroes are not significant.
>
> In exceptional cases, a tolerance is needed by systems validating
> exchange rates where the sender due to billing system limitations is
> not able to support the same number of significant digits as published
> by the IMF.
>
> V2.5 Page 56 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook

In such cases, the Recipient must allow for a tolerance to support the
fact that the Sender can round either up or down to the nearest value
that can be defined using a minimum of 5

significant digits.

Please see TD.57, data item Exchange Rate, for examples and details on
the exchange rate’s rounding and tolerance.

Exchange rates in TAP must be expressed as a minimum with five
significant digits. It is however allowed to exclude trailing zeroes in
TAP (although that could strictly speaking mean that less than five
significant digits are present).

For example (not conclusive), if the exchange rate published by the IMF
is 2,938.570000, the TAP fields can be populated in the following ways:

> • Exchange Rate: 293857, Number of Decimal Places: 2 • Exchange Rate:
> 293850, Number of Decimal Places: 2 • Exchange Rate: 29385, Number of
> Decimal Places: 1 • Exchange Rate: 293860, Number of Decimal Places: 2
> • Exchange Rate: 29386, Number of Decimal Places: 1
>
> • Exchange Rate: 293857000, Number of Decimal Places: 5

**4.7.2** **Exchange** **Rates** **Not** **Quoted** **by** **the**
**IMF**

BA.11 specifies rules on how exchange rates for currencies not quoted by
the IMF are to be calculated. In this case, the exchange rate is
calculated by using the exchange rate from US Dollars (USD) to the local
currency, then using the rate from SDR to USD as quoted by the IMF. For
such currencies, the exchange rate must be expressed in minimum five
significant digits in TAP. It is however allowed to exclude trailing
zeroes in TAP (although that could strictly speaking mean that less than
five significant digits are present). For validation purposes, a minimum
tolerance of two units on the fifth significant digit must be allowed by
the recipient, to allow for differences in how the exchange rate is
reduced to the five significant digits (for example, rounding or
truncating).

For example, if the Sender’s currency is Hong Kong Dollar (HKD), which
does not have an SDR exchange rate quoted by the IMF, the exchange rate
would be calculated by using the USD to HKD exchange rate, and then
using the SDR to USD exchange rate quoted by the IMF.

Example:

> • USD to HKD exchange rate = 7.77305 (1 USD = 7.77305 HKD)
>
> • SDR to USD exchange rate = 1.47816 (1 SDR = 1.47816 USD) • Exchange
> rate for TAP is calculated as:
>
> • 7.77305 x 1.47816 = 11.489811588
>
> • The result can be reduced to five significant digits by rounding or
> truncating: • 11.490 (rounded)
>
> • 11.489 (truncated)

V2.5 Page 57 of 72

> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> When validating the exchange rate in the TAP, when the recipient
> calculates the exchange rate and compares it to the exchange rate in
> the TAP file, the recipient must allow at least
>
> two units of variance on the fifth significant digit.
>
> If the recipient used rounding when determining expected exchange rate
> (11.490) it must consider any exchange rate between (and including)
> 11.488 and 11.492 as valid.
>
> If the recipient used truncation when determining expected exchange
> rate (11.489), it must consider any exchange rate between (and
> including) 11.487 and 11.491 as valid.
>
> In practice this means that exchange rates between (and including)
> 11.488 and 11.491 are always valid.
>
> For example (not conclusive), if the recipient has calculated the
> exchange rate to 11.489811588, TAP files containing the following
> values cannot be rejected:
>
> • Exchange Rate: 11489811599, Number of Decimal Places: 9 • Exchange
> Rate: 114881234, Number of Decimal Places: 7
>
> • Exchange Rate: 114898, Number of Decimal Places: 4 • Exchange Rate:
> 1148980, Number of Decimal Places: 5 • Exchange Rate: 11489, Number of
> Decimal Places: 3
>
> • Exchange Rate: 11490, Number of Decimal Places: 3 • Exchange Rate:
> 1149, Number of Decimal Places: 2
>
> Note: The last example (1149) is actually only 4 significant digits
> from a mathematical perspective. However, as 11490 must be accepted,
> then 1149 must also be accepted as the resulting value of the TAP
> records are exactly the same.
>
> **4.7.3** **Significant** **Digits** **and** **Decimal** **Places**
>
> Significant digits and Decimal Places are used on defining the
> accuracy and precision of the pegged exchange rate value as described
> in BA.11 and on populating and validating the Exchange Rate in TAP as
> defined in TD.57.
>
> In order to avoid misinterpretations this section explains the meaning
> of Significant digits, Decimal Places and the difference between them.

**4.7.3.1** **Significant** **digits**

> In the context of TAP, the significant digits of a number are defined
> as follows:
>
> Starting from left to right, the first non-zero digit is the first
> significant digit. Leading zeroes are not counted as significant
> digits.
>
> The last significant digit is the last digit in the number. Trailing
> zeroes to the right of the decimal point are not significant digits on
> validating by TAP although this is not inline with the mathematical
> definition of significant digits.
>
> For example:
>
> • 6.000 is one significant digit • 0.057 is two significant digits
>
> V2.5 Page 58 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook • 11.90 is
> three significant digits
>
> •     01600 is four significant digits •     1.0456 is five
> significant digits

**4.7.3.2** **Decimal** **Places**

> The Decimal Places indicates the number of fractional digits following
> on the right side of the decimal point.
>
> For Example:
>
> • 0.075 has three decimal places • 1.08300 has five decimal places •
> 1.257646 has six decimal places

**4.7.3.3** **Significant** **Digits** **vs.** **Decimal** **Places**

> Several examples are shown below in order to clearly distinguish
> between Significant digits and Decimal Places:
>
> • 0.123456 is 6 significant digits and also 6 decimal places • 123.456
> is 6 significant digits but only 3 decimal places
>
> • 123.450000 is 5 significant digits and 6 decimal places
>
> **4.8** **Updating** **the** **Local** **Currency** **in** **TAP**
>
> The Local Currency present within Accounting Information Group must be
> the same as the one defined in the VPMN’s IOT. In case an Operator
> decided to change the Local Currency in its IOT, the Local Currency
> data item in TAP must be updated and become effective on the same
> corresponding date as the new VPMN’s IOT.
>
> Operators should maintain a clear split in the TAP-OUT traffic stream
> between the old and the new Local Currency used by the TAP-OUT files.
> An appropriate cut off date (for example, midnight time) can be set up
> in the billing system in order to enforce the separation between the
> old and new Local Currency usage. This is important as only one Local
> Currency is allowed per TAP file where all Call Events within a TAP
> file must be related to the defined TAP file Local Currency.
>
> In the event where the Local Currency in the TAP file does not match
> with the Local Currency defined in the VPMN’s IOT, the Call Events
> will be subject to rejection as the Call Event Charges (based on the
> exchange rate calculations between the Local Currency and TAP Currency
> as set in the TAP File) will not match with the defined IOT’s Tariff
> in this case.
>
> It is essential that any late received Call Events made on dates in
> relation to the old Currency (based on the Call Event/Partial date &
> time) should be provided in a separate TAP file where the Local
> Currency element is populated with the old Local Currency as defined
> in the old IOT. On the other hand, all Call Events made on dates in
> relation to the new Currency (based on the Call Event/partial date &
> time) will be provided in a separate TAP files stream where the Local
> Currency element is populated with the new Local Currency as defined
> in the new IOT.
>
> V2.5 Page 59 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> **4.9** **Population** **of** **high** **and** **low** **values**
> **in** **Charge** **and** **Total** **Charge** **elements**
>
> The Charge and Total Charge elements may contain very high or low
> values due to the extensive or low usage of services, such as HSPA. It
> is recommended that the TAP Sender does not use a large number of TAP
> decimal places. For high values a large number of TAP decimal places
> could potentially cause the charge to exceed the maximum positive
> integer value that can be encoded within the defined element sizes.
> Where the maximum positive integer value is exceeded this may result
> in a negative value on decoding the content of the elements where the
> left most bit is set to 1. For low values a small number of TAP
> decimal places could cause sessions with low traffic usage to be zero
> charged if truncation is used instead of rounding.
>
> It is generally recommended to use 3 TAP Decimal Places.
>
> The table below shows the highest and lowest possible values for
> Charge and Total Charge given the number of TAP decimal places used.

||
||
||
||
||
||
||
||

> **Table** **53:** **Highest** **and** **lowest** **possible**
> **values** **for** **Charge** **and** **Total** **Charge** **by**
> **TAP** **Decimal** **Places**
>
> Where the roaming relationship allows both very high and very low
> charges the above model may not support accurate charge
> representations within a single TAP file. In these cases it may be
> necessary to put the charge records into separate TAP files, each TAP
> file having the appropriate number of TAP Decimal Places to allow for
> accurate charge representation.
>
> **4.10** **Discrepancy** **of** **Calculated** **Tax** **values**
> **between** **TAP** **and** **Invoice**
>
> It is very likely that the sum of all taxes from TAP files (which is
> the sum of applied taxes to each single charge) will not match the
> invoice tax value if this is applied to the overall charge. This can
> occur due to various reasons as for example due to rounding rules, tax
> jurisdiction or currency conversion reasons.
>
> In order to reduce discrepancy and reach a more precise value between
> the calculated tax on TAP and the invoice, the TAP Sender may choose
> to use more than 3 TAP Decimal Places.
>
> **4.11** **IOT** **Validation** **Examples**
>
> This section provides examples for IOT validations. It is related to
> validation rule 200 on Charge.
>
> V2.5 Page 60 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook
>
> The given IOT validation examples are in line with section 5.8 of
> TD.57, defining the Charge Validation Procedure.
>
> **Note:** Although this TAP Implementation Handbook refers to TAP 3.12
> the given IOT validation examples within this section as well as
> section 5.8 in TD.57 is applicable to all TAP 3 releases.
>
> **Note:** Error 20 on Call Type Level 2, is not IOT related, however
> examples are given in this section.
>
> IOT Example 1 is from a VPMN with Country Code 99, charge independent
> on call time. The IOT includes the following information (subset),
> included fully defined Call Type Levels:

||
||
||
||
||
||
||
||
||
||
||
||

> The following table shows call scenarios and possible CDR rejections
> due to the IOT related error codes mentioned above, if appropriate.
> All duration based examples assume a call duration of 60 seconds. All
> volume based examples assume a transferred volume of 1 MB.

||
||
||
||
||
||
||
||
||
||
||
||
||

> V2.5 Page 61 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||
||
||
||
||

> IOT Example 2 is from a VPMN with Country Code 99, charge independent
> on call time. The IOT includes the following information (subset), but
> does not include Call Type Levels.
>
> **Note:** This second IOT is an example of an invalid IOT as the Call
> Type Levels have not been defined. It is however a common scenario and
> the purpose is to explain what can be rejected in TAP, not what IOTs
> should be accepted. As the IOT does not include Call Type Levels it
> must not apply differential charging for MTC and GPRS scenarios unless
> technical parameters are used for the differentiation.Thus an IOT like
> Example 1 is not applicable. Parties issuing IOTs without Call Type
> Levels, but with differential charging for MTC and GPRS scenarios take
> a risk to get rejections for all MTC (except zero charged) and all
> GPRS CDRs (except where verification is possible by pure technical
> parameter usage, for example by APN).

||
||
||
||
||
||
||
||
||
||

> The following table shows call scenarios and possible CDR rejections
> due to the IOT related error codes mentioned above, if appropriate.
> All duration based examples assume a call duration of 60 seconds. All
> volume based examples assume a transferred volume of 1 MB.
>
> V2.5 Page 62 of 72
>
> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> **4.12** **Network** **Node** **Sharing**
>
> The Network Node Sharing in relation to different services,
> geographical areas or countries is a common practice for some
> Operators. It supports Telecom Operators to reduce CAPEX/OPEX
> expenditure in network infrastructure and equipments.
>
> Since Network Node Sharing may represent an impact on Wholesale and
> Retail billing, the purpose of this section is to describe the
> different scenarios affected by Network Node Sharing and the possible
> solutions to avoid any operational problems on Wholesale or Retail
> billing.
>
> **4.12.1** **MSC** **Sharing** **for** **MOC/MTC** **Voice** **Calls**
> **and** **SMS** **Events**
>
> **4.12.1.1** **MSC** **Sharing** **between** **Terrestrial** **/**
> **Non** **terrestrial** **network**
>
> Where a Host Operator (Terrestrial or Non-Terrestrial Operator)
> extends its network coverage into International Zones e.g.
> International Waters or International Airspace, the extension of the
> network is known as the Client Operator where it can be considered a
> Non-Terrestrial Network Extension.
>
> V2.5 Page 63 of 72

GSM Association Confidential - Full, Rapporteur, and Associate
Members<img src="./udfgxql5.png"
style="width:6.26708in;height:4.23611in" />

Official Document TD.58 - TAP3.12 Implementation Handbook

In such cases, MSC nodes must be identified using independent E.164
addresses or ranges of MSC / VLRs. This means that separate ranges of
MSC Global Titles and Mobile Station

Roaming Numbers (MSRNs) must be used for each independent
non-terrestrial network extension and must be different from the host
network MSC Global Titles and MSRN ranges. Please refer to PRD BA.46 for
further details on Network Extensions rules and regulations.

> **Figure** **5:** **Split** **of** **MSC** **GT** **and** **MSRN**
> **ranges**

**4.12.1.2** **MSC** **Sharing** **between** **different**
**geographical** **zones** **/** **areas**

There are some GSM Operators offering services in different areas that
could be different countries or different zones within the same country.

Where the extended network extensions belongs to different countries, a
distinct TAP code, MSRN ranges and MSC Global Titles must be completely
independent per each network extension.

On the other hand, where the area differentiation is within the same
country only, the Serving Location Description within the TAP Events
represents the only means to differentiate the traffic at the Wholesale
level as the TAP codes, MSRN ranges and Global Titles could be the same
in such case.

V2.5 Page 64 of 72

<img src="./uzj1swjf.png"
style="width:5.94167in;height:2.825in" />GSM Association Confidential -
Full, Rapporteur, and Associate Members Official Document TD.58 -
TAP3.12 Implementation Handbook

> **Figure** **6:** **Split** **of** **TAP** **Traffic** **Stream**
> **per** **each** **PMN**

**4.12.2** **SGSN** **Sharing** **between** **two** **or** **more**
**Network** **Operators**

SGSN sharing represents the sharing of the same SGSN IP Address among
more than one Operator or between a Host Operator and its Client network
extension. In such case, a severe impact is highly expected on the
wholesale and Retail billing operational processes.

In case the SGSN is shared between two Operators PMN1 and PMN2, the
VPMN’s billing system must be capable of distinguishing the PS data
traffic generated by each network in order to insert the raised CDR
Events in two separate TAP files streams per each TAP Code. The
wholesale billing could be performed without any problems where such
requirements are fulfilled by the visited network.

SGSN IP address sharing could cause some operational billing problems at
retail level for those cases in which Home network uses real time
charging as for example DIAMETER or uses its own network GGSN CDRs to
charge its end Subscribers. The real problem is more evident if the SGSN
is shared between operators belonging to different countries. This is
due to the fact that real time charging platforms or retail billing
systems uses SGSN IP address to identify the origin of the PDP context
where it identify the country in which the roaming subscriber was
connected to the PS network.

In case the HPMN is not capable of differentiating the IP Address where
a single IP range is used, there will be no way to differentiate whether
the PS traffic is originated from one visited network or another. As a
result, the retail billing would not be performed in a proper way and it
could raise customer claims where it could ultimately leads to revenue
reduction for the home operator.

Therefore, SGSN IP Addresses ranges must be differentiated for host
network and for each

network extension. In addition, the IP Address ranges per each PMN the
corresponding IR.21 document.

V2.5

must be described in

> Page 65 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members
Official Document TD.58 - TAP3.12 Implementation
Handbook<img src="./14bydfug.png"
style="width:6.175in;height:3.95833in" />

> **Figure** **7:** **Split** **of** **SGSN** **IP** **Address**
> **ranges** **per** **each** **PMN**

**4.12.3** **IR.21** **Information** **Required**

IR.21 Document is necessary for the proper retail billing. There are
many situations in which IR.21 is updated with new relevant information
for retail billing but the billing systems themselves are not updated
because it is difficult sometimes to coordinate all the relevant changes
for all the roaming partners.

TADIG billing teams within the Organization at the HPMN side could
analyze the IR.21 Information in order to find the relevant information
required for the wholesale and retail billing and to inform the
corresponding IREG/Network teams at the VPMN side about the correction
of any information within the IR.21 that would have an impact on the
billing processes. With the introduction of GSMA InfoCentre2, it
provides the means to alert TADIG/billing teams at the HPMN side when a
relevant parameter of IR.21 is updated or modified and thus it serves as
a very helpful means in maintaining data synchronization and in
improving the communication between the IREG and TADIG teams within both
the VPMN and HPMN Organizations.

> • Relevant Information contained in IR.21 document for wholesale /
> retail charging: • MSC / VLR Global title ranges
>
> • MSRN Ranges
>
> • SMSC GT Address
>
> • CAMEL Re-routing numbers (CAMEL Destination Number in TAP) • SGSN IP
> Address ranges

V2.5 Page 66 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook

All these technical parameters contained in the IR.21 could be critical
for Wholesale/Retail billing systems. Therefore, the presence of working
procedure to inform about all IR.21

updates to the “Billing Team” of each Operator could be very useful to
prevent severe impact on the Wholesale/Retail billing.

**4.12.4** **Usage** **of** **Location** **Information** **for**
**Serving** **Network** **Identification**

As described in PRD IR.33, the Routing Area Identity (RAI) and User
Location Information represents an alternative way to identify the
serving Operator in case of SGSN IP Address Sharing but it is less
likely to be employed by the HPMN for the following reasons:

> • It represents more work and complexity on the HPMN’s billing system
> to perform further analysis of the RAI and ULI in case there is no
> VPMN’s SGSN IP Address range split.
>
> • The RAI and ULI are not mandatory parameters according to the 3GPP
> specification so it could be risky to use them for retail billing.
>
> • SGSN IP range identification represents a more simple method to
> identify the visited network

While SGSN IP Sharing represents a simplified implementation method for
the visited network, it produces an increased complexity on the Home
Operator’s retail billing system to separate the PS Data traffic
according to the Serving network.

**4.12.5** **Identification** **of** **Host/Network** **Extension**
**for** **Retail** **Billing** **Process**

The following table lists the different options of billing solutions
that the HPMN can employ for Retail Billing and the Network elements
that can be used to identify the VPMN’s traffic streams whether it
belongs to the Host Network or Network Extension per each Option.

||
||
||
||

V2.5 Page 67 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||

> **Table** **54:** **Options** **of** **Billing** **Solutions** **for**
> **Retail** **Billing**

**5** **Change** **Request** **Impact** **Classification**

The impact of each change request is classified by the use of Impact
Class. A change request Impact Class can take values 1, 2, 3 or 4
defined as follows:

**5.1** **Impact** **class** **4**

Class 4 will designate change requests where major impact on existing
application logic and systems interfaced with TAP handling is expected.
Those changes go beyond simple ASN.1 syntax changes. It is expected that
almost every software system dealing with TAP files will

V2.5 Page 68 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook

require upgrades to support implementation of CRs of class 4. Typical
CRs belonging to this class would be for example those:

> • Adding new mandatory data elements which are derived from network •
> Changing of mandatory data elements which are derived from network •
> Support for new services

**5.2** **Impact** **class** **3**

Class 3 will designate change requests, which have direct impact on the
physical layer (ASN.1) of TAP files. It is expected that almost every
software system dealing with TAP files will require upgrades to support
implementation of CRs of class 3. Typical CRs belonging to this class
would be for example those:

> • Adding new billing/rating elements or removing existing ones •
> Changing names or structure of existing elements
>
> • Changing optionality of existing elements

**5.3** **Impact** **class** **2**

Class 2 will designate change requests, which have direct impact on the
logical level of TAP files. It is expected that the majority of software
systems dealing with TAP files will require upgrades to support
implementation of CRs of class 2. Nevertheless, since TAP standards
define the highest level of validations a party may apply (which is not
though mandatory), it might be the case that a subset of CRs of this
class may not have specific impact on systems using lower levels of
validations. Typical CRs belonging to this class would be for example
those:

> • Adding new validations or removing existing ones • Changing severity
> of errors

**5.4** **Impact** **class** **1**

Class 1 will designate change requests which are expected to have no or
minimum impact on systems handling TAP procedures. It is expected that
the majority of software systems dealing with TAP files will not require
any kind of upgrades to support implementation of CRs of class 1.
Typical CRs belonging to this class would be for example:

> • Editorial or cosmetic change requests • Clarification change
> requests

V2.5 Page 69 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members
Official Document TD.58 - TAP3.12 Implementation Handbook

**Annex** **A** **Document** **Management**

**A.1** **Document** **History**

||
||
||
||
||
||
||
||
||
||
||

V2.5 Page 70 of 72

GSM Association Confidential - Full, Rapporteur, and Associate Members

Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||
||
||
||
||
||
||
||

V2.5 Page 71 of 72

> GSM Association Confidential - Full, Rapporteur, and Associate Members
>
> Official Document TD.58 - TAP3.12 Implementation Handbook

||
||
||
||
||
||
||

> **Other** **Information**

||
||
||
||
||

> It is our intention to provide a quality product for your use. If you
> find any errors or omissions, please contact us with your comments.
> You may notify us at [<u>prd@gsma.com</u>](mailto:prd@gsma.com)
>
> Your comments or suggestions & questions are always welcome
>
> V2.5 Page 72 of 72
