# Vampy CLI

## Description

`vampy-cli` is a command-line utility for interacting with the Vampy server. It allows you to manage products, repositories, perform scanning processes, and much more.

`vampy-cli` is easy to use in CI/CD pipelines to run scans and stop pipelines if the scan fails or the scan results do not match the specified release criteria (Security Quality Gates).


## What is Vampy?

Vampy is a free ASPM platform that allows you to get results from SAST, DAST, SCA vulnerability scanners in one window, automate vulnerability elimination and triage processes, and manage risks.

## Installation

You can install `vampy-cli` using the `curl` utility script or download a precompiled file from the [GitHub](https://github.com/hexway/Vampy-CLI) release page.

### Installation with `curl`

```bash
curl -sSL https://get.vampy.ru | sh
```

### Download compiled binaries

The [Releases](https://github.com/hexway/Vampy-CLI/releases) page on GitHub contains compiled `vampy-cli` files for various platforms.

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

- `upload`

    Uploads existing scan results.

- `scan`

    Starts the scan process for the specified repository and scanner.

- `quality-gate`

    Displays the QualityGate results for the selected product or repository.

- `bg-task`

    Checks the status of a background task and provides details.

- `products`

    Retrieves the list of products.

- `repositories`

    Retrieves the list of repositories.

- `help`, `h`

    Displays a list of available commands or help for a specific command.

## Global Options

### General Options

- `--details`

    Shows detailed output for the requested action (e.g., a table with QualityGate results)

    **Default:** `false`.

- `--help`, `-h`

    Displays help.

- `--verbose`

    Shows additional output (e.g., each step of the requested action)

    **Default:** `false`.

- `--version`, `-v`

    Outputs only the program version.


### Connection Parameters

- `--api-token`

    **This is a mandatory parameter.**

    API token for connecting to the Vampy server.

    **Default:** value from environment variable `VAMPY_API_TOKEN`.

- `--api-version`

    Vampy API version.

    **Default:** `v1`.

- `--timeout`

    Timeout in seconds.

    **Default:** 120 (2 minutes).

- `--vampy-url`

    **This is a mandatory parameter.**

    URL of the Vampy server.

    **Default:** value from environment variable `VAMPY_URL`.


## Configuration

To use `vampy-cli` you need to define two **mandatory** connection parameters:

- `--api-token-value`;
- `--vampy-url`.

You can define them in several ways:

- environment variables:

    ```bash
    export VAMPY_API_TOKEN=eyJhb*******xHWcxk
    export VAMPY_URL=https://vampy.hexway.io
    ```

- command line options:

    ```bash
    ./vampy_cli \
       --api-token eyJhb*******xHWcxk \
       --vampy-url https://vampy.hexway.io \
       products
    ```

## Example Usage

### Upload existing scan results

```bash
./vampy_cli upload \
   --repository vmp/product/vampy-engine \
   --file ~/scans_trivy_image.json \
   --scanner TRIVY_IMAGE
```

### Start a scan

```bash
./vampy_cli scan \
   --repository vmp/product/vampy-engine \
   --check-task \
   --details
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

### Getting help

If you have any questions or issues, use the `help` command:

```bash
./vampy_cli help
```
