# CDK Prepare

A GitHub composite action that sets up a Node.js environment with AWS CDK, configures AWS credentials, and prepares CDK stacks for deployment.

## Features

- 🚀 Automated Node.js setup with npm caching
- 🔐 Configures AWS credentials using role assumption
- 📊 Generates detailed stack summary in GitHub Actions step summary
- 📦 Creates deployment package with synthesized CDK stacks

## Usage

```yml
steps:
    - name: CDK Prepare Environment
      uses: banboniera/cdk-prepare@v2
      with:
        aws-region: 'eu-central-1'
        role-to-assume: 'arn:aws:iam::123456789012:role/github-actions-role'
        synth-command: 'npm run synth'  # optional
        artifact-name: 'cdk-deployment-package'  # optional
        node-version: '22'  # optional
```

## Inputs

| Input | Description | Required | Default |
| ----- | ----------- | -------- | ------- |
| `aws-region` | Target AWS region for deployment | true | |
| `role-to-assume` | AWS IAM role ARN to assume | true | |
| `synth-command` | CDK synthesis command | false | `npm run synth` |
| `artifact-name` | Name for the deployment artifact | false | `cdk-deployment-package` |
| `node-version` | Node.js version to use | false | `22` |

## Artifacts

The action creates a deployment package artifact containing:

- Synthesized CDK stacks from `cdk.out`
- Stack analysis summary in GitHub Actions step summary

The artifact is retained for 1 day by default and is compressed at the highest level for optimal storage.
