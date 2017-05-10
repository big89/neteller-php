# NETELLERgo Hosted Payment

## Create an order

The first step in using the NETELLERGO! hosted payment flow, is to create an order. The order may, or may not, contain a detailed list of all items / fees / taxes that you wish to collect payment for. NETELLER recommends you provide as much detail as possible in the order request, as the more detail you can provide, the more likely you customer is to complete the payment as they will have a better understanding of how the total purchase amount was calculated.

Your request should include redirect_urls for where you would like your customer to be returned depending on the outcome of the attempt to collect payment.

## Redirect customer to hosted_payment URL

NETELLER will respond with a unique order id, details of the order request, and a HATEOAS link for the hosted_payment flow that you redirect your customer to.

![Alt text](https://github.com/paysafegroup/neteller_rest_api_v1/raw/master/images/go-1-choose-payment.png "go-1-choose-payment")

![Alt text](https://github.com/paysafegroup/neteller_rest_api_v1/raw/master/images/go-2-success.png "go-2-success")

Once NETELLER has completed the request, the customer will be directed to the appropriate redirection url as supplied in your create order request.

## Verify status of payment invoice

When you enable webhooks from your merchant account portal, NETELLER will notify when the status of the order changes and allow you to take appropriate action. Additionally you can query for the order status or order invoice status to verify your payment. Refer to the order and invoice object for more information on the various status definitions.

The order lookup will also provide related HATEOAS links, including the related invoice and payment.

When specifying neteller as paymentMethod for a NETELLERgo! order, the value will be ignored as your checkout will be prefilled from supplied billingDetails instead.

## Webhooks

A webhook allows you to define an HTTP callback that will be POST to when an event occurs that you would like to be notified of. You can define the notification URL and select which events you wish to be notified of from your merchant account portal.

Webhooks will be sent whenever the state of the resource changes. Certain activity may lead to the same event being sent more than once.

![Alt text](https://github.com/paysafegroup/neteller_rest_api_v1/raw/master/images/merchant-dashboard-webhooks.png "merchant-dashboard-webhooks")

## Responding to a webhook

To acknowledge that you received the webhook without any problem, your server should return a 200 HTTP status code. Any other information you return in the request headers or request body will be ignored. Any response code outside the 200 range, including 3xx codes, will indicate to NETELLER that you did not receive the webhook.

If your system did not respond with a valid HTTP 200 status, NETELLER will continue to retry the request with an escalating time delay for up to 48 hours

## Secure webhooks (recommended)

NETELLER recommends that you use one of the following forms of authentication on your webhook URLs

HTTP Basic Authentication - Use basic authentication syntax in your webhook URL:

Format : https://{username}:{password}@{webhook_url} Example : https://exampleuser:NT1p2dsl@example.com/netellerwebhook

Secret Key - Provide a secret key that is passed back as part of the webhook event notification body.

Format : https://{webhook_url} Example : https://example.com/netellerwebhook

The secret key should not be shared with anyone.

## Test Member Accounts

The following member accounts are available in the sandbox environment for testing purposes.
These accounts should never be used in production and are only intended for use in testing with the test.api.neteller.com endpoint. The password supplied here can be used for testing the Authorization flows for a particular account.

Currency 	Account ID 	  Email Address 	                Secure ID 	Password
AED 	    451323763077 	netellertest_AED@neteller.com 	315508 	    NTt3st1!
AUD 	    451823760529 	netellertest_AUD@neteller.com 	521652 	    NTt3st1!
BGN 	    450424149137 	netellertest_BGN@neteller.com 	354380 	    NTt3st1!
BRL 	    452124231445 	netellertest_BRL@neteller.com 	907916 	    NTt3st1!
CAD 	    455781454840 	netellertest_CAD@neteller.com 	755608 	    NTt3st1!
CHF 	    452324249609 	netellertest_CHF@neteller.com 	372993 	    NTt3st1!
DKK 	    459734233011 	netellertest_DKK@neteller.com 	856751 	    NTt3st1!
EUR 	    453501020503 	netellertest_EUR@neteller.com 	908379 	    NTt3st1!
GBP 	    458591047553 	netellertest_GBP@neteller.com 	411392 	    NTt3st1!
HUF 	    450824149649 	netellertest_HUF@neteller.com 	363552 	    NTt3st1!
INR 	    450824016049 	netellertest_INR@neteller.com 	332880 	    NTt3st1!
JPY 	    452604251512 	netellertest_JPY@neteller.com 	490055 	    NTt3st1!
MAD 	    453123727913 	netellertest_MAD@neteller.com 	796289 	    NTt3st1!
MXN 	    456444237546 	netellertest_MXN@neteller.com 	878408 	    NTt3st1!
MYR 	    452724116521 	netellertest_MYR@neteller.com 	108145 	    NTt3st1!
NGN 	    450924006321 	netellertest_NGN@neteller.com 	205750 	    NTt3st1!
NOK 	    455394172769 	netellertest_NOK@neteller.com 	418852 	    NTt3st1!
PLN 	    451823629489 	netellertest_PLN@neteller.com 	654091 	    NTt3st1!
RON 	    450424018097 	netellertest_RON@neteller.com 	860647 	    NTt3st1!
RUB 	    455121038904 	netellertest_RUB@neteller.com 	888470 	    NTt3st1!
SEK 	    453313818311 	netellertest_SEK@neteller.com 	173419 	    NTt3st1!
SGD 	    451523741861 	netellertest_SGD@neteller.com 	316938 	    NTt3st1!
TND 	    453523858985 	netellertest_TND@neteller.com 	588931 	    NTt3st1!
TWD 	    451723748785 	netellertest_TWD@neteller.com 	711009 	    NTt3st1!
USD 	    454651018446 	netellertest_USD@neteller.com 	270955 	    NTt3st1!
ZAR 	    453523842837 	netellertest_ZAR@neteller.com 	708904 	    NTt3st1!

