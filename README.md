# Assume Role For Environment Action

## Description
This GitHub Action is designed to assume a specific AWS role based on a provided environment name. It is particularly useful for workflows that require different AWS roles for different deployment or operational environments.

## Inputs

### `environment`
**Required** The name of the environment for which to assume the role. Current supported environments are:
- `biscred-dev`
- `biscred-prod`
- `bisnow`
- `vapor`

## How it Works

1. **Set AWS Role ARN for Environment**: This step maps the provided environment input to its corresponding AWS Role ARN. It uses a Bash script to select the right ARN from a predefined list of environments and their associated roles.

2. **Assume GitHub Actions Role**: This step assumes a GitHub Actions role, which is a prerequisite for assuming the environment-specific AWS role.

3. **Assume Environment-Specific AWS Role**: Finally, this step assumes the AWS role that corresponds to the specified environment, allowing for subsequent actions to perform tasks using that role's permissions.

## Usage

To use this action in your workflow, add a step that references it and provide the required input. Here's an example:

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@v2

    - name: Assume Role For Environment
      uses: ./.github/actions/assume-role-for-environment
      with:
        environment: 'biscred-dev'
