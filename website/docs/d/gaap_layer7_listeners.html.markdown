---
layout: "tencentcloud"
page_title: "TencentCloud: tencentcloud_gaap_layer7_listeners"
sidebar_current: "docs-tencentcloud-datasource-gaap_layer7_listeners"
description: |-
  Use this data source to query gaap layer7 listeners.
---

# tencentcloud_gaap_layer7_listeners

Use this data source to query gaap layer7 listeners.

## Example Usage

```hcl
resource "tencentcloud_gaap_proxy" "foo" {
  name              = "ci-test-gaap-proxy"
  bandwidth         = 10
  concurrent        = 2
  access_region     = "SouthChina"
  realserver_region = "NorthChina"
}

resource "tencentcloud_gaap_layer7_listener" "foo" {
  protocol = "HTTP"
  name     = "ci-test-gaap-l7-listener"
  port     = 80
  proxy_id = "${tencentcloud_gaap_proxy.foo.id}"
}

data "tencentcloud_gaap_layer7_listeners" "listenerId" {
  protocol    = "HTTP"
  proxy_id    = "${tencentcloud_gaap_proxy.foo.id}"
  listener_id = "${tencentcloud_gaap_layer7_listener.foo.id}"
}
```

## Argument Reference

The following arguments are supported:

* `protocol` - (Required) Protocol of the layer7 listener to be queried, and the available values include `HTTP` and `HTTPS`.
* `proxy_id` - (Required) ID of the GAAP proxy to be queried.
* `listener_id` - (Optional) ID of the layer7 listener to be queried.
* `listener_name` - (Optional) Name of the layer7 listener to be queried.
* `port` - (Optional) Port of the layer7 listener to be queried.
* `result_output_file` - (Optional) Used to save results.

## Attributes Reference

In addition to all arguments above, the following attributes are exported:

* `listeners` - An information list of layer7 listeners. Each element contains the following attributes:
  * `auth_type` - Authentication type of the layer7 listener. `0` is one-way authentication and `1` is mutual authentication.
  * `certificate_id` - Certificate ID of the layer7 listener.
  * `client_certificate_id` - ID of the client certificate.
  * `create_time` - Creation time of the layer7 listener.
  * `forward_protocol` - Protocol type of the forwarding.
  * `id` - ID of the layer7 listener.
  * `name` - Name of the layer7 listener.
  * `port` - Port of the layer7 listener.
  * `protocol` - Protocol of the layer7 listener.
  * `status` - Status of the layer7 listener.


