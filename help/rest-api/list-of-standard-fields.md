---
title: "Standard Fields"
feature: REST
---

# Standard Fields

Here is a list of standard fields available in Marketo that are accessible via the API.

You can retrieve the list of all supported field names available on your lead records by using the REST [Describe Lead](https://developers.marketo.com/documentation/rest/describe/) endpoint.

| REST API Name | SOAP API Name | Friendly Label | Description |
| --- | --- | --- | --- |
| address | Address | Address | Lead's address |
| annualRevenue | AnnualRevenue | Annual Revenue | Annual Revenue of the lead's company |
| anonymousIP | AnonymousIP | Anonymous IP | IP address of the lead's first recorded web visit |
| billingCity | BillingCity | Billing City | City of the lead's billing address |
| billingCountry | BillingCountry | Billing Country | Country of the lead's billing address |
| billingPostalCode | BillingPostalCode | Billing Postal Code | Postal code of the lead's billing address |
| billingState | BillingState | Billing State | State or province of the lead's billing address |
| billingStreet | BillingStreet | Billing Address | Billing street address of the lead's company |
| city | City | City | Lead's city |
| company | Company | Company Name | Lead's company name |
| country | Country | Country | Lead's country |
| dateOfBirth | DateofBirth | Date of Birth | Lead's date of birth |
| department | Department | Department | Lead's department in their company |
| doNotCall | DoNotCall | Do Not Call | Lead's do-not-call preference |
| doNotCallReason | DoNotCallReason | Do Not Call Reason | Explanation for lead's do-not-call preference |
| email | Email | Email Address | Lead's email address. Standard Marketo key field for lead records |
| fax | Fax | Fax Number | Lead's fax number |
| firstName | FirstName | First Name | Lead's first name |
| industry | Industry | Industry | Lead's Industry |
| inferredCompany | InferredCompany | Inferred Company | Company name inferred by reverse IP lookup of the lead's first recorded web visit |
| inferredCountry | InferredCountry | Inferred Country | Country inferred by reverse IP lookup of the lead's first recorded web visit |
| lastName | LastName | Last Name | Lead's Last Name |
| leadRole | LeadRole | Role | Lead's role in their company |
| leadScore | LeadScore | Lead Score | Integer score awarded to the lead by scoring campaigns and programs |
| leadSource | LeadSource | Lead Source | Field recording what source the lead originated from |
| leadStatus | LeadStatus | Lead Status | Field recording the current marketing/sales status of the lead |
| mainPhone | MainPhone | Main Phone | Primary phone number of the lead's company |
| jigsawContactId | Marketo Jigsaw Contact Id | Marketo Data.com ID | Lead's Data.com ID if available |
| jigsawContactStatus | Marketo Jigsaw Contact Status | Marketo Data.com Status | Lead's Data.com status if available |
| facebookDisplayName | MarketoSocialFacebookDisplayName | Marketo Social Facebook Display Name | Lead's Facebook display name. System populated during social sign-in |
| facebookId | MarketoSocialFacebookId | Marketo Social Facebook Id | Lead's Facebook Id. System populated during social sign-in |
| facebookPhotoURL | MarketoSocialFacebookPhotoURL | Marketo Social Facebook Photo URL | URL of lead's Facebook profile photo. System populated during social sign-in |
| facebookProfileURL | MarketoSocialFacebookProfileURL | Marketo Social Facebook Profile URL | URL of lead's Facebook profile. System populated during social sign-in |
| facebookReach | MarketoSocialFacebookReach | Marketo Social Facebook Reach | The Facebook reach of the lead. System populated during social sign-in |
| facebookReferredEnrollments | MarketoSocialFacebookReferredEnrollments | Marketo Social Facebook Referred Enrollments | Number of referred enrollments attributed to the lead through Facebook. System managed |
| facebookReferredVisits | MarketoSocialFacebookReferredVisits | Marketo Social Facebook Referred Visits | Number of referred visits attributed to the lead through Facebook. System managed |
| gender | MarketoSocialGender | Marketo Social Gender | Gender of the lead. System populated during social sign-in |
| lastReferredEnrollment | MarketoSocialLastReferredEnrollment | Marketo Social Last Referred Enrollment | Date of last completed referral. System managed |
| lastReferredVisit | MarketoSocialLastReferredVisit | Marketo Social Last Referred Visit | Date of last referred visit. System managed |
| linkedInDisplayName | MarketoSocialLinkedInDisplayName | Marketo Social LinkedIn Display Name | Lead's LinkedIn display name. System populated during social sign-in |
| linkedInId | MarketoSocialLinkedInId | Marketo Social LinkedIn Id | Lead's LinkedIn Id. System populated during social sign-in |
| linkedInPhotoURL | MarketoSocialLinkedInPhotoURL | Marketo Social LinkedIn Photo URL | Lead's LinkedIn photo URL. System populated during social sign-in |
| linkedInProfileURL | MarketoSocialLinkedInProfileURL | Marketo Social LinkedIn Profile URL | Lead's LinkedIn profile. System populated during social sign-in |
| linkedInReach | MarketoSocialLinkedInReach | Marketo Social LinkedIn Reach | Lead's LinkedIn reach. System populated during social sign-in |
| linkedInReferredEnrollments | MarketoSocialLinkedInReferredEnrollments | Marketo Social LinkedIn Referred Enrollments | Number of referred enrollments attributed to the lead through LinkedIn. System managed |
| linkedInReferredVisits | MarketoSocialLinkedInReferredVisits | Marketo Social LinkedIn Referred Visits | Number of referred visits attributed to the lead through LinkedIn. System managed |
| syndicationId |  - | Marketo Social Syndication ID | Lead's internal Marketo Social Id. System managed |
| totalReferredEnrollments | MarketoSocialTotalReferredEnrollments | Marketo Social Total Referred Enrollments | Total number of completed referral enrollments attributed to the lead |
| totalReferredVisits | MarketoSocialTotalReferredVisits | Marketo Social Total Referred Visits | Total number of referred visits attributed to the lead |
| twitterDisplayName | MarketoSocialTwitterDisplayName | Marketo Social Twitter Display Name | Lead's Twitter display name. System populated during social sign-in |
| twitterId | MarketoSocialTwitterId | Marketo Social Twitter Id | Lead's Twitter Id. System populated during social sign-in |
| twitterPhotoURL | MarketoSocialTwitterPhotoURL | Marketo Social Twitter Photo URL | Lead's Twitter photo URL. System populated during social sign-in |
| twitterProfileURL | MarketoSocialTwitterProfileURL | Marketo Social Twitter Profile URL | Lead's Twitter profile URL. System populated during social sign-in |
| twitterReach | MarketoSocialTwitterReach | Marketo Social Twitter Reach | Lead's Twitter reach. System populated during social sign-in |
| twitterReferredEnrollments | MarketoSocialTwitterReferredEnrollments | Marketo Social Twitter Referred Enrollments | Number of referred enrollments attributed to the lead through Twitter. System managed |
| twitterReferredVisits | MarketoSocialTwitterReferredVisits | Marketo Social Twitter Referred Visits | Number of referred visits attributed to the lead through Twitter. System managed |
| middleName | MiddleName | Middle Name | Lead's Middle Name |
| mobilePhone | MobilePhone | Mobile Phone Number | Lead's mobile phone number |
| numberOfEmployees | NumberOfEmployees | Num Employees | Number of employees of lead's company |
| phone | Phone | Phone Number | Lead's Phone Number |
| postalCode | PostalCode | Postal Code | Lead's postal code |
| rating | Rating | Lead Rating | Marketing/sales rating of the lead |
| salutation | Salutation | Salutation | Lead's preferred salutation, i.e. Mister, Misses…etc. |
| sicCode | SICCode | SIC Code | Standard Industrial Classification code of the lead's company |
| site | Site | Site |  |
| state | State | State | Lead's state |
| title | Title | Job Title | Lead's job title |
| unsubscribed | Unsubscribed | Unsubscribed | Lead's email-unsubscribed status. Partially system managed. Will prevent receipt of non-operational emails if set to true. |
| unsubscribedReason | UnsubscribedReason | Unsubscribed Reason | Reason for lead's unsubscribed status. Partially system managed. Populated with Email information if lead unsubscribed directly from a Marketo email. |
| website | Website | Website | URL of the website of the lead's company |
| createdAt |  - | Created At | The time when the lead record was initially created. System managed |
| updatedAt |  - | Updated At | The last time the lead record was updated. System managed |
| emailInvalid |  - | Email Invalid | Email invalid status. All emails to the address will be blocked if set to true. Bounces indicating that the email is invalid will automatically set this field to true. |
| emailInvalidCause |  - | Email Invalid Cause | Cause of email invalid status. The instigating bounce message will be recorded in this field when email invalid is set to true. |
| inferredCity |  - | Inferred City | Lead's city inferred by reverse IP lookup of lead's first recorded web visit. |
| inferredMetropolitanArea |  - | Inferred Metropolitan Area | Lead's metropolitan area inferred by reverse IP lookup of lead's first recorded web visit. |
| inferredPhoneAreaCode |  - | Inferred Phone Area Code | Lead's phone area code inferred by reverse IP lookup of lead's first recorded web visit. |
| inferredPostalCode |  - | Inferred Postal Code | Lead's postal code inferred by reverse IP lookup of lead's first recorded web visit. |
| inferredStateRegion |  - | Inferred State Region | Lead's state region inferred by reverse IP lookup of lead's first recorded web visit. |
| isAnonymous |  - | Is Anonymous | Anonymous status of lead record. System managed. |
| priority |  - | Priority | Lead's Sales Insight priority. System managed. |
| relativeScore |  - | Relative Score | Lead's Sales Insight relative score. System managed. |
| urgency |  - | Urgency | Lead's Sales Insight urgency. System managed. |
