# General README for Repository

## Workflows Repository

This repository contains reusable GitHub Actions workflows designed to standardise and streamline development and deployment processes. These workflows manage various tasks such as setting up configurations, deployments, and other automation requirements.

---

### Available Workflows

#### 🔍 Determine Configuration

This reusable workflow dynamically determines environment-specific variables and secrets for deployments. It includes enhanced flexibility, such as dynamically setting the environment for GitHub Actions and filtering secrets based on an optional prefix.

- **Key Features**:
  - Dynamically determines environment settings based on the branch name.
  - Includes environment-specific variables.
  - Optionally filters secrets based on a specified prefix (`allowPrefix`).
  - Outputs a JSON configuration file for deployment and logs the determined environment.

For detailed documentation, see the [🔍 Determine Configuration Workflow README](./.github/workflows/determine-configuration.md).

---

### Getting Started with Workflows

1. **Setup and Configuration**:
   - Ensure your repository contains all required variables and secrets under repository or organisation settings.
   - Add reusable workflows to the `.github/workflows/` directory.

2. **Reference Workflows in Your Projects**:
   - Use the `uses` key in your workflows to reference reusable workflows from this repository.
   - Customise inputs to suit your project's needs.

3. **Validate Outputs**:
   - Most workflows produce artefacts or logs for debugging. Always validate these outputs in your workflow runs.

---

### Repository Structure

```plaintext
.github/
└── workflows/
    ├── determine-configuration.yml    # Dynamically determines and outputs environment configurations.
    ├── deploy-to-iis.yml              # Deploys applications to IIS servers using pre-determined configurations.
    └── <other-workflows>.yml          # Add more workflows as needed.
```

---

### Contributing

1. **Add New Workflows**:
   - Follow the naming conventions and keep workflows modular.
   - Add a brief documentation section in this README or as a dedicated file.

2. **Testing Workflows**:
   - Test new or updated workflows in a non-production environment before merging.

3. **Documentation**:
   - Update the README with relevant details about new workflows or updates.

---

### Workflow-Specific Documentation

For detailed instructions, configurations, and examples, refer to the individual workflow READMEs:

- [🔍 Determine Configuration Workflow](./.github/workflows/determine-configuration.md)
