# GitOps Repository for spring-petclinic-ops

This repo contains all the declarative operations resources for the management of the spring-petclinic-ops app.

## How to Use this GitOps repo with your application

1. Fork/clone/copy contents of this repo and create a new repo named <your-app>-ops.
2. Update the values.yaml file according to your application and commit the changes.
   <mark>**Note: If you do not need a pull secret as part of your deployment, comment the pullSecret.enabled line and that will disable the pull secret injection.</mark>
   At minimum, the following fields should be updated -
   ```yaml
   ---
   replicaCount: 1
   
   image:
     pullPolicy: Always
   
   service:
     name: petclinic #REPLACE THIS VALUE
     type: ClusterIP
     port: 80
     targetport: 8080
   
   probe:
     readypath: /
     livepath:  /
   
   route:
     name: petclinic #REPLACE THIS VALUE
     enabled: True
     annotations: {
     }
     path: /
   
   resources:
     # We usually recommend not to specify default resources and to leave this as a conscious
     # choice for the user. This also increases chances charts run on environments with little
     # resources, such as Minikube. If you do want to specify resources, uncomment the following
     # lines, adjust them as necessary, and remove the curly braces after 'resources:'.
     # limits:   #  cpu: 100m
     #  memory: 128Mi
     # requests:   #  cpu: 100m
     #  memory: 128Mi
   
   nodeSelector: {
   }
   
   tolerations: []
   
   affinity: {
   }
   
   pullSecret:
     enabled: "true" #REPLACE THIS VALUE
     secretName: "pull-secret" #REPLACE THIS VALUE
     secretKey: ".dockerconfigjson" #REPLACE THIS VALUE
   
   # Vault values
   
   # Vault storage backend
   vaultStorage: "vault-backend" #REPLACE THIS VALUE
   vaultSecret: "vault-secret" #REPLACE THIS VALUE
   vaultKey: "token" #REPLACE THIS VALUE
   
   # Vault Keys
   vault:
     registry2: #REPLACE THIS VALUE
       host: #REPLACE THIS VALUE
         key: secret/registry2 #REPLACE THIS VALUE
         property: host #REPLACE THIS VALUE
       user: #REPLACE THIS VALUE
         key: secret/registry2 #REPLACE THIS VALUE
         property: user #REPLACE THIS VALUE
       password: #REPLACE THIS VALUE
         key: secret/registry2 #REPLACE THIS VALUE
         property: password #REPLACE THIS VALUE
   ```
3. Update your application's psr.yaml deploy steps to point at your <your-app>-ops repo. More information about this can be found in this [README](https://github.com/ploigos/ploigos-github-workflows/blob/main/README.md).