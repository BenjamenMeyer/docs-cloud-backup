
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

.. _get-list-events-for-an-agent-v2-project-id-agents-agent-id-events:

List events for an agent
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v2/{project_id}/agents/{agent_id}/events

Lists events for the specified agent.

This operation lists all events for the specified agent. You should consider these events to be transient because they might disappear after a minute or so. Therefore, this operation is most useful for monitoring an agent's current activity. 

You can find additional event information in the following operation descriptions: 

* 
* GET /v2/agents/{id}/browse-request/{request_id} (See "View results of a browse request for an agent".)
* GET /v2/agents/{id}/vault-encryption-request/{request_id} (See "Lists results of a vault encryption request".)
* GET /v2/agents/{id}/vault-password-verification-request/{request_id} (See "View results for a vault password verification request".)
* GET /v2/backups/{id}/browse-request/{request_id} (See "View results of a browse request for a backup".)
* GET /v2/backups/{id}/events (See "List events for a backup".)
* GET /v2/cleanups/{id}/events (See "List events for a cleanup".)
* GET /v2/restores/{id}/events (See "List events for a restore".)






This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |OK                       |                         |
+--------------------------+-------------------------+-------------------------+
|400                       |                         |                         |
+--------------------------+-------------------------+-------------------------+
|401                       |                         |                         |
+--------------------------+-------------------------+-------------------------+
|403                       |                         |                         |
+--------------------------+-------------------------+-------------------------+
|404                       |                         |                         |
+--------------------------+-------------------------+-------------------------+
|405                       |                         |                         |
+--------------------------+-------------------------+-------------------------+
|409                       |                         |                         |
+--------------------------+-------------------------+-------------------------+
|500                       |                         |                         |
+--------------------------+-------------------------+-------------------------+
|503                       |                         |                         |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""




This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{project_id}              |String                   |Project ID of the user.  |
|                          |                         |Also referred to as the  |
|                          |                         |tenant ID or account ID. |
+--------------------------+-------------------------+-------------------------+
|{agent_id}                |String *(Required)*      |Agent ID. For example,   |
|                          |                         |``8f135b4f-7a69-4b8a-    |
|                          |                         |947f-5e80d772fd97``.     |
+--------------------------+-------------------------+-------------------------+



This table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|marker                    |String *(Optional)*      |Event ID. For example,   |
|                          |                         |``5152883998``. Only     |
|                          |                         |events newer than the    |
|                          |                         |event specified by       |
|                          |                         |marker are returned. Use |
|                          |                         |of ``marker`` is most    |
|                          |                         |useful when you are      |
|                          |                         |continuously monitoring  |
|                          |                         |this endpoint for new    |
|                          |                         |events, so that old      |
|                          |                         |events are not repeated  |
|                          |                         |back to you in           |
|                          |                         |subsequent calls.        |
+--------------------------+-------------------------+-------------------------+
|limit                     |Integer *(Optional)*     |Number of events to      |
|                          |                         |list. The default value  |
|                          |                         |is 100.                  |
+--------------------------+-------------------------+-------------------------+
|sort_dir                  |String *(Optional)*      |Direction to sort the    |
|                          |                         |results. Valid values    |
|                          |                         |are ``asc`` and          |
|                          |                         |``desc``. The default    |
|                          |                         |value is ``desc``.       |
+--------------------------+-------------------------+-------------------------+




This operation does not accept a request body.




**Example List events for an agent: JSON request**


.. code::

   GET https://dfw.backup.api.rackspacecloud.com/v2/110011/agents/8f135b4f-7a69-4b8a-947f-5e80d772fd97/events?marker=5152883998&limit=100&sort_dir=desc HTTP/1.1
   Host: dfw.backup.api.rackspacecloud.com
   X-Auth-Token: 0f6e9f63600142f0a970911583522217
   Content-type: application/json





Response
""""""""""""""""





This table shows the body parameters for the response:

+-------------------------------+---------+------------------------------------+
|Name                           |Type     |Description                         |
+===============================+=========+====================================+
|\ **events**                   |String   |Information about events for the    |
|                               |         |agent.                              |
+-------------------------------+---------+------------------------------------+
|events.\ **id**                |String   |ID of the event.                    |
+-------------------------------+---------+------------------------------------+
|events.\ **time**              |String   |Time of the event.                  |
+-------------------------------+---------+------------------------------------+
|\ **event**s.\ **event**       |String   |Type of the event.                  |
+-------------------------------+---------+------------------------------------+
|events.\ **agent**             |String   |Information about the agent for     |
|                               |         |each ``event`` except ``mode``.     |
+-------------------------------+---------+------------------------------------+
|events.agent.\ **id**          |String   |ID of agent.                        |
+-------------------------------+---------+------------------------------------+
|events.agent.\ **name**        |String   |Name of the agent.                  |
+-------------------------------+---------+------------------------------------+
|events.agent.\ **host**        |String   |Information about the host.         |
+-------------------------------+---------+------------------------------------+
|events.agent.h\ **os**t.\      |String   |Information about the operating     |
|**os**                         |         |system for the host.                |
+-------------------------------+---------+------------------------------------+
|events.agent.host.os.\ **name**|String   |Name of the operating system.       |
+-------------------------------+---------+------------------------------------+
|events.agent.host.os.\         |String   |Version of the operating system.    |
|**version**                    |         |                                    |
+-------------------------------+---------+------------------------------------+
|events.agent.host.os.\         |String   |Architecture of the operating       |
|**architecture**               |         |system.                             |
+-------------------------------+---------+------------------------------------+
|events.\ **mode**              |String   |Mode of the event when ``event`` is |
|                               |         |``agent_activate``.                 |
+-------------------------------+---------+------------------------------------+
|events.\ **request_id**        |String   |ID of the request when ``event`` is |
|                               |         |``vault_encryption_enable``,        |
|                               |         |``vault_encryption_change``,        |
|                               |         |``vault_password_verify``,          |
|                               |         |``vault_db_download_in_progress``,  |
|                               |         |``vault_db_download_completed``,    |
|                               |         |``vault_db_download_failed``,       |
|                               |         |``host_browse``,                    |
|                               |         |``logfile_upload``,                 |
|                               |         |``logfile_upload``, or              |
|                               |         |``logfile_completed`` .             |
+-------------------------------+---------+------------------------------------+
|events.\                       |String   |Encrypted old password when         |
|**old_encrypted_password_hex** |         |``event`` is                        |
|                               |         |``vault_encryption_change``.        |
+-------------------------------+---------+------------------------------------+
|events.\                       |String   |Encrypted new password when         |
|**new_encrypted_password_hex** |         |``event`` is                        |
|                               |         |``vault_encryption_change``.        |
+-------------------------------+---------+------------------------------------+
|events.\                       |String   |Encrypted password when ``event``   |
|**encrypted_password_hex**     |         |is ``vault_encryption_enable`` or   |
|                               |         |``vault_password_verify``.          |
+-------------------------------+---------+------------------------------------+
|events.\ **path**              |String   |Path to browse when ``event`` is    |
|                               |         |``host_browse``.                    |
+-------------------------------+---------+------------------------------------+
|events.\ **path_encoded**      |String   |Encoded path to browse when         |
|                               |         |``event`` is ``host_browse``.       |
+-------------------------------+---------+------------------------------------+
|events.\ **links**             |String   |Link information when ``event`` is  |
|                               |         |``logfile_upload``.                 |
+-------------------------------+---------+------------------------------------+
|events.links.\ **href**        |String   |Location (URI) of event.            |
+-------------------------------+---------+------------------------------------+
|events.links.\ **rel**         |String   |How the href link provided is       |
|                               |         |related to this resource URI.       |
+-------------------------------+---------+------------------------------------+
|\ **links**                    |String   |Link information for the next and   |
|                               |         |previous events.                    |
+-------------------------------+---------+------------------------------------+
|links.\ **href**               |String   |Location (URI).                     |
+-------------------------------+---------+------------------------------------+
|links.\ **rel**                |String   |How the href link provided is       |
|                               |         |related to this resource URI.       |
+-------------------------------+---------+------------------------------------+







**Example List events for an agent: JSON response**


.. code::

   200 (OK)
   Content-Type: application/json


.. code::

   {
       "events": [
           {
               "id": "5650135583",
               "time": "2014-10-09T12:26:15.233501Z",
               "event": "agent_registered",
               "agent": {
                   "id": "8f135b4f-7a69-4b8a-947f-5e80d772fd97",
                   "name": "Web Server",
                   "host": {
                       "os": {
                           "name": "Ubuntu",
                           "version": "14.04",
                           "architecture": "64-bit"
                       }
                   }
               }
           },
           {
               "id": "5650135584",
               "time": "2014-10-09T12:26:16.233501Z",
               "event": "agent_activate",
               "mode": "active"
           },
           {
               "id": "5650135585",
               "time": "2014-10-09T12:26:17.233501Z",
               "event": "agent_heartbeat",
               "agent": {
                   "id": "8f135b4f-7a69-4b8a-947f-5e80d772fd97"
               }
           },
           {
               "id": "5650135586",
               "time": "2014-10-09T12:26:18.233501Z",
               "event": "configuration_changed",
               "agent": {
                   "id": "8f135b4f-7a69-4b8a-947f-5e80d772fd97"
               }
           },
           {
               "id": "5650135587",
               "time": "2014-10-09T12:26:19.233501Z",
               "event": "vault_encryption_enable",
               "agent": {
                   "id": "8f135b4f-7a69-4b8a-947f-5e80d772fd97"
               },
               "request_id": "9072bb51-d5fd-4fc5-ad80-d62e573236b6",
               "encrypted_password_hex": "0bff42a526c78076a3d986fa75eecd 83211f166fd7692797cdde2317faee544e3300614fd54b8c0d81f975 3e58cb1ffbd62d3faf0d2bf52e79ce5cd9c6d84b5295e3dea629e71b 0a5e26efda50ff8e05a5475bb7cbd553d238c05655f56ece2df070ce 374ff1e0724827c2300e373241e94c4bc13441561604e3e70b5034eb 58d717864f304c9c73b6d1d46c4276d7ec2f0e2bd9a42a8ab0ba99eb adda84f4cbb5b3611bd319627436246912139c2dde62bd00528b1464 20dceae949d1926ae05fc7df9b474e1ee176f89069fb424b12f8f357 e6e2909ba05152e9f72a68de0046b3e1520838ff5e723af02a96f51a c1e6ef4254226249b872676af76a319cbe"
           },
           {
               "id": "5650135588",
               "time": "2014-10-09T12:26:20.233501Z",
               "event": "vault_encryption_change",
               "agent": {
                   "id": "8f135b4f-7a69-4b8a-947f-5e80d772fd97"
               },
               "request_id": "a072bb51-d5fd-4fc5-ad80-d62e573236b6",
               "old_encrypted_password_hex": "1bff42a526c78076a3d986fa75eecd 83211f166fd7692797cdde2317faee544e3300614fd54b8c0d81f975 3e58cb1ffbd62d3faf0d2bf52e79ce5cd9c6d84b5295e3dea629e71b 0a5e26efda50ff8e05a5475bb7cbd553d238c05655f56ece2df070ce 374ff1e0724827c2300e373241e94c4bc13441561604e3e70b5034eb 58d717864f304c9c73b6d1d46c4276d7ec2f0e2bd9a42a8ab0ba99eb adda84f4cbb5b3611bd319627436246912139c2dde62bd00528b1464 20dceae949d1926ae05fc7df9b474e1ee176f89069fb424b12f8f357 e6e2909ba05152e9f72a68de0046b3e1520838ff5e723af02a96f51a c1e6ef4254226249b872676af76a319cbe",
               "new_encrypted_password_hex": "0bff42a526c78076a3d986fa75eecd 83211f166fd7692797cdde2317faee544e3300614fd54b8c0d81f975 3e58cb1ffbd62d3faf0d2bf52e79ce5cd9c6d84b5295e3dea629e71b 0a5e26efda50ff8e05a5475bb7cbd553d238c05655f56ece2df070ce 374ff1e0724827c2300e373241e94c4bc13441561604e3e70b5034eb 58d717864f304c9c73b6d1d46c4276d7ec2f0e2bd9a42a8ab0ba99eb adda84f4cbb5b3611bd319627436246912139c2dde62bd00528b1464 20dceae949d1926ae05fc7df9b474e1ee176f89069fb424b12f8f357 e6e2909ba05152e9f72a68de0046b3e1520838ff5e723af02a96f51a c1e6ef4254226249b872676af76a319cbe"
           },
           {
               "id": "5650135589",
               "time": "2014-10-09T12:26:21.233501Z",
               "event": "vault_password_verify",
               "agent": {
                   "id": "8f135b4f-7a69-4b8a-947f-5e80d772fd97"
               },
               "request_id": "f353f472-4931-463a-9920-1dcad25f88e7",
               "encrypted_password_hex": "0bff42a526c78076a3d986fa75eecd 83211f166fd7692797cdde2317faee544e3300614fd54b8c0d81f975 3e58cb1ffbd62d3faf0d2bf52e79ce5cd9c6d84b5295e3dea629e71b 0a5e26efda50ff8e05a5475bb7cbd553d238c05655f56ece2df070ce 374ff1e0724827c2300e373241e94c4bc13441561604e3e70b5034eb 58d717864f304c9c73b6d1d46c4276d7ec2f0e2bd9a42a8ab0ba99eb adda84f4cbb5b3611bd319627436246912139c2dde62bd00528b1464 20dceae949d1926ae05fc7df9b474e1ee176f89069fb424b12f8f357 e6e2909ba05152e9f72a68de0046b3e1520838ff5e723af02a96f51a c1e6ef4254226249b872676af76a319cbe"
           },
           {
               "id": "5650135590",
               "time": "2014-10-09T12:26:22.233501Z",
               "event": "vault_db_download_in_progress",
               "agent": {
                   "id": "8f135b4f-7a69-4b8a-947f-5e80d772fd97"
               },
               "request_id": "ae7528c8-bcc3-4356-a237-f20fbdd79ee4"
           },
           {
               "id": "5650135591",
               "time": "2014-10-09T12:26:23.233501Z",
               "event": "vault_db_download_completed",
               "agent": {
                   "id": "8f135b4f-7a69-4b8a-947f-5e80d772fd97"
               },
               "request_id": "ae7528c8-bcc3-4356-a237-f20fbdd79ee4"
           },
           {
               "id": "5650135592",
               "time": "2014-10-09T12:26:24.233501Z",
               "event": "vault_db_download_failed",
               "agent": {
                   "id": "8f135b4f-7a69-4b8a-947f-5e80d772fd97"
               },
               "request_id": "ae7528c8-bcc3-4356-a237-f20fbdd79ee4"
           },
           {
               "id": "5650135593",
               "time": "2014-10-09T12:26:25.233501Z",
               "event": "host_browse",
               "agent": {
                   "id": "8f135b4f-7a69-4b8a-947f-5e80d772fd97"
               },
               "request_id": "16ce47f7-88b2-4983-8b1c-d4a82306ae87",
               "path": "/path/to/browse",
               "path_encoded": "/optional/base64encoded/path/if/non-utf-8/characters/present"
           },
           {
               "id": "5650135594",
               "time": "2014-10-09T12:26:26.233501Z",
               "event": "logfile_upload",
               "agent": {
                   "id": "8f135b4f-7a69-4b8a-947f-5e80d772fd97"
               },
               "request_id": "a533a845-4279-4838-af13-276114e90234",
               "links": [
                   {
                       "href": "https://cloudfilesapi.apiary-mock.com/v1/MossoCloudFS_f14d894e-28cd-4f31-8b08-449ec0876346/CloudBackupLogs/v2/8f135b4f-7a69-4b8a-947f-5e80d772fd97/2014-09-23T12-22-40.606703Z.gz",
                       "rel": "logfile"
                   }
               ]
           },
           {
               "id": "5650135595",
               "time": "2014-10-09T12:26:27.233501Z",
               "event": "logfile_started",
               "agent": {
                   "id": "8f135b4f-7a69-4b8a-947f-5e80d772fd97"
               },
               "request_id": "a533a845-4279-4838-af13-276114e90234"
           },
           {
               "id": "5650135596",
               "time": "2014-10-09T12:26:28.233501Z",
               "event": "logfile_completed",
               "agent": {
                   "id": "8f135b4f-7a69-4b8a-947f-5e80d772fd97"
               },
               "request_id": "a533a845-4279-4838-af13-276114e90234"
           }
       ],
       "links": [
           {
               "href": "https://cloudbackupapi.apiary-mock.com/v2/backups/0d95d699-d16b-11e4-93bd-c8e0eb190e3d/events?marker=5650135596",
               "rel": "next"
           },
           {
               "href": "https://cloudbackupapi.apiary-mock.com/v2/backups/0d95d699-d16b-11e4-93bd-c8e0eb190e3d/events?marker=5650135583&sort_dir=desc",
               "rel": "previous"
           }
       ]
   }




