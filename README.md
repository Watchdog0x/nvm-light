# Node Version Manager Light (NVML) 
![Static Badge](https://img.shields.io/badge/%20Version-1.1.0-rgb(93%2C%2063%2C%20211)?style=for-the-badge&labelColor=%23161B22)

This script is tailored for sysadmins and server environments where managing Node.js versions at the system level is crucial. Unlike user-based NVM installations that are common for development environments, system-based NVM ensures consistent Node.js versions across all users and applications on the server.

## Features:

- **Install Node.js Versions**: Download and install specific Node.js versions from the official Node.js release repository.

- **List Installed Versions**: Display a list of Node.js versions installed on your system, indicating the currently active version.

- **Set Active Version**: Set the active Node.js version, creating symbolic links for node, npx, and npm.

- **Remove Installed Version**: Safely remove an installed Node.js version, excluding the currently active version.

- **Patch Updates**: Check for and install updates to existing Node.js versions, with an option to clean up old versions.

## Installation

#### 1) **Remove the system Node.js and let NVML manage it:**
```bash
sudo apt purge --auto-remove nodejs
```

#### 2) **Navigate to your preferred directory:**
```bash
# in my case I will use opt
cd /opt
```

#### 3) **Clone the repository to your server:**
```bash
sudo git clone https://github.com/Watchdog0x/nvm-light.git && cd nvm-light
```

#### 4) **Create a symbolic link to the completion script:**
```bash
sudo ln -rfs nvml_completion /etc/bash_completion.d/
```
> [!NOTE] 
> The nvml_completion script provides command-line completion for nvml commands, helping you discover available versions and options. After linking, you can use tab completion to explore the available Node.js versions and subcommands.

#### 5) **Create a symbolic link to the nvml:**
```bash
sudo ln -rfs nvml /usr/local/bin/
```

#### 6) **Don't Forget to Source Your Bashrc:**
```bash
source ~/.bashrc
```

#### 7) **Don't forget to install the preferred Node.js version:**
```bash
sudo nvml -i 20.9.0 -s 20.9.0 -l
```
Output
```bash
Node.js version 20.9.0  downloaded successfully to /opt/nvm-light/nodejs
Node.js version 20.9.0  extracted successfully
Node.js version 20.9.0  has been set successfully.
Available Node.js versions installed on your system:
* Node.js 20.9.0  (Running)
```
> [!NOTE] 
> Use `-i` to install, `-s` to set the Node.js version, and `-l` to list them for checking.

>[!IMPORTANT]
>The global installation path for npm packages (npm install -g) is controlled by the system administrator. The standard prefix is set to /usr/local. Ensure that users have the necessary permissions to install global packages or consider running npm commands with elevated privileges.

## Usage:

```bash
nvml [OPTIONS]
```

- `-i, --install`: Install a specific Node.js version.
- `-l, --list`: List available Node.js versions on your system.
- `-s, --set`: Set the active Node.js version.
- `-r, --remove`: Remove an installed Node.js version.
- `-p, --patch`: Update all installed Node.js versions to the latest. Subcommand `clean` removes old versions.
- `-v, --version`: Print the version of nvml
- `-h, --help`: Display the help message.

## Set up Cron Job for Auto-Updates

#### 1) **Open the crontab editor:**
```bash
sudo crontab -e
```

#### 2) Add a cron job to automatically update Node.js versions daily At 00:00:
```bash
# Example: Run nvml patch (update) daily at midnight and log the output
**0 0 * * * /path/to/nvm-script/nvml -p >> /var/log/nvml-update.log 2>&1
```

> [!NOTE] 
> When using `sudo crontab -e` to edit the crontab for the root user, you can also add the `clean` option to enable automatic cleanup. Ensure you have the necessary permissions and use this command responsibly.


## Contributing
Contributions are welcome! Feel free to open issues, submit pull requests, or provide suggestions. Please follow the Contributing Guidelines.


## License
This project is licensed under the MIT License
