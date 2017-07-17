# SSO

### Description	
* How to specify relay state on Identify Provider set up.

Resolution	
* RelayState will be sent as an HTTP Parameter along side a SAML AuthnRequest ( per the SAML standard ).

NOTE: relayState must be a valid SFDC url. External urls are going to fail with and "Invalid Page Redirection" error
 
To set it up in salesforce, please add "&RelayState=FOO" to your login URL. For example, if the IDP init URL is 
 
https://identity.my.salesforce.com/idp/login?app=0spE00000008XXX
 
You'd end up with 
 
https://identity.my.salesforce.com/idp/login?app=0spE00000008XXX&RelayState=FOO 
