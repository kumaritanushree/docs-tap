# Install Tanzu Supply Chain manually (not recommended)

This topic tells you how to install Tanzu Supply Chain manually. This installation method is not recommended.

{{> 'partials/supply-chain/beta-banner' }}

To install Tanzu Supply Chain manually, you must install additional packages that are not bundled with
existing installation profiles.

The following Supply Chain packages are required.

- `supply-chain.apps.tanzu.vmware.com`
- `supply-chain-catalog.apps.tanzu.vmware.com`
- `managed-resource-controller.apps.tanzu.vmware.com`

The following Component packages are required if you're authoring a supply chain:

- `source.component.apps.tanzu.vmware.com`
- `conventions.component.apps.tanzu.vmware.com`
- `buildpack-build.component.apps.tanzu.vmware.com`
- `alm-catalog.component.apps.tanzu.vmware.com`
- `git-writer.component.apps.tanzu.vmware.com`
- `trivy-scanning.component.apps.tanzu.vmware.com`

<br>

1. To install these packages, run the following script:

  ```shell
  export SUPPLY_CHAIN_VERSION=$(kubectl get package -n tap-install -o=jsonpath='{.items[?(@.spec.refName=="supply-chain.apps.tanzu.vmware.com")].spec.version}')
  echo $SUPPLY_CHAIN_VERSION

  tanzu package install supply-chain \
    --package supply-chain.apps.tanzu.vmware.com \
    --version $SUPPLY_CHAIN_VERSION \
    --namespace tap-install

  export SUPPLY_CHAIN_CATALOG_VERSION=$(kubectl get package -n tap-install -o=jsonpath='{.items[?(@.spec.refName=="supply-chain-catalog.apps.tanzu.vmware.com")].spec.version}')
  echo $SUPPLY_CHAIN_CATALOG_VERSION

  tanzu package install supply-chain-catalog \
    --package supply-chain-catalog.apps.tanzu.vmware.com \
    --version $SUPPLY_CHAIN_CATALOG_VERSION \
    --namespace tap-install

  export MANAGED_RESOURCE_VERSION=$(kubectl get package -n tap-install -o=jsonpath='{.items[?(@.spec.refName=="managed-resource-controller.apps.tanzu.vmware.com")].spec.version}')
  echo $MANAGED_RESOURCE_VERSION

  tanzu package install managed-resource-controller \
    --package managed-resource-controller.apps.tanzu.vmware.com \
    --version $MANAGED_RESOURCE_VERSION \
    --namespace tap-install

  export SOURCE_COMPONENT_VERSION=$(kubectl get package -n tap-install -o=jsonpath='{.items[?(@.spec.refName=="source.component.apps.tanzu.vmware.com")].spec.version}')
  echo $SOURCE_COMPONENT_VERSION

  tanzu package install source-component \
    --package source.component.apps.tanzu.vmware.com \
    --version $SOURCE_COMPONENT_VERSION \
    --namespace tap-install

  export CONVENTIONS_COMPONENT_VERSION=$(kubectl get package -n tap-install -o=jsonpath='{.items[?(@.spec.refName=="conventions.component.apps.tanzu.vmware.com")].spec.version}')
  echo $CONVENTIONS_COMPONENT_VERSION

  tanzu package install conventions-component \
    --package conventions.component.apps.tanzu.vmware.com \
    --version $CONVENTIONS_COMPONENT_VERSION \
    --namespace tap-install

  export BUILDPACK_COMPONENT_VERSION=$(kubectl get package -n tap-install -o=jsonpath='{.items[?(@.spec.refName=="buildpack-build.component.apps.tanzu.vmware.com")].spec.version}')
  echo $BUILDPACK_COMPONENT_VERSION

  tanzu package install buildpack-build-component \
    --package buildpack-build.component.apps.tanzu.vmware.com \
    --version $BUILDPACK_COMPONENT_VERSION \
    --namespace tap-install

  export ALM_CATALOG_COMPONENT_VERSION=$(kubectl get package -n tap-install -o=jsonpath='{.items[?(@.spec.refName=="alm-catalog.component.apps.tanzu.vmware.com")].spec.version}')
  echo $ALM_CATALOG_COMPONENT_VERSION

  tanzu package install alm-catalog-component \
    --package alm-catalog.component.apps.tanzu.vmware.com \
    --version $ALM_CATALOG_COMPONENT_VERSION \
    --namespace tap-install

  export GIT_WRITER_COMPONENT_VERSION=$(kubectl get package -n tap-install -o=jsonpath='{.items[?(@.spec.refName=="git-writer.component.apps.tanzu.vmware.com")].spec.version}')
  echo $GIT_WRITER_COMPONENT_VERSION

  tanzu package install git-writer-component \
    --package git-writer.component.apps.tanzu.vmware.com \
    --version $GIT_WRITER_COMPONENT_VERSION \
    --namespace tap-install
  ```

1. Confirm that the required packages are installed and reconciled successfully. Run:

  ```console
  kubectl get pkgi -A
  ```

  Example output

  ```console
  NAMESPACE     NAME                               PACKAGE NAME                                          PACKAGE VERSION                       DESCRIPTION           AGE
  tap-install   alm-catalog-component              alm-catalog.component.apps.tanzu.vmware.com           0.1.4                                 Reconcile succeeded   15d
  ...
  tap-install   buildpack-build-component          buildpack-build.component.apps.tanzu.vmware.com       0.0.2                                 Reconcile succeeded   15d
  ...
  tap-install   conventions-component              conventions.component.apps.tanzu.vmware.com           0.0.3                                 Reconcile succeeded   15d
  ...
  tap-install   git-writer-component               git-writer.component.apps.tanzu.vmware.com            0.1.3                                 Reconcile succeeded   15d
  ...
  tap-install   managed-resource-controller        managed-resource-controller.apps.tanzu.vmware.com     0.1.2                                 Reconcile succeeded   15d
  ...
  tap-install   namespace-provisioner              namespace-provisioner.apps.tanzu.vmware.com           0.6.2                                 Reconcile succeeded   15d
  ...
  tap-install   source-component                   source.component.apps.tanzu.vmware.com                0.0.1                                 Reconcile succeeded   15d
  ...
  tap-install   supply-chain                       supply-chain.apps.tanzu.vmware.com                    0.1.16                                Reconcile succeeded   15d
  tap-install   supply-chain-catalog               supply-chain-catalog.apps.tanzu.vmware.com            0.1.1                                 Reconcile succeeded   15d
  ...
  tap-install   trivy-app-scanning-component       trivy.app-scanning.component.apps.tanzu.vmware.com    0.0.1-alpha.build.40376886+b5f4e614   Reconcile succeeded   15d
  ...
  ```
