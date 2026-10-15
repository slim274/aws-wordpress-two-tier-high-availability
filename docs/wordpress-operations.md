# WordPress AWS Operations & HTTP 503 Recovery

**Scope:** WordPress phase of Week 6 Assignment 3. The report uses a shared ALB/ASG/RDS lab. This runbook is based on reported actions, not a production deployment template.

## Check the web and database tiers

1. Verify WordPress is reachable locally on each active EC2 application host.
2. Check the installed web server/PHP-FPM service and logs; confirm WordPress configuration references the RDS MySQL database (`dbwordpress`).
3. Use the MySQL client from EC2 to test the private RDS connection. Do not print or commit passwords.
4. Inspect target-group registration, health-check path `/`, port 80, and ALB listener rules.
5. Verify the EC2 security group permits HTTP traffic **from the ALB security group**; RDS should accept MySQL only from the designated EC2 security group.
6. Ensure healthy instances exist before carrying out any disruptive test.

## Documented incident: 503 Service Unavailable

**Symptom:** the ALB did not have consistently healthy/registered targets.

**Actions reported:** re-registered running EC2 instances, reviewed health checks and port settings, confirmed relevant ALB→EC2 permissions, checked PHP-FPM and WordPress services, and verified EC2→RDS MySQL connectivity.

**Reported result:** WordPress loaded again through the ALB; database read/write operations worked.

## Documented availability exercise

One instance was detached with **Replace detached instance** enabled in the Auto Scaling Group. During observation, WordPress continued loading through the ALB while remaining healthy instances served traffic.

**What this demonstrates:** an instance-level replacement/availability check. **What it does not demonstrate:** loss of an entire Availability Zone, synchronized WordPress uploads/themes across all instances, or a complete production recovery process.

## Important configuration gap

The internship report specifies both public and private ASG subnets in different sections; do not claim a definite ASG subnet placement without verifying the original AWS evidence. Also, WordPress installation/bootstrapping on every replacement instance was not documented as automated.
