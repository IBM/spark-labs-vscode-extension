# VS Code Extension for Spark Labs

Spark lab is a Spark-based development environment that enables you to interactively program, debug, submit, and test Spark applications on a live Spark cluster running on the Analytics Engine service.

It is available as a VS Code extension and you can install it in your local system to access Spark IDE using Visual Studio Code. It reduces the time for development and increases usability.

[Remote - SSH Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) is required for this extension to work.

## Features
What you can do in Visual Studio Code with this extension:

- Connect to spark labs console
- Create & Delete Spark labs from the extension
- Securely connect to your spark labs console's runtimes via SSH over secure WebSockets
- Develop & Debug the files inside your Spark Labs Git project remotely

## Installation

### Marketplace

You can use VS Code Marketplace to download and install this extension directly to your VS Code.

### From extension package
1. Ask your administrator to enable VS Code support for your cluster
2. Download the Spark Labs extension and then install the downloaded `.vsix` file in VS Code:

    `Cmd/Ctrl + Shift + P -> Extensions: Install from VSIX`

3. Optional, but recommended: Install the [Remote SSH extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) in VS Code.

   If you're not using the Remote SSH extension, you'll need an SSH client on your machine.

### Set up SSH on your machine

**Generating an SSH key pair on Mac and Linux**

**Important**: Before generating a new key pair, check the ~/.ssh directory for any existing key pairs,

To generate an SSH key pair on MacOS and Linux:

1. Open the Terminal
1. Execute this command:
    `ssh-keygen -t rsa -N ""`

When you generate a key pair, specify the location of the private key in the `spark-labs.privateKeyPath` and public key in the `spark-labs.publicKeyPath` settings of the extension.

**Generating an SSH key pair on Windows**

**Important**: Check whether your home directory contains the `.ssh` directory or run `dir "%USERPROFILE%/.ssh"` to check if any keys exist.

To generate an SSH key pair on Windows:

On Windows 10 or newer with the OpenSSH Client feature enabled:

1. Open a new cmd command prompt and use the `ssh-keygen utility.
2. Execute this command:
`ssh-keygen -t rsa -N ""`

If you are using an older Windows version:

- Install a third party tool, such as Putty, to generate a SSH key.
- If your're using Putty, use the `puttygen` utility to generate an SSH key pair.
   Note: PuttyGen does not generate OpenSSH keys by default. To export an OpenSSH key, convert the key: select Conversions -> Export OpenSSH key.


**Optional: Using a separate SSH key for Spark Labs**

To use a seperate SSH key for Spark Labs, add a new entry to your SSH configuration under `~/.ssh/config`: 

```
Host cpdenv
    HostName localhost
    Port 5681 # Same port as spark-labs.localPort
    IdentityFile ~/.ssh/id_cpd_rsa # Path to your private key
```

Then enter the host `cpdenv` under `spark-labs.localHost`. 

## Extension Settings

This extension contributes the following settings:

* `spark-labs.host`: Hostname of the spark labs console. You can find it in the address bar of your browser when you log in to Cloud Pak For Data or IBM Cloud. For example: `cpd.xxx.xxx.xxx.com`.
* `spark-labs.userName`: Username that you use to log in to Cloud Pak For Data or IBM Cloud or IBM Cloud.
* `spark-labs.privateKeyPath`: Path to the private key file for SSH connection.
* `spark-labs.publicKeyPath`: Path to the public key file for SSH connection.
* `spark-labs.localPort`: The port to listen on locally
* `spark-labs.localHost`: The SSH host to which Remote SSH will connect to. Can be any host specified in the SSH client config file. The HostName configured in your SSH client config should always point to localhost and the port specified in localPort. This allows you to use your own SSH settings, e.g. a specific private key.
* `spark-labs.verifySSL`: (Optional) Whether to verify the certificate of the SSL connection or not. Default: `true`.
* `spark-labs.autoOpenRuntime`: Automatically open the runtime once it has been loaded, without the need for extra confirmation.
* `spark-labs.logLevel`: The log level of the extension.
* `spark-labs.storeApiKeyInKeychain`: Whether to store the encrypted Cloud Pak For Data or IBM Cloud API key in your operating system keychain. Default: true. If you disable this option, the API key will be stored in memory only for the duration the current session; when you restart your VS Code instance, you will have to re-enter your API key.
* `spark-labs.autoUpdateHostkey`: Automatically update the host key in the `known_hosts` file by fetching it via a secure TLS connection. Before modifying the known_hosts file, a backup is created under `~/.ssh/.known_hosts.cpd-backup`. This setting should always be enabled, especially when operating with multiple clusters.