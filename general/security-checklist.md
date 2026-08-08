# Security Checklist

Run through this checklist before opening any pull request. Every item is a requirement, not a suggestion.

For the full security policy, see [SECURITY.md](https://github.com/aws-gomal-university/.github/blob/main/SECURITY.md).

---

## Credentials and Secrets

- [ ] No AWS access keys or secret keys committed anywhere in the codebase
- [ ] No API keys, tokens, or passwords present in any file
- [ ] No `.env` files committed (`.env` must be in `.gitignore`)
- [ ] A `.env.example` file is provided with placeholder values, not real ones
- [ ] AWS Secrets Manager, environment variables, or IAM roles are used in place of hardcoded credentials
- [ ] No credentials present in commit history (check with `git log -p`)

> If you accidentally committed a secret, do not just delete it from the latest commit. Notify a maintainer immediately so the credential can be rotated. The secret is still visible in commit history until properly purged.

---

## IAM and Permissions

- [ ] IAM roles and policies follow the principle of least privilege
- [ ] No wildcard (`*`) actions or resources in IAM policies unless explicitly justified
- [ ] No public S3 bucket access unless the use case explicitly requires it
- [ ] No overly permissive security group rules (e.g., `0.0.0.0/0` on sensitive ports)
- [ ] IAM changes have been reviewed by at least one other contributor before merging

---

## Dependencies

- [ ] All dependencies are pinned to specific versions
- [ ] No packages with known critical CVEs (check with `npm audit`, `pip-audit`, or equivalent)
- [ ] No unfamiliar or suspicious package names (verify before adding)

---

## Code

- [ ] No SQL queries built by string concatenation (use parameterized queries)
- [ ] No shell commands built from unvalidated user input
- [ ] Input validation is present where user data is accepted
- [ ] Error messages do not expose internal paths, stack traces, or configuration details
- [ ] Authentication and authorization checks are in place where required

---

## Infrastructure

- [ ] All cloud resources created by this project are documented in the README
- [ ] Cleanup instructions are provided for all resources
- [ ] No resources left running that are not needed for the project
- [ ] Terraform state files or CDK context files are not committed

---

## Repository Hygiene

- [ ] `.gitignore` is present and covers secrets, build artifacts, and local config
- [ ] No large binary files, datasets, or model weights committed
- [ ] No commented-out credential placeholders or debug values left in code

---

## Before You Merge

- [ ] You have reviewed your own diff (`git diff main..feature/your-branch`)
- [ ] All items above are checked
- [ ] If any security concern was found and resolved, it is noted in the PR description
