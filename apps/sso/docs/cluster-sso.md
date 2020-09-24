## Cluster Authentication and Authorization

As the platform moves to a multi-cluster environment, it has become largely apparent that _how_ users authenticate with these clusters require 
some form of unification. The platform services team has weighed a few options that will be outlined below. Prior to that, the current
authentication/authorization mechanism is highlighted for the general audience Openshift cluster 3.11. 


## The state of things


- In Openshift 3.11 users are authenticated against a Github OAuth App. 
- The Github App is installed on [BCDevOps Github Org](https://github.com/bcdevops).
- Users __must be__ apart of the BCDevOps org in order to be authorized
- Users __must have__ Github 2fa enabled in order to authorized
- Openshift usernames map directly to a github username.

## Option 1: Use SSO IDIR for Authentication/Authorization

Ditch the usage of the Github OAuth App. Users will authenticate with the IDIRs via SSO. 

There are a few pros/cons with this approach.

### Pros
- authentication is aligned with Gov's standards of how users access gov services


### Cons
- IDIR does not allow for 2fa
- Creates (as of now) a blocker for non government teams to access a cluster. They would need to procure IDIRs in order to authentication. This process
requires manual intervention (iStore orders and HR processes). 
- Unable to use Github as an IDP. Github oidc does not provide a way to scope users to a particular Github Org. All github users would be authenticated.
Currently there is no way to provide a logic layer to authorize users (a RH ticket has been opened by Shelly inquiring on this process).

