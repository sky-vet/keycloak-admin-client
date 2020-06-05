[![Latest Version](https://img.shields.io/github/v/tag/MohammadWaleed/keycloak-admin-client.svg?style=flat-square)](https://github.com/MohammadWaleed/keycloak-admin-client/releases)

[![Total Downloads](https://img.shields.io/packagist/dt/mohammad-waleed/keycloak-admin-client.svg?style=flat-square)](https://packagist.org/packages/mohammad-waleed/keycloak-admin-client)

- [Introduction](#introduction)
- [How to use](#how-to-use)
- [Supported APIs](#supported-apis)
	- [Attack Detection](#attack-detection)
	- [Authentication Management](#authentication-management)
	- [Client Attribute Certificate](#client-attribute-certificate)
	- [Client Initial Access](#client-initial-access)
	- [Client Registration Policy](#client-registration-policy)
	- [Client Role Mappings](#client-role-mappings)
	- [Client Scopes](#client-scopes)
	- [Clients](#clients)
	- [Component](#component)
	- [Groups](#groups)
	- [Identity Providers](#identity-providers)
	- [Key](#key)
	- [Protocol Mappers](#protocol-mappers)
	- [Realms Admin](#realms-admin)
	- [Role Mapper](#role-mapper)
	- [Roles](#roles)
	- [Roles (by ID)](#roles-by-id)
	- [Scope Mappings](#scope-mappings)
	- [User Storage Provider](#user-storage-provider)
	- [Users](#users)
	- [Root](#root)


# Introduction

This is a php client to connect to keycloak admin rest apis with no headache.

Features:

1- Easy to use 

2- No need to get token or generate it it's already handled by the client

3- No need to specify any urls other than the base uri

4- No encode/decode for json just data as you expect

works with Keycloak 7.0 admin rest api

https://www.keycloak.org/docs-api/7.0/rest-api/index.html


# How to use

1- Create new client 

```php
$client = Keycloak\Admin\KeycloakClient::factory([
    'realm'=>'master',
    'username'=>'admin',
    'password'=>'1234',
    'client_id'=>'admin-cli',
    'baseUri'=>'http://127.0.0.1:8180'
    ]);
```

2- Use it

```php
$client->getUsers();

//Result
// Array of users
/*
[
     [
       "id" => "39839a9b-de08-4d2c-b91a-a6ce2595b1f3",
       "createdTimestamp" => 1571663375749,
       "username" => "admin",
       "enabled" => true,
       "totp" => false,
       "emailVerified" => false,
       "disableableCredentialTypes" => [
         "password",
       ],
       "requiredActions" => [],
       "notBefore" => 0,
       "access" => [
         "manageGroupMembership" => true,
         "view" => true,
         "mapRoles" => true,
         "impersonate" => true,
         "manage" => true,
       ],
     ],
   ]
*/

$client->createUser([
    'username'=>'test',
    'email'=>'test@test.com',
    'enabled'=>true,
    'credentials'=>[
        [
            'type'=>'password',
            'value'=>'1234'
        ]
    ]
    ]);

```

# Supported APIs

## [Attack Detection](https://www.keycloak.org/docs-api/7.0/rest-api/index.html#_attack_detection_resource)

| API | Function Name | Supported |
|-----|:--------:|:---------:|
| Clear any user login failures for all users This can release temporary disabled users | clearAllLoginFailures | ✔️ |
| Get status of a username in brute force detection |  getBruteForceUserStatus | ✔️ |
| Clear any user login failures for the user This can release temporary disabled user | clearUserLoginFailures | ✔️ |

## [Authentication Management](https://www.keycloak.org/docs-api/7.0/rest-api/index.html#_authentication_management_resource)

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Get authenticator providers Returns a list of authenticator providers. | getAuthenticatorProviders | ✔️ |
| Get client authenticator providers Returns a list of client authenticator providers. | getClientAuthenticatorProviders | ✔️ |
| Get authenticator provider’s configuration description | getAuthenticatorConfigInfo | ✔️ |
| Get authenticator configuration |  getAuthenticatorConfig | ✔️ |
| Update authenticator configuration | updateAuthenticatorConfig | ✔️ |
| Delete authenticator configuration | deleteAuthenticatorConfig | ✔️ |
| Add new authentication execution | createAuthenticationExecution | ✔️ |
| Get Single Execution | getAuthenticationExecution | ✔️ |
| Delete execution | deleteAuthenticationExecution | ✔️ |
| Update execution with new configuration | updateAuthenticationExecution | ✔️ |
| Lower execution’s priority | lowerAuthenticationExecutionPriority | ✔️ |
| Raise execution’s priority | raiseAuthenticationExecutionPriority | ✔️ |
| Create a new authentication flow | createAuthenticationFlow | ✔️ |
| Get authentication flows Returns a list of authentication flows. | getAuthenticationFlows | ✔️ |
| Copy existing authentication flow under a new name The new name is given as 'newName' attribute of the passed JSON object | copyAuthenticationFlow | ✔️ |
| Get authentication executions for a flow | getAuthenticationFlowExecutions | ✔️ |
| Update authentication executions for a flow | updateAuthenticationFlowExecutions | ✔️ |
| Add new authentication execution to a flow | createAuthenticationFlowExecution | ✔️ |
| Add new flow with new execution to existing flow | addAuthenticationFlowExecution | ✔️ |
| Get authentication flow for id | getAuthenticationFlow | ✔️ |
| Update authentication flow for id | updateAuthenticationFlow | ✔️ |
| Delete an authentication flow | deleteAuthenticationFlow | ✔️ |
| Get form action providers Returns a list of form action providers. | getFormActionProviders | ✔️ |
| Get form providers Returns a list of form providers. | getFormProviders | ✔️ |
| Get configuration descriptions for all clients | getClientsConfigDescriptions | ✔️ |
| Register a new required actions | createRequiredAction | ✔️ |
| Get required actions Returns a list of required actions. | getRequiredActions | ✔️ |
| Get required action for alias | getAliasRequiredAction | ✔️ |
| Update required action | updateRequiredAction | ✔️ |
| Delete required action | deleteRequiredAction | ✔️ |
| Lower required action’s priority | lowerRequiredActionPriority | ✔️ |
| Raise required action’s priority | raiseRequiredActionPriority | ✔️ |
| Get unregistered required actions Returns a list of unregistered required actions. | getUnregisteredRequiredActions | ✔️ |

## [Client Attribute Certificate](https://www.keycloak.org/docs-api/7.0/rest-api/index.html#_client_attribute_certificate_resource)


| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Get key info (try with attr = "jwt.credential") | getClientKeyInfo | ✔️ |
| Get a keystore file for the client, containing private key and public certificate (note: write response content to a file) | getClientKeyStore | ✔️ |
| Generate a new certificate with new key pair | generateClientCertificate | ✔️ |
| Generate a new keypair and certificate, and get the private key file Generates a keypair and certificate and serves the private key in a specified keystore format. | generateDownloadClientCertificate | ✔️ |
| Upload certificate and eventually private key | uploadClientCertificateAndPrivateKey | ✔️ |
| Upload only certificate, not private key | uploadClientCertificateOnly | ✔️ |

 ## [Client Initial Access](https://www.keycloak.org/docs-api/10.0/rest-api/index.html#_client_initial_access_resource)

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Create a new initial access token. | createClientInitialAccessToken | ✔️ |
| GET /{realm}/clients-initial-access | getClientInitialAccessTokens | ✔️ |
| DELETE /{realm}/clients-initial-access/{id} | deleteClientInitialAccessToken | ✔️ |

 ## [Client Registration Policy](https://www.keycloak.org/docs-api/10.0/rest-api/index.html#_client_registration_policy_resource)

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Base path for retrieve providers with the configProperties properly filled | getClientRegistrationPolicyProviders | ✔️ |

 ## [Client Role Mappings](https://www.keycloak.org/docs-api/10.0/rest-api/index.html#_client_role_mappings_resource)

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Add client-level roles to the group role mapping (couldn't make it seems like an issue with keycloak itslef ??) | addGroupClientRoleMappings | ❌ |
| Get client-level role mappings for the group, and the app | getGroupClientRoleMappings | ✔️ |
| Delete client-level roles from group role mapping | deleteGroupClientRoleMappings | ✔️ |
| Get available client-level roles that can be mapped to the group | getAvailableGroupClientRoleMappings | ✔️ |
| Get effective client-level role mappings This recurses any composite roles for groups | getGroupClientRoleMappingsWithComposite | ✔️ |
| Add client-level roles to the user role mapping (couldn't make it seems like an issue with keycloak itslef ??) | addUserClientRoleMappings | ❌ |
| Get client-level role mappings for the user, and the app | getUserClientRoleMappings | ✔️ |
| Delete client-level roles from user role mapping | deleteUserClientRoleMappings | ✔️ |
| Get available client-level roles that can be mapped to the user | getAvailableUserClientRoleMappings | ✔️ |
| Get effective client-level role mappings This recurses any composite roles for users | getUserClientRoleMappingsWithComposite | ✔️ |

 ## [Client Scopes](https://www.keycloak.org/docs-api/10.0/rest-api/index.html#_client_scopes_resource)

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Create a new client scope Client Scope’s name must be unique! | createClientScope | ✔️ |
| Get client scopes belonging to the realm Returns a list of client scopes belonging to the realm | getClientScopes | ✔️ |
| Get representation of the client scope | getClientScope | ✔️ |
| Update the client scope | updateClientScope | ✔️ |
| Delete the client scope | deleteClientScope | ✔️ |

 ## [Clients]()

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Create a new client Client’s client_id must be unique! | | ❌ |
| Get clients belonging to the realm Returns a list of clients belonging to the realm | getClients | ✔️ |
| Get representation of the client | | ❌ |
| Update the client | | ❌ |
| Delete the client | | ❌ |
| Generate a new secret for the client | | ❌ |
| Get the client secret | | ❌ |
| Get default client scopes. | | ❌ |
| PUT /{realm}/clients/{id}/default-client-scopes/{clientScopeId} | | ❌ |
| DELETE /{realm}/clients/{id}/default-client-scopes/{clientScopeId} | | ❌ |
| Create JSON with payload of example access token | | ❌ |
| Return list of all protocol mappers, which will be used when generating tokens issued for particular client. | | ❌ |
| Get effective scope mapping of all roles of particular role container, which this client is defacto allowed to have in the accessToken issued for him. | | ❌ |
| Get roles, which this client doesn’t have scope for and can’t have them in the accessToken issued for him. | | ❌ |
| GET /{realm}/clients/{id}/installation/providers/{providerId} | | ❌ |
| Return object stating whether client Authorization permissions have been initialized or not and a reference | | ❌ |
| Return object stating whether client Authorization permissions have been initialized or not and a reference | | ❌ |
| Register a cluster node with the client Manually register cluster node to this client - usually it’s not needed to call this directly as adapter should handle by sending registration request to Keycloak | | ❌ |
| Unregister a cluster node from the client | | ❌ |
| Get application offline session count Returns a number of offline user sessions associated with this client { "count": number } | | ❌ |
| Get offline sessions for client Returns a list of offline user sessions associated with this client | | ❌ |
| Get optional client scopes. | | ❌ |
| PUT /{realm}/clients/{id}/optional-client-scopes/{clientScopeId} | | ❌ |
| DELETE /{realm}/clients/{id}/optional-client-scopes/{clientScopeId} | | ❌ |
| Push the client’s revocation policy to its admin URL If the client has an admin URL, push revocation policy to it. | | ❌ |
| Generate a new registration access token for the client | | ❌ |
| Get a user dedicated to the service account | | ❌ |
| Get application session count Returns a number of user sessions associated with this client { "count": number } | | ❌ |
| Test if registered cluster nodes are available Tests availability by sending 'ping' request to all cluster nodes. | | ❌ |
| Get user sessions for client Returns a list of user sessions associated with this client | | ❌ |

 ## [Component]()

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| POST /{realm}/components | | ❌ |
| GET /{realm}/components | | ❌ |
| GET /{realm}/components/{id} | | ❌ |
| PUT /{realm}/components/{id} | | ❌ |
| DELETE /{realm}/components/{id} | | ❌ |
| List of subcomponent types that are available to configure for a particular parent component. | | ❌ |

 ## [Groups]()

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| create or add a top level realm groupSet or create child. | | ✔ |
| Get group hierarchy. | | ❌ |
| Returns the groups counts. | | ❌ |
| GET /{realm}/groups/{id} | | ❌ |
| Update group, ignores subgroups. | | ❌ |
| DELETE /{realm}/groups/{id} | | ❌ |
| Set or create child. | | ❌ |
| Return object stating whether client Authorization permissions have been initialized or not and a reference | | ❌ |
| Return object stating whether client Authorization permissions have been initialized or not and a reference | | ❌ |
| Get users Returns a list of users, filtered according to query parameters | | ❌ |

 ## [Identity Providers]()

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Import identity provider from uploaded JSON file | | ❌ |
| Create a new identity provider | | ❌ |
| Get identity providers | | ❌ |
| Get the identity provider | | ❌ |
| Update the identity provider | | ❌ |
| Delete the identity provider | | ❌ |
| Export public broker configuration for identity provider | | ❌ |
| Return object stating whether client Authorization permissions have been initialized or not and a reference | | ❌ |
| Return object stating whether client Authorization permissions have been initialized or not and a reference | | ❌ |
| Get mapper types for identity provider | | ❌ |
| Add a mapper to identity provider | | ❌ |
| Get mappers for identity provider | | ❌ |
| Get mapper by id for the identity provider | | ❌ |
| Update a mapper for the identity provider | | ❌ |
| Delete a mapper for the identity provider | | ❌ |
| Get identity providers | | ❌ |

 ## [Key]()

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| GET /{realm}/keys | | ❌ |

 ## [Protocol Mappers]()

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Create multiple mappers | | ❌ |
| Create a mapper | | ❌ |
| Get mappers | | ❌ |
| Get mapper by id | | ❌ |
| Update the mapper | | ❌ |
| Delete the mapper | | ❌ |
| Get mappers by name for a specific protocol | | ❌ |
| Create multiple mappers | | ❌ |
| Create a mapper | | ❌ |
| Get mappers | | ❌ |
| Get mapper by id | | ❌ |
| Update the mapper | | ❌ |
| Delete the mapper | | ❌ |
| Get mappers by name for a specific protocol | | ❌ |

 ## [Realms Admin]()

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Import a realm Imports a realm from a full representation of that realm. | | ❌ |
| Get the top-level representation of the realm It will not include nested information like User and Client representations. | | ❌ |
| Update the top-level information of the realm Any user, roles or client information in the representation will be ignored. | | ❌ |
| Delete the realm | | ❌ |
| Get admin events Returns all admin events, or filters events based on URL query parameters listed here | | ❌ |
| Delete all admin events | | ❌ |
| Clear cache of external public keys (Public keys of clients or Identity providers) | | ❌ |
| Clear realm cache | | ❌ |
| Clear user cache | | ❌ |
| Base path for importing clients under this realm. | | ❌ |
| Get client session stats Returns a JSON map. | | ❌ |
| Get realm default client scopes. | | ❌ |
| PUT /{realm}/default-default-client-scopes/{clientScopeId} | | ❌ |
| DELETE /{realm}/default-default-client-scopes/{clientScopeId} | | ❌ |
| Get group hierarchy. | | ❌ |
| PUT /{realm}/default-groups/{groupId} | | ❌ |
| DELETE /{realm}/default-groups/{groupId} | | ❌ |
| Get realm optional client scopes. | | ❌ |
| PUT /{realm}/default-optional-client-scopes/{clientScopeId} | | ❌ |
| DELETE /{realm}/default-optional-client-scopes/{clientScopeId} | | ❌ |
| Get events Returns all events, or filters them based on URL query parameters listed here | | ❌ |
| Delete all events | | ❌ |
| Get the events provider configuration Returns JSON object with events provider configuration | | ❌ |
| Update the events provider Change the events provider and/or its configuration | | ❌ |
| GET /{realm}/group-by-path/{path} | | ❌ |
| Removes all user sessions. | | ❌ |
| Partial export of existing realm into a JSON file. | | ❌ |
| Partial import from a JSON file to an existing realm. | | ❌ |
| Push the realm’s revocation policy to any client that has an admin url associated with it. | | ❌ |
| Remove a specific user session. | | ❌ |
| Test LDAP connection | | ❌ |
| Test SMTP connection with current logged in user | | ❌ |
| GET /{realm}/users-management-permissions | | ❌ |
| PUT /{realm}/users-management-permissions | | ❌ |

 ## [Role Mapper]()

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Get role mappings | | ❌ |
| Add realm-level role mappings to the user | | ❌ |
| Get realm-level role mappings | | ❌ |
| Delete realm-level role mappings | | ❌ |
| Get realm-level roles that can be mapped | | ❌ |
| Get effective realm-level role mappings This will recurse all composite roles to get the result. | | ❌ |
| Get role mappings | | ❌ |
| Add realm-level role mappings to the user | | ❌ |
| Get realm-level role mappings | | ❌ |
| Delete realm-level role mappings | | ❌ |
| Get realm-level roles that can be mapped | | ❌ |
| Get effective realm-level role mappings This will recurse all composite roles to get the result. | | ❌ |

 ## [Roles](https://www.keycloak.org/docs-api/7.0/rest-api/index.html#_roles_resource)

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Create a new role for the realm or client (Client Specific) | | ❌ |
| Get all roles for the realm or client (Client Specific) | getClientRoles | ✔️ |
| Get a role by name (Client Specific) | getClientRole | ✔️ |
| Update a role by name (Client Specific) | | ❌ |
| Delete a role by name (Client Specific) | | ❌ |
| Add a composite to the role (Client Specific) | | ❌ |
| Get composites of the role (Client Specific) | | ❌ |
| Remove roles from the role’s composite (Client Specific) | | ❌ |
| An app-level roles for the specified app for the role’s composite (Client Specific) | | ❌ |
| Get realm-level roles of the role’s composite (Client Specific) | | ❌ |
| Return List of Groups that have the specified role name (Client Specific) | | ❌ |
| Return object stating whether role Authoirzation permissions have been initialized or not and a reference (Client Specific) | | ❌ |
| Update object stating whether role Authoirzation permissions have been initialized or not and a reference (Client Specific) | | ❌ |
| Return List of Users that have the specified role name (Client Specific) | getClientRoleUsers | ✔️ |
| Create a new role for the realm or client | | ❌ |
| Get all roles for the realm or client | | ❌ |
| Get a role by name | | ❌ |
| Update a role by name | | ❌ |
| Delete a role by name | | ❌ |
| Add a composite to the role | | ❌ |
| Get composites of the role | | ❌ |
| Remove roles from the role’s composite | | ❌ |
| An app-level roles for the specified app for the role’s composite | | ❌ |
| Get realm-level roles of the role’s composite | | ❌ |
| Return List of Groups that have the specified role name | | ❌ |
| Return object stating whether role Authoirzation permissions have been initialized or not and a reference | | ❌ |
| Update object stating whether role Authoirzation permissions have been initialized or not and a reference | | ❌ |
| Return List of Users that have the specified role name | | ❌ |

 ## [Roles (by ID)]()

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Get a specific role’s representation | | ❌ |
| Update the role | | ❌ |
| Delete the role | | ❌ |
| Make the role a composite role by associating some child roles | | ❌ |
| Get role’s children Returns a set of role’s children provided the role is a composite. | | ❌ |
| Remove a set of roles from the role’s composite | | ❌ |
| Get client-level roles for the client that are in the role’s composite | | ❌ |
| Get realm-level roles that are in the role’s composite | | ❌ |
| Return object stating whether role Authoirzation permissions have been initialized or not and a reference | | ❌ |
| Return object stating whether role Authoirzation permissions have been initialized or not and a reference | | ❌ |

 ## [Scope Mappings]()

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Get all scope mappings for the client | | ❌ |
| Add client-level roles to the client’s scope | | ❌ |
| Get the roles associated with a client’s scope Returns roles for the client. | | ❌ |
| Remove client-level roles from the client’s scope. | | ❌ |
| The available client-level roles Returns the roles for the client that can be associated with the client’s scope | | ❌ |
| Get effective client roles Returns the roles for the client that are associated with the client’s scope. | | ❌ |
| Add a set of realm-level roles to the client’s scope | | ❌ |
| Get realm-level roles associated with the client’s scope | | ❌ |
| Remove a set of realm-level roles from the client’s scope | | ❌ |
| Get realm-level roles that are available to attach to this client’s scope | | ❌ |
| Get effective realm-level roles associated with the client’s scope What this does is recurse any composite roles associated with the client’s scope and adds the roles to this lists. | | ❌ |
| Get all scope mappings for the client | | ❌ |
| Add client-level roles to the client’s scope | | ❌ |
| Get the roles associated with a client’s scope Returns roles for the client. | | ❌ |
| Remove client-level roles from the client’s scope. | | ❌ |
| The available client-level roles Returns the roles for the client that can be associated with the client’s scope | | ❌ |
| Get effective client roles Returns the roles for the client that are associated with the client’s scope. | | ❌ |
| Add a set of realm-level roles to the client’s scope | | ❌ |
| Get realm-level roles associated with the client’s scope | | ❌ |
| Remove a set of realm-level roles from the client’s scope | | ❌ |
| Get realm-level roles that are available to attach to this client’s scope | | ❌ |
| Get effective realm-level roles associated with the client’s scope What this does is recurse any composite roles associated with the client’s scope and adds the roles to this lists. | | ❌ |

 ## [User Storage Provider]()

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Need this for admin console to display simple name of provider when displaying client detail KEYCLOAK-4328 | | ❌ |
| Need this for admin console to display simple name of provider when displaying user detail KEYCLOAK-4328 | | ❌ |
| Remove imported users | | ❌ |
| Trigger sync of users Action can be "triggerFullSync" or "triggerChangedUsersSync" | | ❌ |
| Unlink imported users from a storage provider | | ❌ |
| Trigger sync of mapper data related to ldap mapper (roles, groups, …​) direction is "fedToKeycloak" or "keycloakToFed" | | ❌ |

 ## [Users]()

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Create a new user Username must be unique. | createUser | ✔️ |
| Get users Returns a list of users, filtered according to query parameters | getUsers | ✔️ |
| GET /{realm}/users/count | | ❌ |
| Get representation of the user | getUser | ️️️✔️ |
| Update the user | | ❌ |
| Delete the user | | ❌ |
| Get consents granted by the user | | ❌ |
| Revoke consent and offline tokens for particular client from user | | ❌ |
| Disable all credentials for a user of a specific type | | ❌ |
| Send a update account email to the user An email contains a link the user can click to perform a set of required actions. | | ❌ |
| Get social logins associated with the user | | ❌ |
| Add a social login provider to the user | | ❌ |
| Remove a social login provider from user | | ❌ |
| GET /{realm}/users/{id}/groups | | ❌ |
| GET /{realm}/users/{id}/groups/count | | ❌ |
| PUT /{realm}/users/{id}/groups/{groupId} | | ❌ |
| DELETE /{realm}/users/{id}/groups/{groupId} | | ❌ |
| Impersonate the user | | ❌ |
| Remove all user sessions associated with the user Also send notification to all clients that have an admin URL to invalidate the sessions for the particular user. | | ❌ |
| Get offline sessions associated with the user and client | | ❌ |
| Remove TOTP from the user | | ❌ |
| Set up a new password for the user. | | ❌ |
| Send an email-verification email to the user An email contains a link the user can click to verify their email address. | | ❌ |
| Get sessions associated with the user | | ❌ |

 ## [Root]()

| API | Function Name | Supported |
|-----|:-------------:|:---------:|
| Get themes, social providers, auth providers, and event listeners available on this server | | ❌ |
| CORS preflight | | ❌ |
