.. _restapi-label:

REST APIs
========================

Introductions
-------------

The Liquid API is organized around `REST <http://en.wikipedia.org/wiki/Representational_State_Transfer>`_. Our API is designed to have predictable, resource-oriented URLs and to use HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP authentication and HTTP verbs, which can be understood by off-the-shelf HTTP clients, and we support cross-origin resource sharing to allow you to interact securely with our API from a client-side web application (though you should remember that you should never expose your secret API key in any public website's client-side code). `JSON <http://www.json.org/>`_  will be returned in all responses from the API, including errors.

To make the Liquid API as explorable as possible, we provide demo reseller account. Please create reseller demo account here to test your code or applications. Data created within demo reseller account will never cost any money and will not create real domain. Read the :ref:`demoaccount-label` documentation.

Authentication
--------------

You authenticate to the Liquid API by providing one of your API keys in the request and your reseller ID. You can manage your API keys from your reseller control panel. You can have multiple API keys active at one time. Your API keys carry many privileges, so be sure to keep them secret! Make sure only use reseller demo account when developing your codes or applications.

Authentication to the API occurs via HTTP Basic Auth. Provide your reseller ID as the basic auth username and API key as password.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. You must authenticate for all requests.


Errors
------

Liquid uses conventional HTTP response codes to indicate success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate an error that resulted from the provided information (e.g. a required parameter was missing, etc.), and codes in the 5xx range indicate an error with Liquid's servers.

Attributes
^^^^^^^^^^

:type: The type of error returned. Can be unauthorized, invalid_request, or card_error.
:message: A human-readable message giving more details about the error. 
:code: Programming readable error code, more details than type. For example: invalid_argument


Pagination
----------

All top-level Liquid API resources have support for bulk fetches — "list" API methods. For instance you can list domains, list contacts,  list customers, list sub-resellers and list transactions. These list API methods share a common structure.

Liquid utilizes standard pagination, using the parameter limit and page_no, see below:

Arguments
^^^^^^^^^

:limit: A limit on the number of objects to be returned. Limit can range between 1 and 100 items.
:page_no: Page number, should be positive number. 

For example, to retrieve items number 11 to 20, you would request with argument limit=10 and page_no=2

Response Format
^^^^^^^^^^^^^^^

body response
*************

The body of the response will contain array of the data requested.

**Full body response example:**

.. code-block:: json

    [
      {
        "customer_id": "111111150843",
        "reseller_id": "111112",
        "status": "Active",
        "email": "example1@example1.com"
      },
      {
        "customer_id": "11111150842",
        "reseller_id": "11111112",
        "status": "Active",
        "email": "example2@example2.com"
      }
    ]

header response
***************

- link
    link will contain list of paging urls (prev url, next url, first url, and last url). 
    Example: 

::

       "Link": "<https://api.liqu.id/v1/customers?limit=10&page_no=3>; rel=\"next\", 
       <https://api.liqu.id/v1/customers?limit=10&page_no=5077>; rel=\"last\", 
       <https://api.liqu.id/v1/customers?limit=10&page_no=1>; rel=\"first\", 
       <https://api.liqu.id/v1/customers?limit=10&page_no=1>; rel=\"prev\""

- X-Total-Count
    total data available from the request.
    Example:

::

        "X-Total-Count": "50763"

**Full header response example:**

.. code-block:: json

    {
     "Date": "Fri, 29 May 2015 16:32:12 GMT",
     "Content-Encoding": "gzip",
     "Server": "nginx",
     "Link": "<https://api.liqu.id/v1/customers?limit=10&page_no=3>; rel=\"next\", <https://api.liqu.id/v1/customers?limit=10&page_no=5077>; rel=\"last\", <https://api.liqu.id/v1/customers?limit=10&page_no=1>; rel=\"first\", <https://api.liqu.id/v1/customers?limit=10&page_no=1>; rel=\"prev\"",
     "X-Frame-Options": "SAMEORIGIN",
     "Vary": "Accept-Encoding",
     "Content-Type": "application/json",
     "Transfer-Encoding": "chunked",
     "Connection": "keep-alive",
     "Keep-Alive": "timeout=5",
     "X-Xss-Protection": "1; mode=block",
     "X-Total-Count": "50763"
    }


Rate Limiting
-------------

The API is provided to you to conduct normal business activities through your own interface(s). Any activity using Liquid API, that causes lossage or creates service degradation for other users, is constituted as abuse by Liquid. A few examples of API Abuse activities are stated below:

- Sending a huge number of Check Availability commands for already registered domain names, repeatedly.
- Adding a large number of Sub-Resellers and/or Customers who do not have any Orders.

Rate limiting in Liquid API is primarily considered on a per-reseller basis. Generally, you may make up to 100 API calls per 15 minutes. When you make more API calls than allowed, your reseller API Key will be temporary suspended, this suspension will not impact your reseller account.

Tips to avoid being Rate Limited
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The tips below are there to help you code defensively and reduce the possibility of being rate limited. 

- Check Domain
    Don’t use Liquid API to check domain availability on your website interface.

- Caching
    Store API responses in your application or on your site if you expect a lot of use. For example, don’t try to call the Liquid API on every page load of your website landing page. Instead, call the API infrequently and load the response into a local cache. When users hit your website load the cached version of the results.

REST API Requests
-----------------

We provide API Console Tool for you to try out the API request and understand the responses.

- `Demo Account API Requests <https://api.liqu.id/docs>`_
- `Live Account Api Requests <https://api.domainsas.com/docs>`_

Feedback
-----------------------

If you find any issues with Liquid API, please use our `ticketing support systems <https://liqudotid.freshdesk.com/support/tickets/new>`_ dedicated to Liquid API where we’ll be available and actively listening to all of your feedback. We look forward to working with you and can’t wait to see what everyone builds.
