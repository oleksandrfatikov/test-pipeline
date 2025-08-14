# Usage

## Environments

### Recommended Structure
This is the recommended structure for each business unit folder:

```
/business-unit
    /non-prod
    /prod
```

Where `business-unit` can be one of the following:

- consumers
- enterprise
- ptx
- trust-services
- wallet-xp

## Non-Production (`non-prod`)

The `non-prod` folder contains environments used for development and testing before deployment to production.

- **sbx (Sandbox)**: This environment is used for experimental features and development. It is the most volatile environment where breaking changes are acceptable.

- **stg (Staging)**: This environment is used for testing the features before they are moved to production. It is more stable than `sbx` and simulates the production environment as closely as possible.

## Production (`prod`)

The `prod` folder contains environments used for live production and pre-production.

- **ppr (Pre-Production)**: This environment is used for final testing and verification before the code is moved to the live production environment. It acts as the last checkpoint.

- **prd (Production)**: This environment is the live environment where the final, stable version of the application runs. It is accessed by end-users.

## App-of-Apps Structure

### Main app-of-apps

There is a main app-of-apps configuration:

```
./applications/app-of-apps.yaml
```

This main app-of-apps file deploys all Argo CD apps defined in all business units.


### app-of-apps per BU

Each business unit has an app-of-apps structure managed by Argo CD:

```
./applications/<business unit>/app-of-apps.yaml
```

To facilitate management, the development team should be added in the `CODEOWNERS` file, enabling them to handle their applications independently.

### Granular App-of-Apps

For more granularity, you can create an app-of-apps per environment. For example:

```
./applications/<business unit>/non-prod/app-of-apps.yaml
./applications/<business unit>/prod/app-of-apps.yaml
```

This structure allows each environment within a business unit to be managed separately, providing more control over the deployment and testing processes.
