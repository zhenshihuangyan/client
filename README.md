# qubic.li - Client
This is the main client component from qubic.li. It connects to the backend api and receives tasks to perform.

## Security Warning
The client is able to download runners, which then performs the AI Training tasks. This can potentially be used in a bad manner. Run the client with the least priviliges which are possble. e.g. on windows NOT as Admininstrator; on linux NOT as root.

Find more information about the "principle of least privilege" on wikipedia: https://en.wikipedia.org/wiki/Principle_of_least_privilege

## What's needed
To run the qubic.li Client you need .Net Runtime in Version 6 on all platforms. You can get it from: https://dotnet.microsoft.com/en-us/download/dotnet/6.0.

The runner needs also the VC Redistributable which can be obtained from: https://learn.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170

## Service Installation
To install the qubic.li Service you can use our quick installation guide. Please consider to check the content of the service installation script.
All commands should either be executed by root or you need to prepend the `sudo` command.

The installerscript places all qubic.li stuff in `/q`.

### Ubuntu 22.04
If the below installation of dotnet6 is not working on your ubuntu please consider to install it directly from microsoft: https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-2204

```bash
# Update packages
apt update
# Install needed packages
apt install dotnet6 unzip -y
# download service installation script
wget https://qubic.li/cloud-init/qli-Service-install.sh
# set the script as executable
chmod u+x qli-Service-install.sh
# install qubic.li client as systemd service
# Syntax: qli-Service-install.sh <threads> <accessToken> [alias]
./qli-Service-install.sh 2 eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJJZCI6IjVlNjJhZjhjLWU5ZTgtNDBiMS04ZmMyLTM5Mzg0Mzk5OTcwNyIsIk1pbmluZyI6IiIsIm5iZiI6MTY3MjE3MTIwMywiZXhwIjoxNzAzNzA3MjAzLCJpYXQiOjE2NzIxNzEyMDMsImlzcyI6Imh0dHBzOi8vcXViaWMubGkvIiwiYXVkIjoiaHR0cHM6Ly9xdWJpYy5saS8ifQ.DJkHv_2K0eNiAkjKia8bxag5I4ixOtjk36AGE6zwzxiEFO_w8ovsoLY4ARONUwnak_N-5-W69PJbbKCphyICpQ
```


### Debian 11
```bash
# download and install microsoft sourcese for dotnet installation
wget https://packages.microsoft.com/config/debian/11/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
# Update Sources and install needed packages
apt update && apt install aspnetcore-runtime-6.0 unzip -y
# download service installation script
wget https://qubic.li/cloud-init/qli-Service-install.sh
# set the script as executable
chmod u+x qli-Service-install.sh
# install qubic.li client as systemd service
# Syntax: qli-Service-install.sh <threads> <accessToken> [alias]
./qli-Service-install.sh 2 eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJJZCI6IjVlNjJhZjhjLWU5ZTgtNDBiMS04ZmMyLTM5Mzg0Mzk5OTcwNyIsIk1pbmluZyI6IiIsIm5iZiI6MTY3MjE3MTIwMywiZXhwIjoxNzAzNzA3MjAzLCJpYXQiOjE2NzIxNzEyMDMsImlzcyI6Imh0dHBzOi8vcXViaWMubGkvIiwiYXVkIjoiaHR0cHM6Ly9xdWJpYy5saS8ifQ.DJkHv_2K0eNiAkjKia8bxag5I4ixOtjk36AGE6zwzxiEFO_w8ovsoLY4ARONUwnak_N-5-W69PJbbKCphyICpQ
```

## Service Monitoring
You can manage your qubic.li Client with the systemd control.

Start Service: `systemctl start qli`
Stop Service: `systemctl stop qli`
Status Service: `systemctl status qli`

you can also see what is going on by observing the logs.
the service logs to `/var/log/qli.log` or `/var/log/qli.error.log`.

to live watch it on the console, use `tail -f /var/log/qli.log`.

## Customizing
you can customize the settings of your client in the settings file `/q/appsettings.json`

This file contains the configuration of your client and need to be placed at the same location as the executable.
You can create a custom file with the name `appsettings.production.json` which has higher priority to be loaded.

|  Setting 	|  Default Value 	|  Description 	|
|---	|---	|---	|
|  baseUrl 	|  https://mine.qubic.li/ 	|  The Base Url of the API 	|
|  amountOfThreads 	|  1 	|  How many threads should be used for the AI Training	|
|  accessToken 	|  JWT Token 	| This is you personal JWT Token which you can obtain from the Control Panel at qubic.li 	|
|  alias 	|  qli Client 	| You can give your Client a Name which will be displayed in the Control Panel. If empty it uses the Hostname.	|




