---
# ----------------------------------------------------------------------------
#
#     ***     AUTO GENERATED CODE    ***    Type: MMv1     ***
#
# ----------------------------------------------------------------------------
#
#     This file is automatically generated by Magic Modules and manual
#     changes will be clobbered when the file is regenerated.
#
#     Please read more about how to change this file in
#     .github/CONTRIBUTING.md.
#
# ----------------------------------------------------------------------------
subcategory: "Compute Engine"
layout: "google"
page_title: "Google: google_compute_address"
sidebar_current: "docs-google-compute-address"
description: |-
  Represents an Address resource.
---

# google\_compute\_address

Represents an Address resource.

Each virtual machine instance has an ephemeral internal IP address and,
optionally, an external IP address. To communicate between instances on
the same network, you can use an instance's internal IP address. To
communicate with the Internet and instances outside of the same network,
you must specify the instance's external IP address.

Internal IP addresses are ephemeral and only belong to an instance for
the lifetime of the instance; if the instance is deleted and recreated,
the instance is assigned a new internal IP address, either by Compute
Engine or by you. External IP addresses can be either ephemeral or
static.


To get more information about Address, see:

* [API documentation](https://cloud.google.com/compute/docs/reference/beta/addresses)
* How-to Guides
    * [Reserving a Static External IP Address](https://cloud.google.com/compute/docs/instances-and-network)
    * [Reserving a Static Internal IP Address](https://cloud.google.com/compute/docs/ip-addresses/reserve-static-internal-ip-address)

<div class = "oics-button" style="float: right; margin: 0 0 -15px">
  <a href="https://console.cloud.google.com/cloudshell/open?cloudshell_git_repo=https%3A%2F%2Fgithub.com%2Fterraform-google-modules%2Fdocs-examples.git&cloudshell_working_dir=address_basic&cloudshell_image=gcr.io%2Fgraphite-cloud-shell-images%2Fterraform%3Alatest&open_in_editor=main.tf&cloudshell_print=.%2Fmotd&cloudshell_tutorial=.%2Ftutorial.md" target="_blank">
    <img alt="Open in Cloud Shell" src="//gstatic.com/cloudssh/images/open-btn.svg" style="max-height: 44px; margin: 32px auto; max-width: 100%;">
  </a>
</div>
## Example Usage - Address Basic


```hcl
resource "google_compute_address" "ip_address" {
  name = "my-address"
}
```
<div class = "oics-button" style="float: right; margin: 0 0 -15px">
  <a href="https://console.cloud.google.com/cloudshell/open?cloudshell_git_repo=https%3A%2F%2Fgithub.com%2Fterraform-google-modules%2Fdocs-examples.git&cloudshell_working_dir=address_with_subnetwork&cloudshell_image=gcr.io%2Fgraphite-cloud-shell-images%2Fterraform%3Alatest&open_in_editor=main.tf&cloudshell_print=.%2Fmotd&cloudshell_tutorial=.%2Ftutorial.md" target="_blank">
    <img alt="Open in Cloud Shell" src="//gstatic.com/cloudssh/images/open-btn.svg" style="max-height: 44px; margin: 32px auto; max-width: 100%;">
  </a>
</div>
## Example Usage - Address With Subnetwork


```hcl
resource "google_compute_network" "default" {
  name = "my-network"
}

resource "google_compute_subnetwork" "default" {
  name          = "my-subnet"
  ip_cidr_range = "10.0.0.0/16"
  region        = "us-central1"
  network       = google_compute_network.default.id
}

resource "google_compute_address" "internal_with_subnet_and_address" {
  name         = "my-internal-address"
  subnetwork   = google_compute_subnetwork.default.id
  address_type = "INTERNAL"
  address      = "10.0.42.42"
  region       = "us-central1"
}
```
<div class = "oics-button" style="float: right; margin: 0 0 -15px">
  <a href="https://console.cloud.google.com/cloudshell/open?cloudshell_git_repo=https%3A%2F%2Fgithub.com%2Fterraform-google-modules%2Fdocs-examples.git&cloudshell_working_dir=address_with_gce_endpoint&cloudshell_image=gcr.io%2Fgraphite-cloud-shell-images%2Fterraform%3Alatest&open_in_editor=main.tf&cloudshell_print=.%2Fmotd&cloudshell_tutorial=.%2Ftutorial.md" target="_blank">
    <img alt="Open in Cloud Shell" src="//gstatic.com/cloudssh/images/open-btn.svg" style="max-height: 44px; margin: 32px auto; max-width: 100%;">
  </a>
</div>
## Example Usage - Address With Gce Endpoint


```hcl
resource "google_compute_address" "internal_with_gce_endpoint" {
  name         = "my-internal-address-"
  address_type = "INTERNAL"
  purpose      = "GCE_ENDPOINT"
}
```
<div class = "oics-button" style="float: right; margin: 0 0 -15px">
  <a href="https://console.cloud.google.com/cloudshell/open?cloudshell_git_repo=https%3A%2F%2Fgithub.com%2Fterraform-google-modules%2Fdocs-examples.git&cloudshell_working_dir=instance_with_ip&cloudshell_image=gcr.io%2Fgraphite-cloud-shell-images%2Fterraform%3Alatest&open_in_editor=main.tf&cloudshell_print=.%2Fmotd&cloudshell_tutorial=.%2Ftutorial.md" target="_blank">
    <img alt="Open in Cloud Shell" src="//gstatic.com/cloudssh/images/open-btn.svg" style="max-height: 44px; margin: 32px auto; max-width: 100%;">
  </a>
</div>
## Example Usage - Instance With Ip


```hcl
resource "google_compute_address" "static" {
  name = "ipv4-address"
}

data "google_compute_image" "debian_image" {
  family  = "debian-9"
  project = "debian-cloud"
}

resource "google_compute_instance" "instance_with_ip" {
  name         = "vm-instance"
  machine_type = "f1-micro"
  zone         = "us-central1-a"

  boot_disk {
    initialize_params {
      image = data.google_compute_image.debian_image.self_link
    }
  }

  network_interface {
    network = "default"
    access_config {
      nat_ip = google_compute_address.static.address
    }
  }
}
```
<div class = "oics-button" style="float: right; margin: 0 0 -15px">
  <a href="https://console.cloud.google.com/cloudshell/open?cloudshell_git_repo=https%3A%2F%2Fgithub.com%2Fterraform-google-modules%2Fdocs-examples.git&cloudshell_working_dir=compute_address_ipsec_interconnect&cloudshell_image=gcr.io%2Fgraphite-cloud-shell-images%2Fterraform%3Alatest&open_in_editor=main.tf&cloudshell_print=.%2Fmotd&cloudshell_tutorial=.%2Ftutorial.md" target="_blank">
    <img alt="Open in Cloud Shell" src="//gstatic.com/cloudssh/images/open-btn.svg" style="max-height: 44px; margin: 32px auto; max-width: 100%;">
  </a>
</div>
## Example Usage - Compute Address Ipsec Interconnect


```hcl
resource "google_compute_address" "ipsec-interconnect-address" {
  name          = "test-address"
  address_type  = "INTERNAL"
  purpose       = "IPSEC_INTERCONNECT"
  address       = "192.168.1.0"
  prefix_length = 29
  network       = google_compute_network.network.self_link
}

resource "google_compute_network" "network" {
  name                    = "test-network"
  auto_create_subnetworks = false
}
```

## Argument Reference

The following arguments are supported:


* `name` -
  (Required)
  Name of the resource. The name must be 1-63 characters long, and
  comply with RFC1035. Specifically, the name must be 1-63 characters
  long and match the regular expression `[a-z]([-a-z0-9]*[a-z0-9])?`
  which means the first character must be a lowercase letter, and all
  following characters must be a dash, lowercase letter, or digit,
  except the last character, which cannot be a dash.


- - -


* `address` -
  (Optional)
  The static external IP address represented by this resource. Only
  IPv4 is supported. An address may only be specified for INTERNAL
  address types. The IP address must be inside the specified subnetwork,
  if any.

* `address_type` -
  (Optional)
  The type of address to reserve.
  Default value is `EXTERNAL`.
  Possible values are `INTERNAL` and `EXTERNAL`.

* `description` -
  (Optional)
  An optional description of this resource.

* `purpose` -
  (Optional)
  The purpose of this resource, which can be one of the following values:
  * GCE_ENDPOINT for addresses that are used by VM instances, alias IP
    ranges, internal load balancers, and similar resources.
  * SHARED_LOADBALANCER_VIP for an address that can be used by multiple
    internal load balancers.
  * VPC_PEERING for addresses that are reserved for VPC peer networks.
  * IPSEC_INTERCONNECT for addresses created from a private IP range
    that are reserved for a VLAN attachment in an IPsec-encrypted Cloud
    Interconnect configuration. These addresses are regional resources.
  * PRIVATE_SERVICE_CONNECT for a private network address that is used
  to configure Private Service Connect. Only global internal addresses
  can use this purpose.
  This should only be set when using an Internal address.

* `network_tier` -
  (Optional)
  The networking tier used for configuring this address. If this field is not
  specified, it is assumed to be PREMIUM.
  Possible values are `PREMIUM` and `STANDARD`.

* `subnetwork` -
  (Optional)
  The URL of the subnetwork in which to reserve the address. If an IP
  address is specified, it must be within the subnetwork's IP range.
  This field can only be used with INTERNAL type with
  GCE_ENDPOINT/DNS_RESOLVER purposes.

* `labels` -
  (Optional, [Beta](https://terraform.io/docs/providers/google/guides/provider_versions.html))
  Labels to apply to this address.  A list of key->value pairs.

* `network` -
  (Optional)
  The URL of the network in which to reserve the address. This field
  can only be used with INTERNAL type with the VPC_PEERING and
  IPSEC_INTERCONNECT purposes.

* `prefix_length` -
  (Optional)
  The prefix length if the resource represents an IP range.

* `region` -
  (Optional)
  The Region in which the created address should reside.
  If it is not provided, the provider region is used.

* `project` - (Optional) The ID of the project in which the resource belongs.
    If it is not provided, the provider project is used.


## Attributes Reference

In addition to the arguments listed above, the following computed attributes are exported:

* `id` - an identifier for the resource with format `projects/{{project}}/regions/{{region}}/addresses/{{name}}`

* `creation_timestamp` -
  Creation timestamp in RFC3339 text format.

* `users` -
  The URLs of the resources that are using this address.

* `label_fingerprint` -
  ([Beta](https://terraform.io/docs/providers/google/guides/provider_versions.html))
  The fingerprint used for optimistic locking of this resource.  Used
  internally during updates.
* `self_link` - The URI of the created resource.


## Timeouts

This resource provides the following
[Timeouts](/docs/configuration/resources.html#timeouts) configuration options:

- `create` - Default is 20 minutes.
- `update` - Default is 20 minutes.
- `delete` - Default is 20 minutes.

## Import


Address can be imported using any of these accepted formats:

```
$ terraform import google_compute_address.default projects/{{project}}/regions/{{region}}/addresses/{{name}}
$ terraform import google_compute_address.default {{project}}/{{region}}/{{name}}
$ terraform import google_compute_address.default {{region}}/{{name}}
$ terraform import google_compute_address.default {{name}}
```

## User Project Overrides

This resource supports [User Project Overrides](https://www.terraform.io/docs/providers/google/guides/provider_reference.html#user_project_override).
