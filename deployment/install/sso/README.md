# Auth via SSO
Login, registration, and role-based authorization is handled via Red Hat SSO (aka Keycloak).
SSO is included as part of OpenShift or any middleware product subscription you have from Red Hat - woot!

## Installation
We can install via Operator into OpenShift. (You can also choose to do this in whatever namespace you want).

### Install the Operator
* As admin, Goto the OpenShift webconsole and Operators > OperatorHub
* Filter by keyword "Keycloak" and you should see a community operator show up - Click it.
* The details will slide in from the right, Click Install (we are using version 8.0.2 today, higher should be OK too)
* Wait until everything finishes and the operator is running

### Customize the Resources
Check out the .yaml files here and customize for your cluster and domain (also you can customize other things like redirect urls, security settings, CORS, etc). Note that we have super relaxed security settings for the demo and they are not recommended to be used like this in production.

### Create an Instance of SSO / Configuration
You can do this CLI or webconsole. If using web console just use the + button at the top then drag'n'drop the file from the steps below.

Create Keycloak Instance
* oc apply -f ./keycloak.yaml

Note: your admin username is `admin` and the password is autogenerated. These are in a secret called: `credential-shared-keycloak`

We configure via Kubernetes resources to create the realm + roles + clients & users as follows:
* oc apply -f ./keycloak-realm.yaml
* oc apply -f ./keycloak-user-1.yaml
* oc apply -f ./keycloak-user-2.yaml


## Access Info / API documentation
- Admin can login at: https://auth-microservices-demo.apps.YOURCLUSTER.COM/
- Users will login at: https://auth-microservices-demo.apps.YOURCLUSTER.COM/auth/realms/microservices/account

To understand more about keycloak check out the resources below:
* [Official Docs][1]
* [Upstream Docs][2]
* [Blog Example][3]

[1]: https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.3/html-single/red_hat_single_sign-on_for_openshift/
[2]: https://www.keycloak.org/documentation.html
[3]: https://developers.redhat.com/blog/2020/01/29/api-login-and-jwt-token-generation-using-keycloak/
