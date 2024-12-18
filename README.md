
## Description

`vampy-cli` is a command-line utility for interacting with the Vampy server.  
It allows you to manage products, repositories, perform scanning processes, and much more.

`vampy-cli` is easy to use in CI/CD pipelines to run scans and stop piplines if the scan fails or the scan results do not match the specified release criteria (Security Quality Gates)


## What is Vampy?

Vampy is a free ASPM platform that allows you to get results from SAST, DAST, SCA vulnerability scanners in one window, automate vulnerability elimination and triage processes, and manage risks.

## Installation

You can install `vampy-cli` using the `curl` utility script or download a precompiled file from the [GitHub](https://github.com/hexway/Vampy-CLI) release page.

### Installation with `curl`

```
$ curl -sSL https://get.vampy.ru | sh
```

### Download compiled binaries

The [Releases](https://github.com/hexway/Vampy-CLI/releases) page on GitHub contains compiled `vampy-cli` files for various platforms

### Use Docker image

```bash
export VAMPY_CLI_VERSION=0.1.0
docker run \
  registry.hexway.io/hexway/vampy-cli:${VAMPY_CLI_VERSION} \
  help
```

## Usage

```bash
vampy-cli [global options] command [command options]
```

## Available Commands

- **`upload`**  
  Uploads existing scan results.

- **`scan`**  
  Starts the scan process for the specified repository and scanner.

- **`quality-gate`**  
  Displays the QualityGate results for the selected product or repository.

- **`bg-task`**  
  Checks the status of a background task and provides details.

- **`products`**  
  Retrieves the list of products.

- **`repositories`**  
  Retrieves the list of repositories.

- **`help, h`**  
  Displays a list of available commands or help for a specific command.

---

## Global Options

### General Options

| Option          | Description                                                                              | Default Value |
| --------------- | ---------------------------------------------------------------------------------------- | ------------- |
| `--help, -h`    | Displays help.                                                                           |               |
| `--details`     | Shows detailed output for the requested action (e.g., a table with QualityGate results). | `false`       |
| `--verbose`     | Shows additional output (e.g., each step of the requested action).                       | `false`       |
| `--version, -v` | Outputs only the program version.                                                        | `false`       |

### Connection Parameters

| Option                | Description                                                                        | Default Value                 |
| --------------------- | ---------------------------------------------------------------------------------- | ----------------------------- |
| `--api-token value`   | API token for connecting to the Vampy server (or value from environment variable). | `value from $VAMPY_API_TOKEN` |
| `--api-version value` | Vampy API version.                                                                 | `v1`                          |
| `--timeout value`     | Timeout in seconds.                                                                | `120`                         |
| `--vampy-url value`   | URL of the Vampy server (or value from environment variable).                      | `value from $VAMPY_URL`       |


## Configuration

To use `vampy-cli` you need to define two **mandatory** connection parameters:

| Option              | Description                                                                        | Default Value                 |
| ------------------- | ---------------------------------------------------------------------------------- | ----------------------------- |
| `--api-token value` | API token for connecting to the Vampy server (or value from environment variable). | `value from $VAMPY_API_TOKEN` |
| `--vampy-url value` | URL of the Vampy server (or value from environment variable).                      | `value from $VAMPY_URL`       |

You can define them in several ways:

### Environment variables

```bash
export VAMPY_API_TOKEN=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InJlc3QtYXBpLXNlYy1lbmdpbmVlciIsImlhdCI6MTcyNTQzMjc5MS4wNjI5NX0.YMCIToiWf0wJwGG8O37-i7I1p47TCFQZyM2ZzxHWcxk
export VAMPY_URL=https://vampy.hexway.io

# get repositories list
./vampy_cli repositories
```

### Command line options

```bash
# get repositories list
./vampy_cli --vampy-url https://vampy.hexway.io  --api-token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InZtcC1jbGkiLCJpYXQiOjE3MzM5MzI2MDYuNjk1Mjk4fQ.TNWsDdhpct6PhZ0jTBZ7QTQyFuMzLN2oBr99e3uhRkA products
```

## Example Usage

### Upload existing scan results
```bash
./vampy_cli upload --repository vmp/product/vampy-engine --file ~/scans_trivy_image.json --scanner TRIVY_IMAGE
```

### Start a scan
```bash
./vampy_cli scan --repository vmp/product/vampy-engine --check-task --details
```

### Display QualityGate results
```bash
vampy-cli quality-gate --verbose
```

### Check background task status
```bash
./vampy_cli bg-task --task-id <task-id> --details
```

### Retrieve the list of products
```bash
./vampy_cli products
```

### Retrieve the list of repositories
```bash
./vampy_cli repositories
```

If you have any questions or issues, use the help command:
```bash
./vampy_cli help
```
