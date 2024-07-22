# dbus-home-wizzard-energy-p1
Integrate Home Wizzard Energy P1 meter into [Victron Energies Venus OS](https://github.com/victronenergy/venus)

## Purpose
With the scripts in this repo it should be possible to add the Homewizzard P1 meter to VenusOS. 



## Origin
This repo is a fork from https://github.com/back2basic/dbus-Home-Wizzard-Energy-P1 

In this version the import en export totals are calculated correctly for 1-phase systems. 


## Install & Configuration
### Get the code
Just grap a copy of the main branche and copy them to `/data/dbus-Home-Wizzard-Energy-P1`.
After that call the install.sh script.

The following script should do everything for you:
```
wget https://github.com/arendbast/dbus-Home-Wizzard-Energy-P1/archive/refs/heads/main.zip
unzip main.zip "dbus-Home-Wizzard-Energy-P1-main/*" -d /data
mv /data/dbus-Home-Wizzard-Energy-P1-main /data/dbus-Home-Wizzard-Energy-P1
chmod a+x /data/dbus-Home-Wizzard-Energy-P1/install.sh
/data/dbus-Home-Wizzard-Energy-P1/install.sh
rm main.zip
```
⚠️ Check configuration after that - because service is already installed an running and with wrong connection data (host, username, pwd) you will spam the log-file

### Change config.ini
Within the project there is a file `/data/dbus-Home-Wizzard-Energy-P1/config.ini` - just change the values - most important is the host, username and password in section "ONPREMISE". More details below:

| Section  | Config vlaue | Explanation |
| ------------- | ------------- | ------------- |
| DEFAULT  | AccessType | Fixed value 'OnPremise' |
| DEFAULT  | SignOfLifeLog  | Time in minutes how often a status is added to the log-file `current.log` with log-level INFO |
| DEFAULT  | CustomName  | Name of your device - usefull if you want to run multiple versions of the script |
| DEFAULT  | DeviceInstance  | DeviceInstanceNumber e.g. 40 |
| DEFAULT  | Role | Fixed value:  'GRID' |
| DEFAULT  | Position | Fixed value: 0 = AC|
| DEFAULT  | LogLevel  | Define the level of logging - lookup: https://docs.python.org/3/library/logging.html#levels |
| DEFAULT  | Phases  | 1 for 1 phase system / 3 for 3 phase system |
| ONPREMISE  | Host | IP or hostname of on-premise Shelly 3EM web-interface |
<!-- | ONPREMISE  | Username | Username for htaccess login - leave blank if no username/password required |
| ONPREMISE  | Password | Password for htaccess login - leave blank if no username/password required |
| ONPREMISE  | L1Position | Which input on the Shelly in 3-phase grid is supplying a single Multi | -->

## Used documentation
- https://github.com/victronenergy/venus/wiki/dbus#grid   DBus paths for Victron namespace GRID
- https://github.com/victronenergy/venus/wiki/dbus#pv-inverters   DBus paths for Victron namespace PVINVERTER
- https://github.com/victronenergy/venus/wiki/dbus-api   DBus API from Victron
- https://www.victronenergy.com/live/ccgx:root_access   How to get root access on GX device/Venus OS
