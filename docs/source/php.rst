.. _PHP-label:

PHP Integrations
========================

Liquid ResellerCamp PHP HTTP Integrations APIs


API library
-----------

Libraries for the Liquid API can be downloaded in `here <https://github.com/liquidregistrar/liquid-php/archive/master.zip>`_.


API Endpoint
------------

::

    https://api.liqu.id/v1


Example Request Authentication
------------------------------

.. sourcecode:: json

    $apiClient = new \Liquid\Client\ApiClient();

You can set the default API key, or you can always pass a key directly to an object's constructor. Authentication is transparently handled for you in subsequent method calls.

A sample test API key is included in all the examples on this page, so you can test any example right away. To test requests using your account, replace the sample API key with your actual API key.


HTTP status code summary
------------------------

+------------------------+----------------------------------------------------------------------------+
|  200 - OK              | Everything worked as expected.                                             |
+------------------------+----------------------------------------------------------------------------+
|  400 - Invalid Request | The request was unacceptable, often due to missing a required parameter.   |
+------------------------+----------------------------------------------------------------------------+
|  401 - Unauthorized    | No or invalid authentication details are provided.                         |
+------------------------+----------------------------------------------------------------------------+
|  402 - Failed Request  | The parameters were valid but the request failed.                          |
+------------------------+----------------------------------------------------------------------------+
|  404 - Not Found       | The requested resource doesn't exist.                                      |
+------------------------+----------------------------------------------------------------------------+


Handling errors
---------------

Our API libraries raise exceptions for many reasons, such as a failed charge, invalid parameters, authentication errors, and network unavailability. We recommend writing code that gracefully handles all possible API exceptions.

.. sourcecode:: json

    try {
        // Use Liquid's library to make requests...
    } catch (Liquid\Client\ApiException $e) {
        echo 'Caught exception: ', $e->getMessage(), "\n";
        echo '<br>HTTP response headers: ', $e->getResponseHeaders(), "\n";
        echo '<br>HTTP response body: ', $e->getResponseBody(), "\n";
        echo '<br>HTTP status code: ', $e->getCode(), "\n";
    }


Expanding Objects
-----------------

Many objects contain the ID of a related object in their response properties. For example, a Charge may have an associated Customer ID. Those objects can be expanded inline with the expand request parameter. Objects that can be expanded are noted in this documentation. This parameter is available on all API requests, and applies to the response of that request only. 

Example Request

.. sourcecode:: php

    $apiClient = new \Liquid\Client\ApiClient();

    // set Host to https://api.domainsas.com/v1 if you want to use Liquid Demo
    $apiClient->getConfig()->setHost('https://api.liqu.id/v1');
    // set Reseller ID here
    $apiClient->getConfig()->setUsername('1');
    // set Apikey here
    $apiClient->getConfig()->setPassword('123');


Retrieving data using callApi()
-------------------------------

Example Request to retrieve all domains with params:

.. sourcecode:: php

    $resourcePath = '/domains';
    $method       = 'GET';
    $formParams   = array();
    $headerParams = array();

    $queryParams['limit'] = 100;
    $queryParams['tld']   = 'com';

    try {
        list($response, $header) = $apiClient->callApi(
            $resourcePath,
            $method,
            $queryParams,
            $formParams,
            $headerParams
        );
    } catch (Liquid\Client\ApiException $e) {
        echo 'Caught exception: ', $e->getMessage(), "\n";
        echo '<br>HTTP response headers: ', $e->getResponseHeaders(), "\n";
        echo '<br>HTTP response body: ', $e->getResponseBody(), "\n";
        echo '<br>HTTP status code: ', $e->getCode(), "\n";
        die;
    }

    // convert obj to array
    $response = json_decode(json_encode($response), true);

    print_r($response);

Example response:

.. sourcecode:: json

    [
        {
            "domain_id":"1",
            "domain_name":"domaindemotestxyz.com",
            "approval_status_id":"1",
            "start_date":"2015-07-27 00:00:00",
            "end_date":"2016-07-27 00:00:00",
            "reseller_id":"1",
            "customer_id":"1",
            "tld_id":"1",
            "order_status_id":"1",
            "lb_order_id":null,
            "is_migrate_cust":"0",
            "is_privacy":"0",
            "reg_contact_id":"1",
            "adm_contact_id":"1",
            "bill_contact_id":"1",
            "tech_contact_id":"1",
            "is_lock":"0",
            "is_suspend":"0",
            "is_theft_protection":"1",
            "raaVerificationStatus":null,
            "raaVerificationStartTime":null,
            "auth_code":null,
            "attr":"[]",
            "last_update":null,
            "ns1":"dnsdemo1.parkir.net",
            "ns2":"dnsdemo2.parkir.net",
            "ns3":"",
            "ns4":null,
            "ns5":null,
            "ns6":null,
            "ns7":null,
            "ns8":null,
            "ns9":null,
            "ns10":null,
            "ns11":null,
            "ns12":null,
            "ns13":null,
            "customer_name":"Customer Demo PHP",
            "expiry_date":"2016-07-27 00:00:00"
        },
        {
            "domain_id":"1",
            "domain_name":"domainreseller1.com",
            "approval_status_id":"1",
            "start_date":"2015-07-27 00:00:00",
            "end_date":"2016-07-27 00:00:00",
            "reseller_id":"1",
            "customer_id":"1",
            "tld_id":"9",
            "order_status_id":"1",
            "lb_order_id":null,
            "is_migrate_cust":"0",
            "is_privacy":"0",
            "reg_contact_id":"1",
            "adm_contact_id":"1",
            "bill_contact_id":"1",
            "tech_contact_id":"1",
            "is_lock":"0",
            "is_suspend":"0",
            "is_theft_protection":"1",
            "raaVerificationStatus":null,
            "raaVerificationStartTime":null,
            "auth_code":null,
            "attr":"[]",
            "last_update":null,
            "ns1":"dnsdemo1.parkir.net",
            "ns2":"dnsdemo2.parkir.net",
            "ns3":"",
            "ns4":null,
            "ns5":null,
            "ns6":null,
            "ns7":null,
            "ns8":null,
            "ns9":null,
            "ns10":null,
            "ns11":null,
            "ns12":null,
            "ns13":null,
            "customer_name":"Customer Demo PHP",
            "expiry_date":"2016-07-27 00:00:00"
        }
    ]


Creating data using callApi()
-----------------------------

Example Request to create a new customer:

.. sourcecode:: php

    $resourcePath   = '/customers';
    $method         = 'POST';
    $queryParams    = array();
    $headerParams   = array();

    $formParams['email']          = 'demo.php@customdemo.net';
    $formParams['name']           = 'Customer Demo PHP';
    $formParams['password']       = '21&^90asfA';
    $formParams['company']        = 'Customer Demo PHP';
    $formParams['address_line_1'] = 'Pajangan';
    $formParams['city']           = 'Bantul';
    $formParams['state']          = 'Yogyakarta';
    $formParams['country_code']   = 'ID';
    $formParams['zipcode']        = '55321';
    $formParams['tel_cc_no']      = 62;
    $formParams['tel_no']         = 857321654;

    try {
        list($response, $header) = $apiClient->callApi(
            $resourcePath,
            $method,
            $queryParams,
            $formParams,
            $headerParams
        );
    } catch (Liquid\Client\ApiException $e) {
        echo 'Caught exception: ', $e->getMessage(), "\n";
        echo '<br>HTTP response headers: ', $e->getResponseHeaders(), "\n";
        echo '<br>HTTP response body: ', $e->getResponseBody(), "\n";
        echo '<br>HTTP status code: ', $e->getCode(), "\n";
        die;
    }

    // convert obj to array
    $response = json_decode(json_encode($response), true);

    print_r($response);

Example response:

.. sourcecode:: json

    {
        "customer_id":"1",
        "reseller_id":"1",
        "status":"Active",
        "email":"demo.php@customdemo.net",
        "name":"Customer Demo PHP",
        "company":"Customer Demo PHP",
        "creation_date":"2015-11-09 07:40:29",
        "total_receipts":"0.00",
        "address_line_1":"Pajangan",
        "address_line_2":"",
        "address_line_3":"",
        "city":"Bantul",
        "state":"Yogyakarta",
        "country_code":"ID",
        "country_name":"Indonesia",
        "zipcode":"55321",
        "tel_cc_no":"62",
        "tel_no":"857321654",
        "alt_tel_cc_no":null,
        "alt_tel_no":null,
        "mobile_cc_no":null,
        "mobile_no":null,
        "fax_cc_no":null,
        "fax_no":null,
        "lang_id":"English"
    }


Updating data using callApi()
-----------------------------

Example Request to update a customer:

.. sourcecode:: php

    $customer_id    = 1;
    $resourcePath   = '/customers/' . $customer_id;
    $method         = 'PUT';
    $queryParams    = array();
    $headerParams   = array();

    $formParams['email']          = 'demo.php@customdemo.net';
    $formParams['name']           = 'Customer Demo PHP';
    $formParams['company']        = 'Customer Demo PHP';
    $formParams['address_line_1'] = 'Pajangan';
    $formParams['city']           = 'Bantul';
    $formParams['state']          = 'Yogyakarta';
    $formParams['country_code']   = 'ID';
    $formParams['zipcode']        = '55321';
    $formParams['tel_cc_no']      = 62;
    $formParams['tel_no']         = 857321654;

    try {
        list($response, $header) = $apiClient->callApi(
            $resourcePath,
            $method,
            $queryParams,
            $formParams,
            $headerParams
        );
    } catch (Liquid\Client\ApiException $e) {
        echo 'Caught exception: ', $e->getMessage(), "\n";
        echo '<br>HTTP response headers: ', $e->getResponseHeaders(), "\n";
        echo '<br>HTTP response body: ', $e->getResponseBody(), "\n";
        echo '<br>HTTP status code: ', $e->getCode(), "\n";
        die;
    }

    // convert obj to array
    $response = json_decode(json_encode($response), true);

    print_r($response);

Example response:

.. sourcecode:: json

    {
        "customer_id":"1",
        "reseller_id":"1",
        "status":"Active",
        "email":"demo.php@customdemo.net",
        "name":"Customer Demo PHP",
        "company":"Customer Demo PHP",
        "creation_date":"2015-07-27 02:18:42",
        "total_receipts":"80.00",
        "address_line_1":"Pajangan",
        "address_line_2":"",
        "address_line_3":"",
        "city":"Bantul",
        "state":"Yogyakarta",
        "country_code":"ID",
        "country_name":"Indonesia",
        "zipcode":"55321",
        "tel_cc_no":"62",
        "tel_no":"857321654",
        "alt_tel_cc_no":null,
        "alt_tel_no":null,
        "mobile_cc_no":null,
        "mobile_no":null,
        "fax_cc_no":null,
        "fax_no":null,
        "lang_id":"English"
    }


Deleting data using callApi()
-----------------------------

Example Request to delete a customer:

.. sourcecode:: php

    $customer_id  = 1;
    $resourcePath = '/customers/' . $customer_id;
    $method       = 'DELETE';
    $queryParams  = array();
    $headerParams = array();
    $formParams   = array();

    try {
        list($response, $header) = $apiClient->callApi(
            $resourcePath,
            $method,
            $queryParams,
            $formParams,
            $headerParams
        );
    } catch (Liquid\Client\ApiException $e) {
        echo 'Caught exception: ', $e->getMessage(), "\n";
        echo '<br>HTTP response headers: ', $e->getResponseHeaders(), "\n";
        echo '<br>HTTP response body: ', $e->getResponseBody(), "\n";
        echo '<br>HTTP status code: ', $e->getCode(), "\n";
        die;
    }

    // convert obj to array
    $response = json_decode(json_encode($response), true);

    print_r($response);

Example response:

.. sourcecode:: json

    {
        "customer_id":"1",
        "deleted":true
    }


Retrieving data using available class api
-----------------------------------------

Using DomainsApi() to retrieve all domains:

.. sourcecode:: php

    $apiDomains = new \Liquid\Client\Api\DomainsApi($apiClient);

    $limit                      = 2;
    $page_no                    = null;
    $domain_id                  = null;
    $reseller_id                = null;
    $customer_id                = null;
    $show_child_orders          = null;
    $tld                        = null;
    $status                     = null;
    $domain_name                = null;
    $privacy_protection_enabled = null;
    $creation_time_start        = null;
    $creation_time_end          = null;
    $expiry_date_start          = null;
    $expiry_date_end            = null;
    $reseller_email             = null;
    $customer_email             = null;
    $exact_domain_name          = null;

    try {
        list($response, $header) = $apiDomains->retrieve(
            $limit, 
            $page_no, 
            $domain_id, 
            $reseller_id, 
            $customer_id, 
            $show_child_orders, 
            $tld, 
            $status, 
            $domain_name, 
            $privacy_protection_enabled, 
            $creation_time_start, 
            $creation_time_end, 
            $expiry_date_start, 
            $expiry_date_end, 
            $reseller_email, 
            $customer_email, 
            $exact_domain_name
        );
    } catch (Liquid\Client\ApiException $e) {
        echo 'Caught exception: ', $e->getMessage(), "\n";
        echo '<br>HTTP response headers: ', $e->getResponseHeaders(), "\n";
        echo '<br>HTTP response body: ', $e->getResponseBody(), "\n";
        echo '<br>HTTP status code: ', $e->getCode(), "\n";
        die;
    }

    // convert obj to array
    $response = json_decode(json_encode($response), true);

    print_r($response);

Example response:

.. sourcecode:: json

    [
        {
            "domain_id":"1",
            "domain_name":"testdomaindemo1231.com",
            "approval_status_id":"1",
            "start_date":"2015-07-27 00:00:00",
            "end_date":"2016-07-27 00:00:00",
            "reseller_id":"1",
            "customer_id":"1",
            "tld_id":"9",
            "order_status_id":"1",
            "lb_order_id":null,
            "is_migrate_cust":"0",
            "is_privacy":"0",
            "reg_contact_id":"1",
            "adm_contact_id":"1",
            "bill_contact_id":"1",
            "tech_contact_id":"1",
            "is_lock":"0",
            "is_suspend":"0",
            "is_theft_protection":"1",
            "raaVerificationStatus":null,
            "raaVerificationStartTime":null,
            "auth_code":null,
            "attr":"[]",
            "last_update":null,
            "ns1":"dnsdemo1.parkir.net",
            "ns2":"dnsdemo2.parkir.net",
            "ns3":"",
            "ns4":null,
            "ns5":null,
            "ns6":null,
            "ns7":null,
            "ns8":null,
            "ns9":null,
            "ns10":null,
            "ns11":null,
            "ns12":null,
            "ns13":null,
            "customer_name":"Customer Demo PHP",
            "expiry_date":"2016-07-27 00:00:00"
        },
        {
            "domain_id":"1",
            "domain_name":"testdomainphp3123.com",
            "approval_status_id":"1",
            "start_date":"2015-07-27 00:00:00",
            "end_date":"2016-07-27 00:00:00",
            "reseller_id":"1",
            "customer_id":"1",
            "tld_id":"1",
            "order_status_id":"1",
            "lb_order_id":null,
            "is_migrate_cust":"0",
            "is_privacy":"0",
            "reg_contact_id":"1",
            "adm_contact_id":"1",
            "bill_contact_id":"1",
            "tech_contact_id":"1",
            "is_lock":"0",
            "is_suspend":"0",
            "is_theft_protection":"1",
            "raaVerificationStatus":null,
            "raaVerificationStartTime":null,
            "auth_code":null,
            "attr":"[]",
            "last_update":null,
            "ns1":"dnsdemo1.parkir.net",
            "ns2":"dnsdemo2.parkir.net",
            "ns3":"",
            "ns4":null,
            "ns5":null,
            "ns6":null,
            "ns7":null,
            "ns8":null,
            "ns9":null,
            "ns10":null,
            "ns11":null,
            "ns12":null,
            "ns13":null,
            "customer_name":"Customer Demo PHP",
            "expiry_date":"2016-07-27 00:00:00"
        }
    ]


Creating data using available class api
---------------------------------------

Using BillingApi() to add fund a reseller:

.. sourcecode:: php

    $apiBilling = new \Liquid\Client\Api\BillingApi($apiClient);

    $reseller_id = 1;
    $amount      = 150;
    $description = 'add fund from API';

    try {
        list($response, $header) = $apiBilling->addFundReseller(
            $reseller_id,
            $amount,
            $description
        );
    } catch (Liquid\Client\ApiException $e) {
        echo 'Caught exception: ', $e->getMessage(), "\n";
        echo '<br>HTTP response headers: ', $e->getResponseHeaders(), "\n";
        echo '<br>HTTP response body: ', $e->getResponseBody(), "\n";
        echo '<br>HTTP status code: ', $e->getCode(), "\n";
        die;
    }

    // convert obj to array
    $response = json_decode(json_encode($response), true);

    print_r($response);

Example response:

.. sourcecode:: json

    {
        "transaction_id":"1",
        "reseller_id":"1",
        "transaction_type":"deposit",
        "amount":150,
        "balance":350,
        "date":"2015-11-09 08:15:32",
        "description":"add fund from API",
        "status":"pending"
    }


Updating data using available class api
---------------------------------------

Using ResellersApi() to update a reseller:

.. sourcecode:: php

    $apiReseller = new \Liquid\Client\Api\ResellersApi($apiClient);

    $reseller_id      = 1;
    $email            = 'demo.php@customdemo.net';
    $name             = 'Customer Demo PHP';
    $company          = 'Customer Demo PHP';
    $address_line_1   = 'Pajangan';
    $city             = 'Bantul';
    $state            = 'Yogyakarta';
    $country_code     = 'ID';
    $zipcode          = '55321';
    $tel_cc_no        = 62;
    $tel_no           = 8579321465;
    $selling_currency = 'USD';
    $address_line_2   = null;
    $address_line_3   = null;
    $alt_tel_cc_no    = null;
    $alt_tel_no       = null;
    $mobile_cc_no     = null;
    $mobile_no        = null;
    $fax_cc_no        = null;
    $fax_no           = null;

    try {
        list($response, $header) = $apiReseller->updateReseller(
            $reseller_id,
            $email,
            $name,
            $company,
            $address_line_1,
            $city,
            $state,
            $country_code,
            $zipcode,
            $tel_cc_no,
            $tel_no,
            $selling_currency,
            $address_line_2,
            $address_line_3,
            $alt_tel_cc_no,
            $alt_tel_no,
            $mobile_cc_no,
            $mobile_no,
            $fax_cc_no,
            $fax_no
        );
    } catch (Liquid\Client\ApiException $e) {
        echo 'Caught exception: ', $e->getMessage(), "\n";
        echo '<br>HTTP response headers: ', $e->getResponseHeaders(), "\n";
        echo '<br>HTTP response body: ', $e->getResponseBody(), "\n";
        echo '<br>HTTP status code: ', $e->getCode(), "\n";
        die;
    }

    // convert obj to array
    $response = json_decode(json_encode($response), true);

    print_r($response);

Example response:

.. sourcecode:: json

    {
        "reseller_id":"1",
        "parent_reseller_id":"1",
        "status":"Active",
        "email":"demo.php@customdemo.net",
        "name":"Customer Demo PHP",
        "brand_name":"Tambah Senin",
        "company":"Customer Demo PHP",
        "creation_date":"2014-10-27 03:06:38",
        "total_receipts":"159.00",
        "address_line_1":"Pajangan",
        "address_line_2":"",
        "address_line_3":"",
        "city":"Bantul",
        "state":"Yogyakarta",
        "country_code":"ID",
        "country_name":"Indonesia",
        "zipcode":"55321",
        "tel_cc_no":"62",
        "tel_no":"8579321465",
        "alt_tel_cc_no":null,
        "alt_tel_no":null,
        "mobile_cc_no":null,
        "mobile_no":null,
        "fax_cc_no":null,
        "fax_no":null,
        "selling_currency":"USD",
        "accounting_currency":"USD",
        "parentselling_currency":"USD",
        "lang_id":"English"
    }


Deleting data using available class api
---------------------------------------

Using ResellersApi() to delete a reseller:

.. sourcecode:: php

    $apiReseller = new \Liquid\Client\Api\ResellersApi($apiClient);

    $reseller_id = 1;

    try {
        list($response, $header) = $apiReseller->delete_(
            $reseller_id
        );
    } catch (Liquid\Client\ApiException $e) {
        echo 'Caught exception: ', $e->getMessage(), "\n";
        echo '<br>HTTP response headers: ', $e->getResponseHeaders(), "\n";
        echo '<br>HTTP response body: ', $e->getResponseBody(), "\n";
        echo '<br>HTTP status code: ', $e->getCode(), "\n";
        die;
    }

    // convert obj to array
    $response = json_decode(json_encode($response), true);

    print_r($response);

Example response:

.. sourcecode:: json

    {
        "reseller_id":"1",
        "deleted":true
    }



Available class api list
------------------------

+------------------------+------------------------+------------------------+
|  AccountApi()          |  CustomerApi()         |  EmailforwardingApi()  |
+------------------------+------------------------+------------------------+
|  BillingApi()          |  DnsApi()              |  PrivacyprotectionApi()|
+------------------------+------------------------+------------------------+
|  CommonApi()           |  DomainforwardingApi() |  ResellersApi()        |
+------------------------+------------------------+------------------------+
|  ContactsApi()         |  DomainsApi()          |                        |
+------------------------+------------------------+------------------------+


Feedback
---------

If you find any issues with Liquid Resellercamp's PHP integration APIs, please use our `ticketing support systems <https://liqudotid.freshdesk.com/support/tickets/new>`_ where we’ll be available and actively listening to all of your feedback.
