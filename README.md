<!-- This file was automatically generated by the `geine`. Make all changes to `README.yaml` and run `make readme` to rebuild this file. -->

<p align="center"> <img src="https://user-images.githubusercontent.com/50652676/62349836-882fef80-b51e-11e9-99e3-7b974309c7e3.png" width="100" height="100"></p>


<h1 align="center">
    Terraform AWS VPC
</h1>

<p align="center" style="font-size: 1.2rem;"> 
    Terraform module vpc to create new modules using this as baseline
     </p>

<p align="center">

<a href="https://github.com/clouddrove/terraform-aws-vpc/releases/latest">
  <img src="https://img.shields.io/github/release/clouddrove/terraform-aws-vpc.svg" alt="Latest Release">
</a>
<a href="https://github.com/clouddrove/terraform-aws-vpc/actions/workflows/tfsec.yml">
  <img src="https://github.com/clouddrove/terraform-aws-vpc/actions/workflows/tfsec.yml/badge.svg" alt="tfsec">
</a>
<a href="LICENSE.md">
  <img src="https://img.shields.io/badge/License-APACHE-blue.svg" alt="Licence">
</a>


</p>
<p align="center">

<a href='https://facebook.com/sharer/sharer.php?u=https://github.com/clouddrove/terraform-aws-vpc'>
  <img title="Share on Facebook" src="https://user-images.githubusercontent.com/50652676/62817743-4f64cb80-bb59-11e9-90c7-b057252ded50.png" />
</a>
<a href='https://www.linkedin.com/shareArticle?mini=true&title=Terraform+AWS+VPC&url=https://github.com/clouddrove/terraform-aws-vpc'>
  <img title="Share on LinkedIn" src="https://user-images.githubusercontent.com/50652676/62817742-4e339e80-bb59-11e9-87b9-a1f68cae1049.png" />
</a>
<a href='https://twitter.com/intent/tweet/?text=Terraform+AWS+VPC&url=https://github.com/clouddrove/terraform-aws-vpc'>
  <img title="Share on Twitter" src="https://user-images.githubusercontent.com/50652676/62817740-4c69db00-bb59-11e9-8a79-3580fbbf6d5c.png" />
</a>

</p>
<hr>


We eat, drink, sleep and most importantly love **DevOps**. We are working towards strategies for standardizing architecture while ensuring security for the infrastructure. We are strong believer of the philosophy <b>Bigger problems are always solved by breaking them into smaller manageable problems</b>. Resonating with microservices architecture, it is considered best-practice to run database, cluster, storage in smaller <b>connected yet manageable pieces</b> within the infrastructure. 

This module is basically combination of [Terraform open source](https://www.terraform.io/) and includes automatation tests and examples. It also helps to create and improve your infrastructure with minimalistic code instead of maintaining the whole infrastructure code yourself.

We have [*fifty plus terraform modules*][terraform_modules]. A few of them are comepleted and are available for open source usage while a few others are in progress.




## Prerequisites

This module has a few dependencies: 






## Examples


**IMPORTANT:** Since the `master` branch used in `source` varies based on new modifications, we suggest that you use the release versions [here](https://github.com/clouddrove/terraform-aws-vpc/releases).


Here are some examples of how you can use this module in your inventory structure:

### vpc basic example
```hcl
    module "vpc" {
    source                              = "clouddrove/vpc/aws"
    version                             = "1.3.1"
    name                                = "vpc"
    environment                         = "example"
    cidr_block                          = "10.0.0.0/16"
    enable_flow_log                     = true # Flow logs will be stored in cloudwatch log group. Variables passed in default.
    create_flow_log_cloudwatch_iam_role = true
    additional_cidr_block               = ["172.3.0.0/16", "172.2.0.0/16"]
    dhcp_options_domain_name            = "service.consul"
    dhcp_options_domain_name_servers    = ["127.0.0.1", "10.10.0.2"]
   }
```

### vpc complete example
```hcl
    module "vpc" {
    source                           = "clouddrove/vpc/aws"
    version                          = "1.3.1"
    name                             = "vpc"
    environment                      = "example"
    cidr_block                       = "10.0.0.0/16"
    enable_flow_log                  = true
    flow_log_destination_type        = "s3"
    flow_logs_bucket_name            = "gc-vpc-flow-logs-bucket"
    additional_cidr_block            = ["172.3.0.0/16", "172.2.0.0/16"]
    dhcp_options_domain_name         = "service.consul"
    dhcp_options_domain_name_servers = ["127.0.0.1", "10.10.0.2"]
   }
```






## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| additional\_cidr\_block | List of secondary CIDR blocks of the VPC. | `list(string)` | `[]` | no |
| assign\_generated\_ipv6\_cidr\_block | Requests an Amazon-provided IPv6 CIDR block with a /56 prefix length for the VPC. You cannot specify the range of IP addresses, or the size of the CIDR block. Conflicts with ipv6\_ipam\_pool\_id | `bool` | `true` | no |
| aws\_default\_network\_acl | A boolean flag to enable/disable Default Network acl in the VPC. | `bool` | `true` | no |
| aws\_default\_route\_table | A boolean flag to enable/disable Default Route Table in the VPC. | `bool` | `true` | no |
| cidr\_block | CIDR for the VPC. | `string` | `""` | no |
| create\_flow\_log\_cloudwatch\_iam\_role | Flag to be set true when cloudwatch iam role is to be created when flow log destination type is set to cloudwatch logs. | `bool` | `false` | no |
| default\_network\_acl\_egress | List of maps of egress rules to set on the Default Network ACL | `list(map(string))` | <pre>[<br>  {<br>    "action": "allow",<br>    "cidr_block": "0.0.0.0/0",<br>    "from_port": 0,<br>    "protocol": "-1",<br>    "rule_no": 100,<br>    "to_port": 0<br>  },<br>  {<br>    "action": "allow",<br>    "from_port": 0,<br>    "ipv6_cidr_block": "::/0",<br>    "protocol": "-1",<br>    "rule_no": 101,<br>    "to_port": 0<br>  }<br>]</pre> | no |
| default\_network\_acl\_ingress | List of maps of ingress rules to set on the Default Network ACL | `list(map(string))` | <pre>[<br>  {<br>    "action": "allow",<br>    "cidr_block": "0.0.0.0/0",<br>    "from_port": 0,<br>    "protocol": "-1",<br>    "rule_no": 100,<br>    "to_port": 0<br>  },<br>  {<br>    "action": "allow",<br>    "from_port": 0,<br>    "ipv6_cidr_block": "::/0",<br>    "protocol": "-1",<br>    "rule_no": 101,<br>    "to_port": 0<br>  }<br>]</pre> | no |
| default\_route\_table\_routes | Configuration block of routes. | `list(map(string))` | `[]` | no |
| default\_security\_group\_egress | List of maps of egress rules to set on the default security group | `list(map(string))` | `[]` | no |
| default\_security\_group\_ingress | List of maps of ingress rules to set on the default security group | `list(map(string))` | `[]` | no |
| dhcp\_options\_domain\_name | Specifies DNS name for DHCP options set (requires enable\_dhcp\_options set to true) | `string` | `"service.consul"` | no |
| dhcp\_options\_domain\_name\_servers | Specify a list of DNS server addresses for DHCP options set, default to AWS provided (requires enable\_dhcp\_options set to true) | `list(string)` | <pre>[<br>  "AmazonProvidedDNS"<br>]</pre> | no |
| dhcp\_options\_netbios\_name\_servers | Specify a list of netbios servers for DHCP options set (requires enable\_dhcp\_options set to true) | `list(string)` | `[]` | no |
| dhcp\_options\_netbios\_node\_type | Specify netbios node\_type for DHCP options set (requires enable\_dhcp\_options set to true) | `string` | `""` | no |
| dhcp\_options\_ntp\_servers | Specify a list of NTP servers for DHCP options set (requires enable\_dhcp\_options set to true) | `list(string)` | `[]` | no |
| dns\_hostnames\_enabled | A boolean flag to enable/disable DNS hostnames in the VPC. | `bool` | `true` | no |
| dns\_support\_enabled | A boolean flag to enable/disable DNS support in the VPC. | `bool` | `true` | no |
| enable | Flag to control the vpc creation. | `bool` | `true` | no |
| enable\_dhcp\_options | Should be true if you want to specify a DHCP options set with a custom domain name, DNS servers, NTP servers, netbios servers, and/or netbios server type | `bool` | `false` | no |
| enable\_flow\_log | Enable vpc\_flow\_log logs. | `bool` | `false` | no |
| enable\_key\_rotation | Specifies whether key rotation is enabled. Defaults to true(security best practice) | `bool` | `true` | no |
| enable\_network\_address\_usage\_metrics | Determines whether network address usage metrics are enabled for the VPC | `bool` | `null` | no |
| enabled\_ipv6\_egress\_only\_internet\_gateway | A boolean flag to enable/disable IPv6 Egress-Only Internet Gateway creation | `bool` | `true` | no |
| environment | Environment (e.g. `prod`, `dev`, `staging`). | `string` | `""` | no |
| flow\_log\_cloudwatch\_log\_group\_retention\_in\_days | Specifies the number of days you want to retain log events in the specified log group for VPC flow logs | `number` | `null` | no |
| flow\_log\_destination\_arn | ARN of destination where vpc flow logs are to stored. Can be of existing s3 or existing cloudwatch log group. | `string` | `null` | no |
| flow\_log\_destination\_type | Type of flow log destination. Can be s3 or cloud-watch-logs | `string` | `"cloud-watch-logs"` | no |
| flow\_log\_file\_format | (Optional) The format for the flow log. Valid values: `plain-text`, `parquet` | `string` | `null` | no |
| flow\_log\_hive\_compatible\_partitions | (Optional) Indicates whether to use Hive-compatible prefixes for flow logs stored in Amazon S3 | `bool` | `false` | no |
| flow\_log\_iam\_role\_arn | The ARN for the IAM role that's used to post flow logs to a CloudWatch Logs log group. When flow\_log\_destination\_arn is set to ARN of Cloudwatch Logs, this argument needs to be provided | `string` | `null` | no |
| flow\_log\_log\_format | The fields to include in the flow log record, in the order in which they should appear | `string` | `null` | no |
| flow\_log\_max\_aggregation\_interval | The maximum interval of time during which a flow of packets is captured and aggregated into a flow log record. Valid Values: `60` seconds or `600` seconds | `number` | `600` | no |
| flow\_log\_per\_hour\_partition | (Optional) Indicates whether to partition the flow log per hour. This reduces the cost and response time for queries | `bool` | `false` | no |
| flow\_log\_traffic\_type | The type of traffic to capture. Valid values: ACCEPT, REJECT, ALL | `string` | `"ALL"` | no |
| flow\_logs\_bucket\_name | Name  (e.g. `mybucket` or `bucket101`). | `string` | `null` | no |
| instance\_tenancy | A tenancy option for instances launched into the VPC. | `string` | `"default"` | no |
| ipam\_pool\_enable | Flag to be set true when using ipam for cidr. | `bool` | `false` | no |
| ipv4\_ipam\_pool\_id | The ID of an IPv4 IPAM pool you want to use for allocating this VPC's CIDR. | `string` | `""` | no |
| ipv4\_netmask\_length | The netmask length of the IPv4 CIDR you want to allocate to this VPC. Requires specifying a ipv4\_ipam\_pool\_id | `string` | `null` | no |
| ipv6\_cidr\_block | IPv6 CIDR for the VPC. | `string` | `null` | no |
| ipv6\_cidr\_block\_network\_border\_group | Set this to restrict advertisement of public addresses to a specific Network Border Group such as a LocalZone. | `string` | `null` | no |
| ipv6\_ipam\_pool\_id | The ID of an IPv6 IPAM pool you want to use for allocating this VPC's CIDR. | `string` | `null` | no |
| ipv6\_netmask\_length | The netmask length of the IPv4 CIDR you want to allocate to this VPC. Requires specifying a ipv6\_ipam\_pool\_id | `string` | `null` | no |
| kms\_key\_deletion\_window | KMS Key deletion window in days. | `number` | `10` | no |
| label\_order | Label order, e.g. `name`,`application`. | `list(any)` | <pre>[<br>  "name",<br>  "environment"<br>]</pre> | no |
| managedby | ManagedBy, eg 'CloudDrove' | `string` | `"hello@clouddrove.com"` | no |
| name | Name  (e.g. `app` or `cluster`). | `string` | `""` | no |
| repository | Terraform current module repo | `string` | `"https://github.com/clouddrove/terraform-aws-vpc"` | no |
| restrict\_default\_sg | Flag to control the restrict default sg creation. | `bool` | `true` | no |
| s3\_sse\_algorithm | Server-side encryption algorithm to use. Valid values are AES256 and aws:kms | `string` | `"aws:kms"` | no |
| vpc\_flow\_log\_permissions\_boundary | The ARN of the Permissions Boundary for the VPC Flow Log IAM Role | `string` | `null` | no |

## Outputs

| Name | Description |
|------|-------------|
| arn | Amazon Resource Name (ARN) of VPC |
| igw\_id | The ID of the Internet Gateway. |
| ipv6\_cidr\_block | The IPv6 CIDR block. |
| ipv6\_cidr\_block\_network\_border\_group | The IPv6 Network Border Group Zone name |
| ipv6\_egress\_only\_igw\_id | The ID of the egress-only Internet Gateway |
| tags | A mapping of tags to assign to the resource. |
| vpc\_arn | The ARN of the VPC |
| vpc\_cidr\_block | The CIDR block of the VPC. |
| vpc\_default\_network\_acl\_id | The ID of the network ACL created by default on VPC creation. |
| vpc\_default\_route\_table\_id | The ID of the route table created by default on VPC creation. |
| vpc\_default\_security\_group\_id | The ID of the security group created by default on VPC creation. |
| vpc\_id | The ID of the VPC. |
| vpc\_ipv6\_association\_id | The association ID for the IPv6 CIDR block. |
| vpc\_main\_route\_table\_id | The ID of the main route table associated with this VPC. |




## Testing
In this module testing is performed with [terratest](https://github.com/gruntwork-io/terratest) and it creates a small piece of infrastructure, matches the output like ARN, ID and Tags name etc and destroy infrastructure in your AWS account. This testing is written in GO, so you need a [GO environment](https://golang.org/doc/install) in your system. 

You need to run the following command in the testing folder:
```hcl
  go test -run Test
```



## Feedback 
If you come accross a bug or have any feedback, please log it in our [issue tracker](https://github.com/clouddrove/terraform-aws-vpc/issues), or feel free to drop us an email at [hello@clouddrove.com](mailto:hello@clouddrove.com).

If you have found it worth your time, go ahead and give us a ★ on [our GitHub](https://github.com/clouddrove/terraform-aws-vpc)!

## About us

At [CloudDrove][website], we offer expert guidance, implementation support and services to help organisations accelerate their journey to the cloud. Our services include docker and container orchestration, cloud migration and adoption, infrastructure automation, application modernisation and remediation, and performance engineering.

<p align="center">We are <b> The Cloud Experts!</b></p>
<hr />
<p align="center">We ❤️  <a href="https://github.com/clouddrove">Open Source</a> and you can check out <a href="https://github.com/clouddrove">our other modules</a> to get help with your new Cloud ideas.</p>

  [website]: https://clouddrove.com
  [github]: https://github.com/clouddrove
  [linkedin]: https://cpco.io/linkedin
  [twitter]: https://twitter.com/clouddrove/
  [email]: https://clouddrove.com/contact-us.html
  [terraform_modules]: https://github.com/clouddrove?utf8=%E2%9C%93&q=terraform-&type=&language=
