# terraform-aws-route53-alias

Terraform module that implements "vanity" host names (e.g. `brand.com`) as `ALIAS` records to another Route53 DNS resource record (e.g. ELB/ALB, S3 Bucket Endpoint or CloudFront Distribution).
Unlike `CNAME` records, the synthetic `ALIAS` record works with zone apexes.


## Usage


**IMPORTANT:** The `master` branch is used in `source` just as an example. In your code, do not pin to `master` because there may be breaking changes between releases.
Instead pin to the release tag (e.g. `?ref=tags/x.y.z`) of one of our [latest releases](https://github.com/ceibo-it/terraform-aws-route53-alias/releases).


This will define a `A` resource record for `www.example.com` as an alias of the `aws_elb.example.dns_name`.

```terraform
module "production_www" {
  source          = "git::https://github.com/ceibo-it/terraform-aws-route53-alias.git?ref=master"
  aliases         = ["www.example.com.", "static1.cdn.example.com.", "static2.cdn.example.com"]
  parent_zone_id  = "${var.parent_zone_id}"
  target_dns_name = "${aws_elb.example.dns_name}"
  target_zone_id  = "${aws_elb.example.zone_id}"
}
```

## Requirements

| Name | Version |
|------|---------|
| terraform | ~> 0.12.0 |
| aws | ~> 2.0 |
| local | ~> 1.2 |

## Providers

| Name | Version |
|------|---------|
| aws | ~> 2.0 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| aliases | List of aliases | `list(string)` | n/a | yes |
| allow\_overwrite | Allow creation of this record in Terraform to overwrite an existing record, if any. This does not affect the ability to update the record in Terraform and does not prevent other resources within Terraform or manual Route 53 changes outside Terraform from overwriting this record. false by default. This configuration is not recommended for most environments | `bool` | `false` | no |
| enabled | Set to false to prevent the module from creating any resources | `bool` | `true` | no |
| evaluate\_target\_health | Set to true if you want Route 53 to determine whether to respond to DNS queries | `bool` | `false` | no |
| ipv6\_enabled | Set to true to enable an AAAA DNS record to be set as well as the A record | `bool` | `false` | no |
| parent\_zone\_id | ID of the hosted zone to contain this record  (or specify `parent_zone_name`) | `string` | `""` | no |
| parent\_zone\_name | Name of the hosted zone to contain this record (or specify `parent_zone_id`) | `string` | `""` | no |
| private\_zone | Is this a private hosted zone? | `bool` | `false` | no |
| target\_dns\_name | DNS name of target resource (e.g. ALB, ELB) | `string` | n/a | yes |
| target\_zone\_id | ID of target resource (e.g. ALB, ELB) | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| hostnames | List of DNS records |
| parent\_zone\_id | ID of the hosted zone to contain the records |
| parent\_zone\_name | Name of the hosted zone to contain the records |


## Copyright

Copyright © 2020 [Ceibo IT](https://ceibo.it/copyright)


## License 

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) 

See [LICENSE](LICENSE) for full details.

    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      https://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.


## NOTICE

terraform-aws-route53-alias
Copyright 2020 Ceibo


This product includes software developed by
Cloud Posse, LLC (c) (https://cloudposse.com/)
Licensed under Apache License, Version 2.0
Copyright © 2017-2019 Cloud Posse, LLC