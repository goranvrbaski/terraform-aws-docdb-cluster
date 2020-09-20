AWS DocumentDB Cluster Module
===========

A terraform module to provide DocumentDB Cluster in AWS. This module will create DocumentDB cluster with instances.
Usage


```hcl
module "docdb-cluster" {
  source  = "goranvrbaski/documentdb-cluster/aws"

  cluster_name       = "docdb-cluster"
  master_username    = "doc-user"
  master_password    = "SuperCoolPassword123"
  availability_zones = ["eu-west-1a", "eu-west-1b", "eu-west-1c"]
  subnet_group_ids   = ["subnet-0e850eb742a6603fe", "subnet-0af42ab0203c31963", "subnet-0dca788fac5b76a63"]
  security_group_ids = ["sg-056b779af0e7e0129"]
}
```

Module Input Variables
----------------------

| Name   |      Type      |  Default Value |  Description |
|----------|:-------------:|:------:|:------ |
| `cluster_name` |  string | `n/a`| name for the cluster | 
| `master_username` |  string | `n/a` | name for the master user | 
| `master_password` |  string | `n/a` | value for the master password | 
| `instance_class` |  string | `"db.t3.medium"`| documentdb instance class |
| `instance_count` |  integer | `2` | number of documentdb instances in the cluster | 
| `subnet_group_ids` |  list | `[]` | list of subnet ids where to create documentdb cluster | 
| `security_group_ids` |  list | `[]` | list of security group ids to attach to the cluster | 
| `availability_zones` |  list | `[]` | list of availability zones to put the instances in | 
| `backup_retention_period` |  integer | `7`| backup retention period for the cluster | 
| `backup_window` |  string | `07:00-09:00`| backup window for the cluster | 
| `maintenance_window` |  string | `Mon:00:00-Mon:03:00`| maintenance window for the cluster | 
| `skip_final_snapshot` | bool | `true` | skip creating documentdb snapshot on deleting cluster | 
| `storage_encrypted` | bool | `true` | encrypt data at rest |
| `tags` | map(string) | `{ terraform = true }` | attach tags to documentdb |


Outputs
=======

| Name   |      Type      |  Description |
|----------|:-------------:|:------:|
| `cluster_id` |  string | the cluster id |
| `cluster_arn` |  string | the cluster arn |
| `cluster_members` |  list(string) | list of the cluster instances |
| `cluster_endpoint` | string | the cluster endpoint for read/write |
| `cluster_reader_endpoint` | string | the cluster endpoint optimized for read |
| `master_username` | string | the cluster master username |
| `master_password` | string | the cluster master password |
