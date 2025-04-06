# CDK Prepare Environment Action

A GitHub composite action that sets up a Node.js environment with AWS CDK, configures AWS credentials, and prepares CDK stacks for deployment with optimized caching and minimal dependencies.

## Features

- 🚀 Automated Node.js setup with optimized npm caching
- 🔐 Configures AWS credentials using role assumption
- 🔄 Enhanced CDK synthesis caching for faster builds
- 📊 Generates detailed stack summary in GitHub Actions step summary
- 📦 Creates optimized deployment package with minimal dependencies
- ⚡ Hoisted dependency installation for better performance
- 🧹 Automatic cleanup of unnecessary files in node_modules

## Usage

```yml
steps:
    - name: CDK Prepare Environment
      uses: banboniera/cdk-prepare@v2
      with:
        aws-region: 'eu-central-1'
        role-to-assume: 'arn:aws:iam::123456789012:role/github-actions-role'
        synth-command: 'npx cdk synth'  # optional
        artifact-name: 'cdk-deployment-package'  # optional
        artifact-path: 'deployment'  # optional
        node-version: '22'  # optional
```

## Inputs

| Input | Description | Required | Default |
| ----- | ----------- | -------- | ------- |
| `aws-region` | Target AWS region for deployment | true | |
| `role-to-assume` | AWS IAM role ARN to assume | true | |
| `synth-command` | CDK synthesis command | false | `npx cdk synth` |
| `artifact-name` | Name for the deployment artifact | false | `cdk-deployment-package` |
| `artifact-path` | Path to store deployment files | false | `deployment` |
| `node-version` | Node.js version to use | false | `22` |

## Artifacts

The action creates a deployment package artifact containing:

- Synthesized CDK stacks from `cdk.out`
- Minimal `package.json` with only required AWS CDK dependencies
- Optimized `node_modules` directory with:
  - Hoisted dependency installation
  - Removed test files, documentation, examples, and source maps
  - Removed unnecessary metadata files
- Stack analysis summary in GitHub Actions step summary

The artifact is retained for 1 day by default and is compressed at the highest level for optimal storage.
