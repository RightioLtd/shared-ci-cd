# 🔍 Determine Configuration Workflow README

## 🔍 Determine Configuration Workflow

This reusable GitHub Actions workflow, `determine-configuration.yml`, is designed to dynamically set up environment-specific variables and secrets for deployments. It allows for flexible configuration through inputs and dynamically sets the GitHub Actions environment based on the branch name.

---

### Features

- Dynamically determines environment settings based on the branch name.
- Includes environment-specific variables.
- Optionally filters secrets based on a specified prefix (`allowPrefix`).
- Outputs a JSON configuration file for deployment.
- Logs the determined environment as an output for further workflow steps.

---

### Workflow Inputs

| Input Name    | Type   | Required | Default   | Description                                                                 |
|---------------|--------|----------|-----------|-----------------------------------------------------------------------------|
| `branch`      | string | ✅        | N/A       | The branch name used to determine the environment (`main`, `master`, `development`, or `training`). |
| `allowPrefix` | string | ❌        | Empty     | A prefix to filter which secrets to include in the configuration (e.g., `STRIPE_`). |

---

### Outputs

The workflow generates a JSON file named `configuration.json` with the following structure:

```json
{
  "configuration": "Release or Debug",
  "build_flag": "prod, dev, or train",
  "app_domain": "domain name based on the branch",
  "app_environment": "production, development, or training",
  "static_variables": {
    /* Environment variables */
  },
  "static_secrets": {
    /* Filtered secrets based on allowPrefix */
  }
}
```

Additionally, it sets the following GitHub Actions outputs:

- `environment`: The determined environment (`production`, `development`, or `training`).

---

### How to Use

1. **Ensure the Workflow is Available**:
   - Ensure `determine-configuration.yml` is present in your `.github/workflows/` directory.

2. **Reference the Workflow**:
   Add the following to your deployment workflow:

    ```yaml
    name: 🚀 Deploy API to IIS

    on:
      push:
        branches:
          - main
          - master
          - development
          - training

    jobs:
      deploy:
        uses: ./.github/workflows/determine-configuration.yml
        with:
          branch: ${{ github.ref_name }}
          allowPrefix: "STRIPE_"
    ```

3. **Customise Inputs**:
   - `branch`: Set dynamically based on the branch being pushed.
   - `allowPrefix`: Specify a prefix to include only certain secrets (e.g., `STRIPE_`).

---

### Debugging and Validation

#### Generated JSON File

The workflow outputs a `configuration.json` file as an artefact. Download this from the Actions run logs to inspect the configuration.

#### Debugging Secrets

The workflow logs the keys of filtered secrets (values are not exposed). This can help verify that the filtering logic is working as intended.

---

### Common Use Cases

1. **Deploying to Multiple IIS Environments**:
   - Dynamically determine environment-specific settings based on the branch.
   - Filter secrets securely using the `allowPrefix` input.

2. **Debugging Configurations**:
   - Download and inspect the `configuration.json` file for debugging.

3. **Secure Secrets Management**:
   - Use the `allowPrefix` input to restrict included secrets to only those necessary for the deployment.

---

### Notes

- Ensure all necessary variables and secrets are configured in your repository or organisation settings.
- Test the workflow in a non-production environment before using it in production.

---

By using this reusable workflow, you can standardise and secure the configuration process across multiple deployment environments, while maintaining flexibility and clarity.
