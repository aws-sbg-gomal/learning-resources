# AWS Environment Setup

This guide walks through setting up your AWS environment for contributing to projects under AWS SBG Gomal University. Complete these steps before working on any cloud project.

---

## 1. Create an AWS Account

If you do not already have one, create a free AWS account at [aws.amazon.com](https://aws.amazon.com).

- Use your university email address if possible for consistency.
- Enable **MFA (Multi-Factor Authentication)** on your root account immediately after creation. Never use the root account for day-to-day work.

---

## 2. Create an IAM User

Do not use your root account credentials for any project work. Create a dedicated IAM user instead.

1. Sign in to the [AWS Console](https://console.aws.amazon.com) with your root account.
2. Navigate to **IAM** > **Users** > **Create user**.
3. Set a username (e.g., `yourname-dev`).
4. Attach the **AdministratorAccess** policy for initial setup (you can scope this down per project later).
5. Enable **Console access** and set a password.
6. Enable **MFA** on the IAM user as well.

> Never share IAM credentials. Never commit them to any repository.

---

## 3. Create an Access Key for CLI Use

1. In IAM, open your user and go to **Security credentials**.
2. Under **Access keys**, select **Create access key**.
3. Choose **CLI** as the use case.
4. Download the `.csv` file and store it securely. You will not be able to view the secret key again.

---

## 4. Install the AWS CLI

Download and install the AWS CLI for your operating system:

- [Install AWS CLI v2](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)

Verify the installation:

```bash
aws --version
# Expected: aws-cli/2.x.x
```

---

## 5. Configure the AWS CLI

Run the following and enter your IAM access key, secret key, default region, and output format:

```bash
aws configure
```

```
AWS Access Key ID [None]: YOUR_ACCESS_KEY
AWS Secret Access Key [None]: YOUR_SECRET_KEY
Default region name [None]: ap-southeast-1
Default output format [None]: json
```

> Use `ap-southeast-1` (Singapore) or `us-east-1` (N. Virginia) as your default region unless a project specifies otherwise.

Verify the configuration:

```bash
aws sts get-caller-identity
```

A successful response returns your account ID, user ID, and ARN.

---

## 6. Set Up Named Profiles (Recommended)

If you work with multiple AWS accounts, use named profiles to avoid credential confusion:

```bash
aws configure --profile gomal-dev
```

Then use the profile explicitly in commands:

```bash
aws s3 ls --profile gomal-dev
```

Or set it as the default for your current session:

```bash
# macOS/Linux
export AWS_PROFILE=gomal-dev

# Windows (CMD)
set AWS_PROFILE=gomal-dev

# Windows (PowerShell)
$env:AWS_PROFILE="gomal-dev"
```

---

## 7. Install Supporting Tools (as needed)

Depending on your track, you may need the following:

| Tool | Purpose | Install Guide |
|---|---|---|
| Terraform | Infrastructure as Code | [terraform.io](https://developer.hashicorp.com/terraform/install) |
| AWS CDK | Cloud Development Kit | `npm install -g aws-cdk` |
| AWS SAM CLI | Serverless local testing | [AWS SAM install](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html) |
| Node.js | Runtime for CDK and JS projects | [nodejs.org](https://nodejs.org) |
| Python 3 | Runtime for ML and backend projects | [python.org](https://python.org) |

---

## 8. Cost Awareness

All projects must operate within AWS Free Tier limits or available credits. Before deploying anything:

- Review the [AWS Free Tier](https://aws.amazon.com/free/) limits for the services you plan to use.
- Set up a **Billing Alert** in AWS to notify you if spending exceeds a threshold:
  1. Go to **Billing** > **Budgets** > **Create budget**.
  2. Set a monthly budget (e.g., $5 USD) with an email alert at 80% threshold.
- Always clean up resources after a project is complete or inactive.

---

## Troubleshooting

| Issue | Solution |
|---|---|
| `aws: command not found` | Re-run the CLI installer and restart your terminal |
| `Unable to locate credentials` | Run `aws configure` and verify your access key |
| `Access Denied` errors | Check IAM permissions for your user or role |
| Unexpected charges | Check the AWS Cost Explorer and terminate unused resources |
