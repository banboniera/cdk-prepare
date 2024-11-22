# Setup CDK Environment Action

A GitHub composite action that sets up a Node.js environment with AWS CDK and configures AWS credentials.

## Features

- 🚀 Automated Node.js setup with npm caching
- 📦 Installs project dependencies and AWS CDK
- 🔐 Configures AWS credentials
- 📁 Supports custom working directory
- ✅ Validates installations and configurations

## Usage

```yaml
steps:
    - uses: actions/checkout@v4
    - name: Setup CDK Environment
      uses: banboniera/setup-cdk@v1
      with:
        aws-region: 'eu-central-1'
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

For a specific CDK version:

```yaml
steps:
    - uses: actions/checkout@v4
    - name: Setup CDK Environment
      uses: banboniera/setup-cdk@v1
      with:
        aws-region: 'eu-central-1'
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        cdk-version: '2.170.0'  # Optional - will use latest version if not specified
```

## Inputs

| Input | Description | Required | Default |
| ----- | ----------- | -------- | ------- |
| `aws-region` | AWS Region | true | |
| `aws-access-key-id` | AWS Access Key ID | true | |
| `aws-secret-access-key` | AWS Secret Access Key | true | |
| `node-version` | Node.js version to use | false | `20` |
| `cdk-version` | AWS CDK version to install | false | `latest` |
| `working-directory` | Working directory for npm commands | false | `.` |
| `skip-dependencies` | Skip installing dependencies | false | `true` |
