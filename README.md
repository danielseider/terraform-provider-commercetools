# commercetools Terraform Provider

[![Test status](https://github.com/labd/terraform-provider-commercetools/workflows/Run%20Tests/badge.svg)](https://github.com/labd/terraform-provider-commercetools/actions?query=workflow%3A%22Run+Tests%22)
[![codecov](https://codecov.io/gh/LabD/terraform-provider-commercetools/branch/master/graph/badge.svg)](https://codecov.io/gh/LabD/terraform-provider-commercetools)
[![Go Report Card](https://goreportcard.com/badge/github.com/labd/terraform-provider-commercetools)](https://goreportcard.com/report/github.com/labd/terraform-provider-commercetools)


The Terraform commercetools provider allows you to configure
your [commercetools](https://commercetools.com/) project with
infrastructure-as-code principles.

# Commercial support

Need support implementing this terraform module in your organization? We are
able to offer support. Please contact us at opensource@labdigital.nl

# Quick start

[Read our documentation](https://registry.terraform.io/providers/labd/commercetools/latest/docs)
and check out the [examples](https://registry.terraform.io/providers/labd/commercetools/latest/docs/guides/extensions).


## Usage

The provider is distributed via the Terraform registry. To use it you need to configure the [`required_provider`](https://www.terraform.io/language/providers/requirements#requiring-providers) block. For example:

```hcl
terraform {
  required_providers {
    commercetools = {
      source = "labd/commercetools"
      
      # It's recommended to pin the version, e.g.:
      # version = "~> 1.4.0"
    }
  }
}
```

# Binaries

Packages of the releases are available at
https://github.com/labd/terraform-provider-commercetools/releases See the
[terraform documentation](https://www.terraform.io/docs/configuration/providers.html#third-party-plugins)
for more information about installing third-party providers.

# Contributing

## Building the provider

Clone repository to: `$GOPATH/src/github.com/labd/terraform-provider-commercetools`

```sh
$ mkdir -p $GOPATH/src/github.com/labd; cd $GOPATH/src/github.com/labd
$ git clone git@github.com:labd/terraform-provider-commercetools
```

Enter the provider directory and build the provider

```sh
$ cd $GOPATH/src/github.com/labd/terraform-provider-commercetools
$ make build
```

To then locally test:

```sh
$ cd $GOPATH/src/github.com/labd/terraform-provider-commercetools
$ make build-local
```
A build is created `terraform-provider-commercetools_99.0.0` in the root directory and added to plugin folder available locally:
```sh
~/.terraform.d/plugins/local/labd/commercetools/99.0.0/${OS_ARCH}/terraform-provider-commercetools_v99.0.0
```

Use version `99.0.0` in the provider to test your changes locally

```hcl
terraform {
  required_providers {
    commercetools = {
      source = "labd/commercetools"
      version = "99.0.0"
    }
  }
}
```


## Adding new resources
When commercetools releases new features which include new resources these need to be implemented
in terraform as new resources too. This provider is currently undergoing a migration path to
move from [terraform-plugin-sdk](https://github.com/hashicorp/terraform-plugin-sdk/) to the new
[terraform-plugin-framework](https://github.com/hashicorp/terraform-plugin-framework/). All new
resources therefore need to be written using the terraform-plugin-framework module. See the
`subscription` component as example.

## Debugging / Troubleshooting

There are two environment settings for troubleshooting:

- `TF_LOG=INFO` enables debug output for Terraform.
- `CTP_DEBUG=1` enables debug output for the Commercetools GO SDK this provider uses.

Note this generates a lot of output!

## Releasing

When pushing a new tag prefixed with `v` a GitHub action will automatically
use Goreleaser to build and release the build.

```sh
git tag <release> -m "Release <release>" # please use semantic version, so always vX.Y.Z
git push --follow-tags
```

## Testing

### Running the unit tests

```sh
$ make test
```

### Running an Acceptance Test

In order to run the full suite of Acceptance tests, run `make testacc`.

**NOTE:** Acceptance tests create real resources.

Prior to running the tests provider configuration details such as access keys
must be made available as environment variables.

Since we need to be able to create commercetools resources, we need the
commercetools API credentials. So in order for the acceptance tests to run
correctly please provide all of the following:

```sh
export CTP_CLIENT_ID=...
export CTP_CLIENT_SECRET=...
export CTP_PROJECT_KEY=...
export CTP_SCOPES=...
```

For convenience, place a `testenv.sh` in your `local` folder (which is
included in .gitignore) where you can store these environment variables.

Tests can then be started by running

```sh
$ source local/testenv.sh
$ make testacc
```

## Authors

This project is developed by [Lab Digital](https://www.labdigital.nl). We
welcome additional contributors. Please see our
[GitHub repository](https://github.com/labd/terraform-provider-commercetools)
for more information.
