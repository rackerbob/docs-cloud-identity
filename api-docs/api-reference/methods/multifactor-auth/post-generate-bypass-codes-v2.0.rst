.. _post-generate-bypass-codes-v2.0:

Generate bypass codes
~~~~~~~~~~~~~~~~~~~~~

.. code::

    POST /v2.0/users/{userId}/RAX-AUTH/multi-factor/bypass-codes

Use this operation to generate bypass codes that can be substituted for a
multi-factor authentication passcode. You can use these codes to recover access
to an account if you are unable to retrieve the multi-factor authentication
passcode  from your multi-factor authentication device. In the request, you can
specify the number  of bypass codes to generate and set an expiration date for
the generated codes.

Identity administrations (``identity:user-admin``) can  generate a single
bypass code for another user's account. Administrator-generated codes  are
valid for 30 minutes by default. Administrators can configure the validity
duration from  1 to 180 minutes.

Each bypass code can be used only one time. A bypass code remains valid until
it expires. Bypass codes are also invalidated if multi-factor authentication is
disabled on the account associated with the bypass code.

.. note::

   You can also generated bypass codes from the Account settings page in the
   Rackspace Cloud Control panel.


This table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |The request succeeded.   |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad Request              |The request is missing   |
|                          |                         |one or more elements, or |
|                          |                         |the values of some       |
|                          |                         |elements are invalid.    |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |You are not authorized   |
|                          |                         |to complete this         |
|                          |                         |operation. This error    |
|                          |                         |can occur if the request |
|                          |                         |is submitted with an     |
|                          |                         |invalid authentication   |
|                          |                         |token.                   |
+--------------------------+-------------------------+-------------------------+
|403                       |Forbidden                |The request was valid,   |
|                          |                         |but the server is        |
|                          |                         |refusing to respond      |
|                          |                         |because you do not have  |
|                          |                         |permission to access the |
|                          |                         |requested resource.      |
|                          |                         |Submit a request to your |
|                          |                         |account administrator to |
|                          |                         |determine how to gain    |
|                          |                         |access.                  |
+--------------------------+-------------------------+-------------------------+
|405                       |Invalid Method           |The method specified in  |
|                          |                         |the request is not valid |
|                          |                         |for the resource         |
|                          |                         |identified in the        |
|                          |                         |request URI.             |
+--------------------------+-------------------------+-------------------------+
|413                       |Over Limit               |The number of items      |
|                          |                         |returned is above the    |
|                          |                         |allowed limit.           |
+--------------------------+-------------------------+-------------------------+
|415                       |Bad Media Type           |Bad media type. This may |
|                          |                         |result if the wrong      |
|                          |                         |media type is used in    |
|                          |                         |the API request. Check   |
|                          |                         |the content-type and     |
|                          |                         |accept headers included  |
|                          |                         |in the request.          |
+--------------------------+-------------------------+-------------------------+
|503                       |Service Fault            |Service is not available.|
+--------------------------+-------------------------+-------------------------+


Request
-------

This table shows the header and URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |Header                   |A valid admin            |
|                          |String *(Required)*      |authentication token.    |
+--------------------------+-------------------------+-------------------------+
|{userId}                  |URI                      |The unique, system-      |
|                          |String *(Required)*      |generated user ID for an |
|                          |                         |account.                 |
+--------------------------+-------------------------+-------------------------+


This table shows the body parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|RAX-AUTH:bypassCodes      |Object                   |This object specifies    |
|                          |String *(Optional)*      |the ``validityDuration`` |
|                          |                         |and ``numberofcodes``    |
|                          |                         |attributes for the       |
|                          |                         |Generate bypass codes    |
|                          |                         |operation. See the XML   |
|                          |                         |and JSON request         |
|                          |                         |examples for the correct |
|                          |                         |syntax.                  |
+--------------------------+-------------------------+-------------------------+
|RAX-AUTH:bypassCodes.\    |Duration *(Optional)*    |Specifies the            |
|**validityDuration**      |                         |time interval that the   |
|                          |                         |bypass codes remain      |
|                          |                         |valid.                   |
|                          |                         |                         |
|                          |                         |- If no value is         |
|                          |                         |  specified, the value   |
|                          |                         |  defaults to 30 minutes |
|                          |                         |  ``PT30M``.             |
|                          |                         |                         |
|                          |                         |- If the bypass codes    |
|                          |                         |  are for your own       |
|                          |                         |  account, customize the |
|                          |                         |  value as needed.       |
|                          |                         |                         |
|                          |                         |- Administrators can     |
|                          |                         |  configure an interval  |
|                          |                         |  between 1 and 180      |
|                          |                         |  minutes when creating a|
|                          |                         |  bypass code for another|
|                          |                         |  user account.          |
|                          |                         |                         |
|                          |                         |The value                |
|                          |                         |is expressed in          |
|                          |                         |xsd:duration format,     |
|                          |                         |``PT20MPnYnMnDTnHnMnS``. |
|                          |                         |                         |
|                          |                         |``P`` indicates          |
|                          |                         |the period (required)    |
|                          |                         |                         |
|                          |                         |``nY`` indicates the     |
|                          |                         |number of years          |
|                          |                         |                         |
|                          |                         |``nM``                   |
|                          |                         |indicates the number of  |
|                          |                         |months                   |
|                          |                         |                         |
|                          |                         |``nD`` indicates the     |
|                          |                         |number of days           |
|                          |                         |                         |
|                          |                         |``T`` indicates the      |
|                          |                         |start time of a section. |
|                          |                         |(required                |
|                          |                         |if the duration value    |
|                          |                         |includes hours, minutes, |
|                          |                         |or seconds)              |
|                          |                         |                         |
|                          |                         |``nH`` indicates the     |
|                          |                         |number of hours          |
|                          |                         |                         |
|                          |                         |``nM`` indicates         |
|                          |                         |the number of minutes    |
|                          |                         |                         |
|                          |                         |``nS`` indicates the     |
|                          |                         |number of seconds        |
+--------------------------+-------------------------+-------------------------+
|RAX-AUTH:bypassCodes.\    |Integer *(Optional)*     |Specifies the number of  |
|**numberofcodes**         |                         |bypass codes to generate |
|                          |                         |codes to generate. If    |
|                          |                         |                         |
|                          |                         |If not specified, the    |
|                          |                         |value defaults to ``1``. |
|                          |                         |                         |
|                          |                         |Users can generate up to |
|                          |                         |10 bypass codes for their|
|                          |                         |own account.             |
|                          |                         |                         |
|                          |                         |Administrators can       |
|                          |                         |generate only one bypass |
|                          |                         |code for user accounts   |
|                          |                         |other than their own.    |
+--------------------------+-------------------------+-------------------------+


**Example: Generate bypass codes HTTP header request: XML**


.. code::

   POST /v2.0/users/e0fb2b4ddb594819b697d0048614c117/RAX-AUTH/multi-factor/bypass-codes HTTP/1.1
   Host: identity.api.rackspacecloud.com
   Accept: application/xml
   X-Auth-Token: 9b830c07c29f4d17a7e53d2341301234
   Content-type: application/xml


**Example:Generate bypass codes request: XML**

.. code::

   <?xml version="1.0" encoding="UTF-8"?>
   <bypassCodes validityDuration="PT20M" numberOfCodes="1"
        xmlns="http://docs.rackspace.com/identity/api/ext/RAX-AUTH/v1.0"
        xmlns:OS-KSADM="http://docs.openstack.org/identity/api/ext/OS-KSADM/v1.0"
        xmlns:atom="http://www.w3.org/2005/Atom" xmlns:identity="http://docs.openstack.org/identity/api/v2.0"/>


**Example: Generate bypass codes HTTP header request: JSON**


.. code::

   POST /v2.0/users/e0fb2b4ddb594819b697d0048614c117/RAX-AUTH/multi-factor/bypass-codes HTTP/1.1
   Host: identity.api.rackspacecloud.com
   Accept: application/json
   X-Auth-Token: 9b830c07c29f4d17a7e53d2341301234
   Content-type: application/json


**Example:Generate bypass codes request: JSON**

.. code::

   {
     "RAX-AUTH:bypassCodes": {
       "validityDuration": "PT20M",
       "numberOfCodes": "1"
     }
   }



Response
--------

This table shows the body parameters for the response:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|RAX-AUTH:bypassCodes      |Object                   |This object returns the  |
|                          |String *(Optional)*      |list of ``bypass codes`` |
|                          |                         |and the                  |
|                          |                         |``validityDuration``     |
|                          |                         |setting that specifies   |
|                          |                         |how long the codes are   |
|                          |                         |valid. See the XML and   |
|                          |                         |JSON request examples    |
|                          |                         |for the correct syntax.  |
+--------------------------+-------------------------+-------------------------+
|RAX-AUTH:bypassCodes.\    |String list *(Optional)* |Returns a list of the    |
|**codes**                 |                         |generated bypass codes.  |
+--------------------------+-------------------------+-------------------------+
|RAX-AUTH:bypassCodes.\    |Duration *(Optional)*    |The time interval that   |
|validityDuration          |                         |specifies how long the   |
|                          |                         |generated codes remain   |
|                          |                         |valid.                   |
+--------------------------+-------------------------+-------------------------+


**Example: Generate bypass codes HTTP response header: XML**


.. code::

   HTTP/1.1 200 OK
   Content-Type: application/xml


**Example:Generate bypass codes response: XML**

.. code::

   <?xml version="1.0" encoding="UTF-8"?>
   <bypassCodes validityDuration="PT10M0.000S" codes="123456789"
        xmlns="http://docs.rackspace.com/identity/api/ext/RAX-AUTH/v1.0"
        xmlns:OS-KSADM="http://docs.openstack.org/identity/api/ext/OS-KSADM/v1.0"
        xmlns:atom="http://www.w3.org/2005/Atom" xmlns:identity="http://docs.openstack.org/identity/api/v2.0"/>



**Example: Generate bypass codes HTTP response header: JSON**


.. code::

   HTTP/1.1 200 OK
   Content-Type: application/json



**Example: Generate bypass codes response: JSON**

.. code::

   {
     "RAX-AUTH:bypassCodes": {
       "codes": [
         "123456789"
       ],
       "validityDuration":"PT20M0.000S"
     }
   }
