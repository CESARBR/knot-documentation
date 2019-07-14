Authenticator SDK
=================

KNoT Cloud authenticator service JavaScript library.

----------------------------------------------------------------

Quick Start
-----------

Install
'''''''

.. code:: bash

   npm install --save @cesarbr/knot-cloud-sdk-js-authenticator

Run
'''

``KNoTCloudAuthenticator`` connects to <protocol>://<hostname>:<port>
using email and password as credentials. Replace this address with your
authenticator instance and the credentials with valid ones.

.. code:: javascript

   const KNoTCloudAuthenticator = require('@cesarbr/knot-cloud-sdk-js-authenticator');

   const client = new KNoTCloudAuthenticator({
     protocol: 'https',
     hostname: 'auth.knot.cloud',
   });

   async function main() {
     try {
       console.log(await client.authUser('user@provider.com', '123qwe!@#QWE'));
     } catch (err) {
       if (err.response) {
         console.error(err.response.data.message);
         return;
       }
       console.error(err);
     }
   }
   main();

----------------------------------------------------------------

Methods
-------

constructor(options)
''''''''''''''''''''

Create a client object that will connect to a KNoT Cloud protocol
authenticator instance.

:Parameters:

-  ``options`` **Object** JSON object with request details.

   -  ``protocol`` **String** (Optional) Either ``'http'`` or
      ``'https'``. Default: ``'https'``.
   -  ``hostname`` **String** KNoT Cloud authenticator instance host
      name.
   -  ``port`` **Number** (Optional) KNoT Cloud authenticator instance
      port. Default: 443.
   -  ``pathname`` **String** (Optional) Path name on the server.

:Return:

A client object that will connect to a KNoT Cloud

:Example:

.. code:: javascript

   const KNoTCloudAuthenticator = require('@cesarbr/knot-cloud-sdk-js-authenticator');

   const client = new KNoTCloudAuthenticator({
     protocol: 'https',
     hostname: 'auth.knot.cloud',
   });

----------------------------------------------------------------

createUser(email, password)
'''''''''''''''''''''''''''

Creates a new user.

.. _Parameters-1:

:Parameters:

-  ``email`` **String** User email.
-  ``password`` **String** User password in plain text. ### Result


:Return:

-  ``user`` **Object** JSON object containing user credentials after
   creation on cloud.

.. _example-1:

:Example:

.. code:: javascript

   const KNoTCloudAuthenticator = require('@cesarbr/knot-cloud-sdk-js-authenticator');

   const client = new KNoTCloudAuthenticator({
     protocol: 'https',
     hostname: 'auth.knot.cloud',
   });

   async function main() {
     try {
       console.log(await client.createUser('user@provider.com', '123qwe!@#QWE'));
     } catch (err) {
       if (err.response) {
         console.error(err.response.data.message);
         return;
       }
       console.error(err);
     }
   }
   main();

   // { id: '863ad780-efd9-4158-b24a-026de3f1dffb'
   //   token: '40ad864d503488eda9b629825876d46cb1356bdf' }

----------------------------------------------------------------

authUser(email, password)
'''''''''''''''''''''''''

Authenticate a user.

:Parameters:

-  ``email`` **String** User email.
-  ``password`` **String** User password in plain text. ### Result

:Return:

-  ``user`` **Object** JSON object containing user credentials after
   authentication on cloud.

:Example:

.. code:: javascript

   const KNoTCloudAuthenticator = require('@cesarbr/knot-cloud-sdk-js-authenticator');

   const client = new KNoTCloudAuthenticator({
     protocol: 'https',
     hostname: 'auth.knot.cloud',
   });

   async function main() {
     try {
       console.log(await client.authUser('user@provider.com', '123qwe!@#QWE'));
     } catch (err) {
       if (err.response) {
         console.error(err.response.data.message);
         return;
       }
       console.error(err);
     }
   }
   main();

   // { id: '863ad780-efd9-4158-b24a-026de3f1dffb'
   //   token: '40ad864d503488eda9b629825876d46cb1356bdf' }

----------------------------------------------------------------

forgotPassword(email)
'''''''''''''''''''''

Tells to cloud that a user forgot its password. The cloud then sends an
email with a token to reset the password.

.. _Parameters-1:

:Parameters:

-  ``email`` **String** User email.

.. _example-1:

:Example:

.. code:: javascript

   const KNoTCloudAuthenticator = require('@cesarbr/knot-cloud-sdk-js-authenticator');

   const client = new KNoTCloudAuthenticator({
     protocol: 'https',
     hostname: 'auth.knot.cloud',
   });

   async function main() {
     try {
       await client.forgotPassword('user@provider.com');
     } catch (err) {
       if (err.response) {
         console.error(err.response.data.message);
         return;
       }
       console.error(err);
     }
   }
   main();

----------------------------------------------------------------

resetPassword(email, token, newPassword)
''''''''''''''''''''''''''''''''''''''''

Resets a password from a user.

.. _Parameters-2:

:Parameters:

-  ``email`` **String** User email.
-  ``token`` **String** Token sent by email.
-  ``newPassword`` **String** User password in plain text.

.. _example-2:

:Example:

.. code:: javascript

   const KNoTCloudAuthenticator = require('@cesarbr/knot-cloud-sdk-js-authenticator');

   const client = new KNoTCloudAuthenticator({
     protocol: 'https',
     hostname: 'auth.knot.cloud',
   });

   async function main() {
     try {
       const token = '54ad864d5034887419b629825876d46cb1356b06';
       const newPassword = 'QWEqwe!@#123';
       await client.resetPassword('user@provider.com', token, newPassword);
     } catch (err) {
       if (err.response) {
         console.error(err.response.data.message);
         return;
       }
       console.error(err);
     }
   }
   main();
