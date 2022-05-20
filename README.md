# crossplane-demo

https://crossplane.github.io/docs/v1.8/getting-started/create-configuration.html

## Create and Install Azure PostgreSQL configuration package

  $ cd /postgresql-package
  $ curl -OL https://raw.githubusercontent.com/crossplane/crossplane/release-1.8/docs/snippets/package/azure/definition.yaml
  $ curl -OL https://raw.githubusercontent.com/crossplane/crossplane/release-1.8/docs/snippets/package/azure/composition.yaml
  $ curl -OL https://raw.githubusercontent.com/crossplane/crossplane/release-1.8/docs/snippets/package/azure/crossplane.yaml
  $ kubectl crossplane build configuration
  $ kubectl crossplane install configuration ....
  $ watch kubectl get pkg

## Create secret and configure Provider

  $ cd /postgresql-configure
  $ AWS_PROFILE=default && echo -e "[default]\naws_access_key_id = $(aws configure get aws_access_key_id --profile $AWS_PROFILE)\naws_secret_access_key = $(aws configure get aws_secret_access_key --profile $AWS_PROFILE)" > creds.conf
  $ kubectl create secret generic aws-creds -n crossplane-system --from-file=creds=./creds.conf
  $ kubectl apply -f https://raw.githubusercontent.com/crossplane/crossplane/release-1.8/docs/snippets/configure/aws/providerconfig.yaml

## Provision Azure PostgreSQL infrastructure  

  $ cd /postgresql-compose
  $ kubectl apply -f https://raw.githubusercontent.com/crossplane/crossplane/release-1.8/docs/snippets/compose/claim-azure.yaml 
  $ kubectl get postgresqlinstance my-db

  Note: while waiting for the PostgreSQLInstance to become ready, you may want to look at other resources in your cluster. The following commands will allow you to view groups of Crossplane resources:
  $ kubectl get claim: get all resources of all claim kinds, like PostgreSQLInstance.
  $ kubectl get composite: get all resources that are of composite kind, like XPostgreSQLInstance.
  $ kubectl get managed: get all resources that represent a unit of external infrastructure.
  $ kubectl get <name-of-provider>: get all resources related to <provider>.
  $ kubectl get crossplane: get all resources related to Crossplane.

## Consume provisioned service

  $ kubectl apply -f https://raw.githubusercontent.com/crossplane/crossplane/release-1.8/docs/snippets/compose/pod.yaml

## Clean up

  $ kubectl delete pod see-db
  $ kubectl delete postgresqlinstance my-db


