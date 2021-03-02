---
title: Install and use Cloud Accelerator Platform CLI
---

# Install and use Cloud Accelerator Platform CLI

This topic helps you to install, configure, and use the Hitachi Cloud Accelerator Platform Command Line Interface (Cloud Accelerator Platform CLI), which is a tool that enables you to perform various actions in Hitachi Cloud Accelerator Platform - Deploy (Deploy Accelerator), Hitachi Cloud Accelerator Platform - Test (Test Accelerator), Hitachi Cloud Accelerator Platform - Workflow (Workflow Accelerator), and the Admin Console. You can use the Cloud Accelerator Platform CLI to deploy environments, run tests, manage users, and perform many other actions.

## <a name="Content"></a>Contents
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'cliTool', viewSection: 'supported-os'})" style="text-decoration:none">Supported operating systems</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'cliTool', viewSection: 'cliprereq'})" style="text-decoration:none">Prerequisites</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'cliTool', viewSection: 'cliinstall'})" style="text-decoration:none">Installing the Cloud Accelerator Platform CLI</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'cliTool', viewSection: 'cliconfig'})" style="text-decoration:none">Configuring the Cloud Accelerator Platform CLI</a>
* <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'cliTool', viewSection: 'acc-version'})" style="text-decoration:none">Verifying supported versions of the accelerators</a>
* <a href="" ui-sref="rean-platform-docs.clidoc" target="_blank" style="text-decoration:none">Platform CLI command reference</a>

## <a id="supported-os" name="supported-os"></a>Supported operating systems

The Cloud Accelerator Platform CLI is supported on the following operating systems:

- Linux
- macOS

## <a id="cliprereq" name="cliprereq"></a>Prerequisites

Before installing the Cloud Accelerator Platform CLI, you must perform the following actions:

- Ensure that the computer on which you plan to install the Cloud Accelerator Platform CLI meets the following requirements:
  - Python and PIP 3.5 or later is installed on the computer.
  - [Cloud Accelerator Platform Artifactory](https://artifactory.reancloud.com/artifactory/webapp/#/home) is accessible from the computer.
- Create a user for accessing Cloud Accelerator Platform Artifactory and generate the API key from the Cloud Accelerator Platform Artifactory.

_**Note:** If you cannot access Cloud Accelerator Platform Artifactory or create your user, contact the [Cloud Accelerator Platform Support team](mailto:hcap.support@hitachivantara.com)._  

## <a id="cliinstall" name="cliinstall"></a>Installing the Cloud Accelerator Platform CLI

1. On the computer on which you want to install the Cloud Accelerator Platform CLI, perform one of the following actions:

   - To install the latest version of the Cloud Accelerator Platform CLI, use the following command.

      ```bash
      pip3 install reanplatform-cli --index-url https://<Artifactory_user_name>:<Artifactory password or api_key>@artifactory.reancloud.com/artifactory/api/pypi/virtual-pypi/simple
      ```

      **Example:**

      ```bash
      pip3 install reanplatform-cli --index-url https://m.connor:AVCdaxyzRam79HC3TByNw2vVd5XMKv4vpyZjhAsyhsANC78B0XXXviud@artifactory.reancloud.com/artifactory/api/pypi/virtual-pypi/simple
      ```

   - To install a specific version of the Cloud Accelerator Platform CLI, run the following command**.**

     ```bash
     pip3 install reanplatform-cli==<cli_version> --index-url https://<Artifactory_user_name>:<Artifactory password or api_key>@artifactory.reancloud.com/artifactory/api/pypi/virtual-pypi/simple
     ```

     **Example:**

     ```bash
     pip3 install reanplatform-cli==2.28.0 --index-url https://m.connor:AVCdaxyzRam79HC3TByNw2vVd5XMKv4vpyZjhAsyhsANC78B0XXXviud@artifactory.reancloud.com/artifactory/api/pypi/virtual-pypi/simple
     ```

2. _(Optional)_ To verify the version of the Cloud Accelerator Platform CLI that is installed, run the following command:

   ```bash
   pip3 list | grep reanplatform-cli
   ```

## <a id="cliconfig" name="cliconfig"></a>Configuring the Cloud Accelerator Platform CLI

After installing the Cloud Accelerator Platform CLI, you can configure access to the Cloud Accelerator Platform instance by using one of the following methods:

- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'cliTool', viewSection: 'set-env'})" style="text-decoration:none">Set environment variables</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'cliTool', viewSection: 'config-file-existing'})" style="text-decoration:none">Use an existing configuration file</a>
- <a href="" ui-sref="rean-platform-docs.accelerator({viewAccelerator: 'rean-platform-common', viewPage: 'cliTool', viewSection: 'config-file'})" style="text-decoration:none">Create a configuration file</a>

_**Note:** The precedence order for fetching configuration details is environment variables, existing configuration file, and finally the configuration file that you create._

### <a id="set-env" name="set-env"></a>Set environment variables

To configure access to a Cloud Accelerator Platform instance by setting environment variables, run the following commands:

```bash
export REAN_PLATFORM_USER_NAME="<username>"
export REAN_PLATFORM_PASSWORD="<password>"
export REAN_PLATFORM_BASE_URL="<PlatformURL>"
```

**Example**

```bash
export REAN_PLATFORM_USER_NAME="m.connor@companyname.com"
export REAN_PLATFORM_PASSWORD="Password@1234"
export REAN_PLATFORM_BASE_URL="https://rean-platform.reancloud.com"
```

**SSL certificate verification**

By default, SSL certificate verification is enabled for Cloud Accelerator Platform CLI. Based on your requirements, you can set the following optional environment variables.

- To configure the certificate path, set the **REAN_PLATFORM_SSL_CERTIFICATE_PATH** environment variable to the absolute path of the certificate, as shown in the example below.

  ```bash
  export REAN_PLATFORM_SSL_CERTIFICATE_PATH="/Users/mconner/gitRepos/companyname/cli/rootCA.pem"
  ```

- To skip verifying the SSL certificate, set the **REAN_PLATFORM_VERIFY_SSL** environment variable to **False**, as shown below.

  ```bash
  export REAN_PLATFORM_VERIFY_SSL=False
  ```

  _**Note:** The default value of the **REAN_PLATFORM_VERIFY_SSL** environment variable is **true**._

### <a id="config-file-existing" name="config-file-existing"></a>Use an existing configuration file

To configure access to a Cloud Accelerator Platform instance by using an existing configuration file, perform the following actions:

1. Ensure that your existing configuration file (YAML file) is in the following format:

   ```yaml
   <any-value-specific-to-environment>:
     base_url: <base_url>
     username: <username>
     password: <password>
   ```

   **SSL certificate verification**

   By default, SSL certificate verification is enabled for Cloud Accelerator Platform CLI. Based on your requirements, you can add the following optional parameters in the configuration file.

   - To configure the certificate path, set the **ssl_certificate_path** parameter to the absolute path of the certificate, as shown in the example below.

     ```yaml
     <any-value-specific-to-environment>:
       base_url: <base_url>
       username: <username>
       password: <password>
       ssl_certificate_path: /Users/mconner/gitRepos/companyname/cli/rootCA 
     ```

   - To skip verifying the SSL certificate, set the **verify_ssl_certificate** parameter to **false**, as shown below.

     ```yaml
     <any-value-specific-to-environment>:
       base_url: <base_url>
       username: <username>
       password: <password>
       verify_ssl_certificate: false
     ```

     _**Note:** To later enable SSL certificate verification, you can set the **verify_ssl_certificate** parameter to **true**._  

2. To export the configuration file path through an environment variable, run the following command:

   ```bash
   export REAN_PLATFORM_CONFIG_FILE_PATH=<Path_to_configuration_yaml_file>
   ```

### <a id="config-file" name="config-file"></a>Create a configuration file

1. Run one of the following commands:

   ```bash
   rean-platform configure --platform_base_url <platform_url> --username <platform_username>
   ```

   ```bash
   rean-platform configure -url <platform_url> -u <platform_username>
   ```

   **Example**

   ```bash
   rean-platform configure --platform_base_url https://rean-platform.reancloud.com --username m.connor@companyname.com
   ```

   **Store credentials in an encrypted format**

   To store the credentials in an encrypted format, use the **--encrypt_credentials** or **-e** parameter in the command, as shown below.

   ```bash
   rean-platform configure --platform_base_url <platform_url> --username <platform_username> --encrypt_credentials
   ```

   ```bash
   rean-platform configure -url <platform_url> -u <platform_username> -e
   ```

   **Verify SSL certificate**

   By default, SSL certificate verification is enabled for Cloud Accelerator Platform CLI. Based on your requirements, you can use the following optional parameters in the command.

   - To configure the certificate path when SSL certificate verification is enabled, use the **--ssl_certificate_path** parameter and specify the absolute path of the certificate, as shown below.

     ```bash
     rean-platform configure --platform_base_url <platform_url> --username <platform_username> --ssl_certificate_path <certificate_absolute_path> 
     ```

   - To skip verifying the SSL certificate, use the **--ignore_ssl_verification** or **-i** parameter, as shown below.

     ```bash
     rean-platform configure --platform_base_url <platform_url> --username <platform_username> --ignore_ssl_verification
     ```

     ```bash
     rean-platform configure -url <platform_url> -u <platform_username> -i
     ```

2. Enter the password for the user name that you have specified.

## <a id="acc-version" name="acc-version"></a>Verifying supported versions of the accelerators

Each release of Cloud Accelerator Platform CLI supports a specific version of Admin Console, Deploy Accelerator, Test  Accelerator, and Workflow Accelerator.<br>

To find out which accelerator versions are supported by the Cloud Accelerator Platform CLI that you have installed, run the following commands:

- Admin Console

  ```bash
  rean-auth --version
  ```

- Deploy Accelerator

  ```bash
  rean-deploy --version
  ```

- Test Accelerator

  ```bash
  rean-test --version
  ```

- Workflow Accelerator

  ```bash
  rean-workflow --version
  ```

