# crossplane-demo

https://crossplane.github.io/docs/v1.8/getting-started/create-configuration.html

## Create Azure "POSTGRESQL" configuration package
cd postgresql-package
curl -OL https://raw.githubusercontent.com/crossplane/crossplane/release-1.8/docs/snippets/package/azure/definition.yaml
curl -OL https://raw.githubusercontent.com/crossplane/crossplane/release-1.8/docs/snippets/package/azure/composition.yaml
curl -OL https://raw.githubusercontent.com/crossplane/crossplane/release-1.8/docs/snippets/package/azure/crossplane.yaml
kubectl crossplane build configuration



