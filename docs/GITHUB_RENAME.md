# Optional GitHub repository rename

**Recommended name:** `aws-wordpress-two-tier-high-availability`

**Suggested GitHub description:** `WordPress two-tier deployment on AWS EC2 and private RDS MySQL, with ALB, Auto Scaling, Multi-AZ networking, and HTTP 503 recovery evidence.`

The original existing repository name, `aws-wordpress-alb-rds`, is also accurate. You do **not** have to rename it to use this documentation.

If you choose to rename: open your repository's **Settings → General → Repository name** and change it to `aws-wordpress-two-tier-high-availability`.

For a local cloned copy, update the origin URL:

```bash
git remote set-url origin https://github.com/slim274/aws-wordpress-two-tier-high-availability.git
git remote -v
```

Review files and sensitive information before committing. Then:

```bash
git add README.md docs/ screenshots/ diagrams/ .gitignore
git diff --cached --check
git status --short
git commit -m "Correct WordPress two-tier documentation and evidence"
git push
```

**Note:** These instructions have not been executed on your GitHub account. The README shows both existing and recommended repository names until you complete a rename.
