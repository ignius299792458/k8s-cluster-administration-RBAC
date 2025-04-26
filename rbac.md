# workout on rbac.yml

Exammple
```
➜  RBAC git:(main) ✗ kubectl auth whoami
ATTRIBUTE                                           VALUE
Username                                            kubernetes-admin
Groups                                              [kubeadm:cluster-admins system:authenticated]
Extra: authentication.kubernetes.io/credential-id   [X509SHA256=6e388e1955f6e2aa169fbf82b5028e510d0a77d9328508ab546569eab97044eb]
➜  RBAC git:(main) ✗ kubectl auth can-i
error: you must specify two arguments: verb resource or verb resource/resourceName.
See 'kubectl auth can-i -h' for help and examples.
➜  RBAC git:(main) ✗ kubectl auth can-i get pods
yes
➜  RBAC git:(main) ✗ kubectl auth can-i get pods -n rbac-ns
yes
➜  RBAC git:(main) ✗ vim rbac.yml 
➜  RBAC git:(main) ✗ mv rbac.yml manager.yml
➜  RBAC git:(main) ✗ kubectl apply -f manager.yml 
role.rbac.authorization.k8s.io/apache-manager created
➜  RBAC git:(main) ✗ kubectl get role -n rbac-ns
NAME             CREATED AT
apache-manager   2025-04-26T10:43:22Z
➜  RBAC git:(main) ✗ vim service-account.yml
➜  RBAC git:(main) ✗ kubectl apply -f service-account.yml 
serviceaccount/apache-user created
➜  RBAC git:(main) ✗ kubectl get serviceaccount -n rbac-ns
NAME          SECRETS   AGE
apache-user   0         16s
default       0         47m
➜  RBAC git:(main) ✗ kubectl auth can-i get pods -n apache
yes
➜  RBAC git:(main) ✗ kubectl auth can-i get pods -n apache --as=apache-user
no


➜  RBAC git:(main) ✗ vim role-binding.yml
➜  RBAC git:(main) ✗ kubectl apply -f role-binding.yml
rolebinding.rbac.authorization.k8s.io/apache-manager-rolebinding created
➜  RBAC git:(main) ✗ 

```
