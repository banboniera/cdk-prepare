# CDK Prepare Environment Action

A GitHub composite action that sets up a Node.js environment with AWS CDK, configures AWS credentials, and prepares CDK stacks for deployment.

## Features

- 🚀 Automated Node.js setup with npm caching
- 📦 Installs project dependencies
- 🔐 Configures AWS credentials using role assumption
- 🔍 Analyzes CDK stacks and their dependencies
- 📦 Creates optimized deployment package
- 📤 Uploads deployment package as artifact

## Usage

```yaml
steps:
    - uses: actions/checkout@v4
    - name: CDK Prepare Environment
      uses: banboniera/cdk-prepare@v2
      with:
        aws-region: 'eu-central-1'
        role-to-assume: 'arn:aws:iam::123456789012:role/github-actions-role'
```

## Inputs

| Input | Description | Required | Default |
| ----- | ----------- | -------- | ------- |
| `aws-region` | AWS Region | true | |
| `role-to-assume` | ARN of the IAM role to assume | true | |
| `synth-command` | Command to synthesize CDK stacks | false | `npm run synth` |
| `node-version` | Node.js version to use | false | `22` |

## Outputs

| Output | Description |
| ------ | ----------- |
| `stacks` | JSON array of synthesized stacks |
| `dependencies` | JSON object of stack dependencies |

## Artifacts

The action creates a deployment package artifact named `cdk-deployment-package` containing:

- Synthesized CDK stacks
- Minimal package.json with required dependencies
- Optimized node_modules directory

The artifact is retained for 1 day by default.
