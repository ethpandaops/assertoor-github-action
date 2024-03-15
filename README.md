# Assertoor Github Action

`assertoor-github-action` is a GitHub Action designed to interface with the Assertoor API for Ethereum Testnet testing. Assertoor is specialized in assessing the overall network stability and executing specific beacon chain actions, such as deposits and exits. This capability makes it an essential tool for developers looking to ensure the reliability and robustness of their Ethereum-based applications before proceeding to the main network.

This GitHub Action is particularly useful when combined with [Kurtosis](https://kurtosis.tech/), a platform that streamlines the setup and management of multi-client Ethereum networks. However, its flexibility allows for deployment in various other testing scenarios that utilize Assertoor to conduct tests.

## Features

- **Polling Assertoor API:** Automatically polls the Assertoor API to monitor the execution status of your Ethereum Testnet tests.
- **Execution Status Checks:** The action concludes successfully once all tests have passed, or it fails immediately if any test fails, facilitating a rapid feedback loop.
- **Optional Log Streaming:** For those seeking deeper insights into the test execution process, the action offers the capability to stream Assertoor logs. It's worth noting that this feature requires integration with Kurtosis and specifying the Kurtosis enclave name.

## Prerequisites

To utilize this GitHub Action, you'll need an operational instance of Assertoor, accessible via a URL. Instructions for setting up Assertoor can be found at [ethpandaops/assertoor](https://github.com/ethpandaops/assertoor).

## Usage

This action necessitates the provision of the Assertoor API URL as input. It then continuously polls this API to verify the execution status of all tests.

### Basic Setup

Incorporate the `assertoor-github-action` into your GitHub Actions workflow with the following setup:

```yaml
jobs:
  assertoor-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      # Spin up Kurtosis enclave with ethereum-package
      # ...

      - name: Assertoor Status Check
        uses: ethpandaops/assertoor-github-action@v1
        with:
          assertoor_api_url: "http://assertoor-url"
```

### With Kurtosis and Log Streaming

For those leveraging Kurtosis for Ethereum Testnet management and wishing to include log streaming, here's a sample configuration:

```yaml
jobs:
  kurtosis-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      # Spin up Kurtosis enclave with ethereum-package
      # ...

      - name: Assertoor Status Check
        uses: ethpandaops/assertoor-github-action@v1
        with:
          # Specify the Assertoor API URL
          assertoor_api_url: 'http://assertoor-url'
          # (Optional) Specify the Kurtosis enclave name for log streaming
          kurtosis_enclave_name: 'assertoor-test'
```

## Inputs

- `assertoor_api_url`: **Required**. The URL to your Assertoor API endpoint.
- `kurtosis_enclave_name`: Optional. The name of your Kurtosis enclave, necessary for log streaming.

## Outputs

This action defines the following outputs for use in subsequent steps of your workflow:

- `result`: Final Test status (success / failure).
- `test_overview`: Assertoor Test overview.
- `failed_test_details`: Failed Assertoor Test details.

## Contributing

Contributions to `assertoor-github-action` are warmly welcomed. Please refer to the project's issues and pull request sections for guidelines on contributing.

## License

Refer to the repository's license file for information on the licensing of this GitHub Action and the associated software.
