# automatic_downtime
Icinga2 eventhandler Script to set an automatic downtime for a host and its services

## FAQ
 * This Script will set a downtime for your host and its services when the condition `max_check_attempts -1` is met.
 * The `DOWNTIME_AUTHOR` must be a unique username that is not used anywhere (user object must not exist), removing downtimes are based on that username.
 * The eventhandler will run on the same host as the host `check_command` runs!
 * You can set a downtime length with the host variable `vars.downtime_length`. 
   Keep in mind that the Icinga Director only store it as a string, so set it in seconds if you use Icinga Director.
   
## Installation

 1. Copy the `eventhandler-automatic-downtime.conf` into your Icinga2 configuration folder.
 2. Copy the script `automtic-downtime` into your Icinga2 `PluginDir`.
 3. Edit `automtic-downtime` and edit these variables to fit your environment:
 ```bash
readonly DOWNTIME_AUTHOR="Automatic Downtime"
readonly API_HOST="localhost"
readonly API_PORT="5665"
readonly API_USERNAME="root"
readonly API_PASSWD="d6312b5777a8c8ba"
```
 4. Create a api user with the rights to set and remove downtimes.

## Configuration

Enable event handler with `enable_event_handler = true` and `event_command = "automatic-downtime"` in your host object.  
If you want a different downtime then 1 day, set the downtime length in seconds with `vars.downtime_length = 3600`.
