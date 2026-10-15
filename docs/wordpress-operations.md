# WordPress AWS Operations & 503 Recovery

This runbook summarizes the **WordPress segment of Week 6 Assignment 3**, which reused the two-tier ALB/ASG/RDS lab.

## Validate components (lab checklist)

1. Confirm the WordPress HTTP application responds on its EC2 host.
2. Check the PHP runtime/PHP-FPM status and relevant web-server logs.
3. Verify database configuration for the WordPress `dbwordpress` database.
4. From EC2, use a MySQL client to test connectivity to the private RDS host; supply credentials securely at runtime.
5. Inspect ALB target-group health-check path and listener/target port.
6. Confirm the EC2 security group permits inbound traffic **from the ALB security group**.
7. Confirm a healthy target is registered before simulating replacement.

## Actual issue: HTTP 503 Service Unavailable

- **Finding in the report:** the ALB target group contained deregistered or unhealthy instances.
- **Actions recorded:** re-register running EC2 targets, verify health-check settings and security group source, confirm PHP-FPM/WordPress service, retest DB connectivity.
- **Observed outcome:** WordPress became accessible through the ALB again and RDS read/write operations worked.

## Availability exercise

The exercise detached one instance with **Replace detached instance** enabled and checked that remaining healthy targets continued to serve WordPress. This is an instance-level test, not proof of an AZ-wide outage.

## Not demonstrated

- A complete user-data/bootstrap install for WordPress
- Shared filesystem/assets between WordPress servers
- WordPress updates, backup/restore, WAF, HTTPS/TLS, secrets management
- A reproducible production rollout or formal load test

For the infrastructure setup itself see the related `aws-two-tier-high-availability` lab documentation.
