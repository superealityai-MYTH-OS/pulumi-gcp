[![Actions Status](https://github.com/pulumi/pulumi-gcp/workflows/master/badge.svg)](https://github.com/pulumi/pulumi-gcp/actions)
[![Slack](http://www.pulumi.com/images/docs/badges/slack.svg)](https://slack.pulumi.com)
[![NPM version](https://badge.fury.io/js/%40pulumi%2Fgcp.svg)](https://npmjs.com/package/@pulumi/gcp)
[![NuGet version](https://badge.fury.io/nu/pulumi.gcp.svg)](https://badge.fury.io/nu/pulumi.gcp)
[![Python version](https://badge.fury.io/py/pulumi-gcp.svg)](https://pypi.org/project/pulumi-gcp)
[![PkgGoDev](https://pkg.go.dev/badge/github.com/pulumi/pulumi-gcp/sdk/v6/go)](https://pkg.go.dev/github.com/pulumi/pulumi-gcp/sdk/v6/go)
[![License](https://img.shields.io/npm/l/%40pulumi%2Fgcp.svg?color=limegreen)](https://github.com/pulumi/pulumi-gcp/blob/master/LICENSE)

# Google Cloud Platform Resource Provider

The Google Cloud Platform (GCP) resource provider for Pulumi lets you use GCP resources in your cloud programs. To use
this package, [install the Pulumi CLI](https://www.pulumi.com/docs/get-started/install/). For a streamlined Pulumi walkthrough, including language runtime installation and GCP configuration, select "Get Started" below.

<div>
    <a href="https://www.pulumi.com/docs/get-started/gcp" title="Get Started">
       <img src="https://www.pulumi.com/images/get-started.svg?" width="120">
    </a>
</div>

## Table of Contents

- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
- [Installing](#installing)
- [Configuration](#configuration)
- [Development Setup](#development-setup)
- [Troubleshooting](#troubleshooting)
- [Reference](#reference)

## Prerequisites

Before using this provider, you'll need:

1. **Pulumi CLI**: [Install Pulumi](https://www.pulumi.com/docs/get-started/install/)
2. **Google Cloud Account**: [Sign up for GCP](https://cloud.google.com/)
3. **Google Cloud CLI** (recommended): [Install gcloud](https://cloud.google.com/sdk/docs/install)
4. **Language Runtime**: Choose one based on your preference:
   - Node.js 14+ for JavaScript/TypeScript
   - Python 3.7+
   - Go 1.18+
   - .NET 6.0+
   - Java 11+

## Quick Start

1. **Install Pulumi CLI**:
   ```bash
   # macOS
   brew install pulumi/tap/pulumi
   
   # Linux
   curl -fsSL https://get.pulumi.com | sh
   
   # Windows
   choco install pulumi
   ```

2. **Authenticate with Pulumi**:
   ```bash
   # Login to Pulumi Cloud (manages state and secrets)
   pulumi login
   
   # Or use a personal access token
   pulumi login --cloud-url https://api.pulumi.com
   export PULUMI_ACCESS_TOKEN=pul-xxxxxxxxxxxxx
   ```

3. **Configure GCP Authentication**:
   ```bash
   # Authenticate with Google Cloud
   gcloud auth application-default login
   
   # Set your default project
   gcloud config set project YOUR_PROJECT_ID
   ```

4. **Create a new Pulumi project**:
   ```bash
   mkdir my-gcp-project && cd my-gcp-project
   pulumi new gcp-typescript  # or gcp-python, gcp-go, gcp-csharp
   ```

5. **Deploy your infrastructure**:
   ```bash
   pulumi up
   ```

## Installing

This package is available in many languages in the standard packaging formats.

### Node.js (JavaScript/TypeScript)

To use from JavaScript or TypeScript in Node.js, install using either `npm`:

    $ npm install @pulumi/gcp

or `yarn`:

    $ yarn add @pulumi/gcp

### Python

To use from Python, install using `pip`:

    $ pip install pulumi_gcp

### Go

To use from Go, use `go get` to grab the latest version of the library

    $ go get github.com/pulumi/pulumi-gcp/sdk/v6

### .NET 

To use from .NET, install using `dotnet add package`:

   $ dotnet add package Pulumi.Gcp

### Java

To use from Java, add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.pulumi</groupId>
    <artifactId>gcp</artifactId>
    <version>VERSION</version>
</dependency>
```

## Configuration

### Pulumi Configuration

After installing Pulumi, authenticate using one of these methods:

1. **Interactive Login** (recommended for local development):
   ```bash
   pulumi login
   ```

2. **Access Token**:
   ```bash
   export PULUMI_ACCESS_TOKEN=pul-xxxxxxxxxxxxx
   pulumi login
   ```

3. **Self-hosted Backend**:
   ```bash
   pulumi login s3://my-pulumi-state-bucket
   ```

### GCP Authentication

Configure your GCP credentials using one of these methods:

1. **Google Cloud CLI** (recommended for local development):
   ```bash
   gcloud auth application-default login
   gcloud config set project YOUR_PROJECT_ID
   ```

2. **Service Account** (recommended for CI/CD):
   ```bash
   export GOOGLE_APPLICATION_CREDENTIALS=/path/to/service-account-key.json
   ```

3. **Environment Variables**:
   ```bash
   export GOOGLE_PROJECT=your-project-id
   export GOOGLE_REGION=us-central1
   export GOOGLE_ZONE=us-central1-a
   ```

For detailed authentication options, see the [Installation & Configuration Guide](https://www.pulumi.com/registry/packages/gcp/installation-configuration/).

### Setting Project Configuration

Set required configuration values for your Pulumi stack:

```bash
pulumi config set gcp:project YOUR_PROJECT_ID
pulumi config set gcp:region us-central1
pulumi config set gcp:zone us-central1-a
```

## Development Setup

If you want to contribute to this provider or build it from source:

### Prerequisites for Development

- Go 1.21 or later
- Node.js 18 or later
- Python 3.9 or later
- .NET 6.0 or later
- Java 11 or later (with Gradle)
- Pulumi CLI
- Make

### Building from Source

1. **Clone the repository**:
   ```bash
   git clone https://github.com/pulumi/pulumi-gcp.git
   cd pulumi-gcp
   ```

2. **Initialize the upstream submodule**:
   ```bash
   make upstream
   ```

3. **Build the provider and SDKs**:
   ```bash
   make build
   ```

This will:
- Build the provider binary
- Generate the provider schema
- Generate and build SDKs for all supported languages

### Common Development Tasks

- **Build provider only**: `make provider`
- **Generate schema**: `make schema`
- **Build all SDKs**: `make build_sdks`
- **Build specific SDK**: `make build_nodejs`, `make build_python`, etc.
- **Run provider tests**: `make test_provider`
- **Lint provider code**: `make lint_provider`

For more details, see [CONTRIBUTING.md](./CONTRIBUTING.md).

## Troubleshooting

### Authentication Issues

**Problem**: `Error: google: could not find default credentials`

**Solution**: Ensure you've authenticated with GCP:
```bash
gcloud auth application-default login
```

**Problem**: `Error: Your application has authenticated using end user credentials`

**Solution**: For production use, switch to a service account:
```bash
export GOOGLE_APPLICATION_CREDENTIALS=/path/to/service-account-key.json
```

### Project Configuration Issues

**Problem**: `Error: project is required`

**Solution**: Set your project in Pulumi configuration:
```bash
pulumi config set gcp:project YOUR_PROJECT_ID
```

Or set it via environment variable:
```bash
export GOOGLE_PROJECT=YOUR_PROJECT_ID
```

### Quota and API Issues

**Problem**: `Error: Google Cloud APIs are not enabled`

**Solution**: Enable required APIs for your project:
```bash
gcloud services enable compute.googleapis.com
gcloud services enable storage.googleapis.com
# Enable other APIs as needed
```

**Problem**: `Error: Quota exceeded`

**Solution**: Check your quota limits in the [GCP Console](https://console.cloud.google.com/iam-admin/quotas) and request increases if needed.

### Common Pulumi Issues

**Problem**: `error: could not create provider: unknown provider type`

**Solution**: The GCP provider plugin may not be installed. It will be automatically installed on first use, or manually install:
```bash
pulumi plugin install resource gcp v7.0.0
```

**Problem**: State file conflicts

**Solution**: If multiple people are working on the same stack:
- Use Pulumi Cloud (recommended)
- Or use a shared backend (AWS S3, Azure Blob, GCS)

For more help:
- [Pulumi GCP Documentation](https://www.pulumi.com/registry/packages/gcp/)
- [Pulumi Community Slack](https://slack.pulumi.com)
- [GCP Support](https://cloud.google.com/support)

## Reference

For further information, visit [GCP in the Pulumi Registry](https://www.pulumi.com/registry/packages/gcp/)
or for detailed API reference documentation, visit [GCP API Docs in the Pulumi Registry](https://www.pulumi.com/registry/packages/gcp/api-docs/).
