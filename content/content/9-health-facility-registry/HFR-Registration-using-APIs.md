# Health Facility Registry
Health Facility Registry is a comprehensive repository of health facilities of the country across modern and traditional systems of medicine. It includes both public and private healthcare facilities which includes hospitals, clinics, diagnostic laboratories and imaging centers, pharmacies, etc. A facility can register in ABDM HFR by following just a few simple steps for registration. Registrations steps are listed on webpage, [Health Facility Registry](https://facility.abdm.gov.in/) under menu item, 'Resource Center'.

## Terminologies used in ABDM HFR 

**ABDM** - Ayushman Bharat Digital Mission

**Authorization token** - To obtain, the HRP can call ‘sessions API’ along with the received Client ID and Client Secret. Same must be used in header for other APIs.

**Client ID** - Post internal approval, Integrator will receive Client ID to access ABDM APIs

**Client Secret** - Post internal approval, Integrator will receive Client Secret to access ABDM APIs

**Gateway** - Gateway is the hub that mediates and connects Consent Manager(s), Health Repository Providers and HIUs in the network.

**HIMS** -Healthcare information management system

**HIU** - An HIU (Health Information User) is an entitythat wants access to digital health information from HIPs, in order to provide services to the patient to whom the information belongs. An HIU can be a hospital, clinic, healthcare technology company, organizations working on health analytics, insurers, medical researchers and government entities.

**LIMS** -laboratory information management system
Request ID - UUID or in response from the API (UUID and response requestIDcan not be same in one call) 

**Sandbox** - Sandbox is a framework that will allow technologies or products to be tested in the contained environment in compliance with ABDM standards.

**UUID** - 128-bit universally unique identifier 

**X-HIP ID** - Obtained from HFR registration and Register as HIP service through the API

**X-HIU ID** - Obtained from HFR registration and Register as HIU service through the API

**X-CM ID** - For sandbox = sbx , for Production = abdm 

**HIP (Health Information Provider)** - HIP can be a hospital, laboratory, health care center, clinic or pharmacy. Essentially, it is any healthcare facility which creates medical data pertaining to a citizen/patient. In order to become an HIP, the said health facility will need to enroll in the ABDM Health Facility Registry (HFR) and link to the HRP

**HRP (Health repository providers)** - HRP are software service providers who offer ABDM compliant software and long-term digital storage of health records to HIPs like hospitals, labs, clinics, etc. Their primary role is to enable HIPs to meet their obligations of sharing and securely maintaining the health records of patients digitally. 


## Registration in Health Facility Registry

*All APIs provided in this documentation are for the ABDM Sandbox. Remove “sbx” for the production URLs*

#### Step 1: Register the facility manager for the HRP

Before starting to create/register a facility using the APIs, following two steps are required to be successfully completed.

1. 	Creation of Healthcare Professional ID (HPID) of the facility manager – Generate HPID using Aadhaar, by integrating the APIs published on the [swagger page of HPID](https://hpridsbx.abdm.gov.in/api/swagger-ui.html#/) including setting up the password.
2. 	In the absence of API integration, visit [Sandbox HPR registration page](https://hpridsbx.abdm.gov.in/register?origin=HFR) to create HPID for the facility manager. Once ID is generated, password setup must also be completed. 
3. 	To start with the third step, HPID and the password (as set in Step-2) must be in handy. To complete the third step, visit [HPID swagger link]( https://hpridsbx.abdm.gov.in/api/swagger-ui.html#/) and expand the “Authentication” tab and select “/v1/auth/authPassword” API. Fill in the request body and execute this API. Please save the “token” returned in the response as it will be used in header of create API for HFR.
4. 	API integration to generate HPID, and its authentication can be offered as a native experience to health facilities in the HRP (HMIS/LMIS/digital solutions) interface.
5. 	Successful completion of above steps are mandatory to initiate the process of facility creation in HFR using APIs.

 
#### Step 2: Register the Health Facility

**------------------------------below this not yet corrected**
The following section covers the APIs, their required parameters, and their example requests and responses for easy understanding. The easiest way to start using the HFR APIs is by trying them out in Postman (a free tool that helps developers run and debug API requests) or our Swagger UI (https://facilitysbx.abdm.gov.in/swagger-ui.html#/)

The APIs are based around REST architecture and use the basic HTTPS request methods. Our APIs accept JSON- encoded body requests and return data in the same form.

The APIs should be integrated and tested out in sandbox, prior to requesting access for production details.


Getting Started
First, you will need to whitelist the Public IP of HFR sandbox to integrate and access the APIs. Please make note of the details
•	Public IP: 121.242.73.85
•	Port to be opened: 443
•	Domain: facilitysbx.abdm.gov.in

For Production, the Public IP will need to be changed to 121.242.73.91 and domain updated to facility.abdm.gov.in

API Usage Guidelines
•	Our APIs use the basic HTTP request codes: POST and GET.
•	Each API has been described in detail with the attribute description, format followed if any and mandatory or not.
•	There are certain APIs which have Authorization as a Header which will need an access-token.
•	The APIs and related details are also present on our swagger interface (https://facilitysbx.abdm.gov.in/swagger-ui.html# ). 
•	We have also created master APIs where you can check what all master data sets are available in the HFR system and see corresponding values as well. These are present under the “Utilities” tab on swagger link.

It is requested that you first check if the facility is already registered using the Search API or the HFR UI. If the facility is already registered, you can proceed with linking the facility as in the “Link the facility with your HRP software” step. In order to register a new facility pass all the required information in order in the mentioned APIs (basic information, additional information, detailed information, submit facility). The tables following in each API section below describes the various fields / formats and validations
