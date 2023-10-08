NOTE: This document contains base notes and has NOT been cleaned up at all yet.

---

# Theory of RBAC
- k8s does not do user management, instead it offloads it to identity providers.

- role = yaml file  where you give hte permissions etc. --> kind of like iam policies

- role binding --> how you attach roles to Users and Service Accounts

RBAC on k8s is made up of: 
- SA --> user/user management
- Role --> defines the permissions (cluster role if cluster based) (role if namespace based)
- Rolebinding --> connects the SAs with the Roles

---
use a 30 day free k8 openshift sandbox --> https://developers.redhat.com/developer-sandbox

use dev sandbox.

Use your own terminal
1. if you need to run `brew install openshift-cli`
2. run `brew install openshift-cli`
3. on the developer sandbox cluster click your user name in the top right > copy login command > copy the "oc" command > paste it and run it in your terminal ... should look like `oc login --token=<token> --server=<url><port>`
4. do your rbac learning here 
---
# Useful Links
[k8.io/service-accounts](https://kubernetes.io/docs/concepts/security/service-accounts/)
[rbac](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)
[k8.io/RBAC-Good-Practices](https://kubernetes.io/docs/concepts/security/rbac-good-practices/)