# SSO

* [RelayState ID](https://help.salesforce.com/articleView?id=000176508&type=1)
* [Customize SAML Start, Error, Login, and Logout Pages](https://help.salesforce.com/articleView?id=sso_saml_start_stop_pages.htm&type=0)

### Description	
* How to specify relay state on Identify Provider set up.

Resolution	
* RelayState will be sent as an HTTP Parameter along side a SAML AuthnRequest ( per the SAML standard ).

NOTE: relayState must be a valid SFDC url. External urls are going to fail with and "Invalid Page Redirection" error
 
To set it up in salesforce, please add "&RelayState=FOO" to your login URL. For example, if the IDP init URL is 
 
https://identity.my.salesforce.com/idp/login?app=0spE00000008XXX
 
You'd end up with 
 
https://identity.my.salesforce.com/idp/login?app=0spE00000008XXX&RelayState=FOO 

Verify SAML request & response to check if there RelayState param is not NULL. You can use Fiddler logs or SAML tracer(Firefox Plugin) to check this.

Example Request sent to IDP:
RequestBinding: HTTPPost
PartnerId: https://demoorg.na2.force.com/login
so: 00Dx0000000XXXX
POST
RelayState: /00O/0

Example Response returned from IDP:
GET
so: 00Dx0000000YYYY
POST
RelayState: /00O/0
Relay State
In the above example, "/00O/ is the object key prefix to reports. After successful sign on, user is automatically redirected to Reports tab in salesforce.

Note: Salesforce does a POST request, so check your IDP url that is provided by your IDP is not doing a GET request. Else, Relaystate param will be returned as NULL.
