# Configuration

The [configs](../master/configs/configs.csv) file contains a list of configuration commands for any number of cameras listed in the [paths](../master/cameras/paths.csv) file.


## Fields

| Field | Description | Required |
| ----- | ----------- | -------- |
| maker	| The name of the camera manufacturer, e.g. "Sharx" or "Amcrest" | required |
| command_id	| An unique identifier string for the command, e.g. "enable_wifi" | required |
| url	| The full url used to execute the camera configuration | required |
| method | The method used to access `url`, e.g. "GET" | required |
| regex_model	| A regex representing all the models that support the comamnd, e.g "SCNC3[89]0[45]" | required |
| regex_firmware	| A regex representing all the firmware versions that support the comamnd, e.g "^v4" | required |
| regex_success	| A regex that represents the response of a command successfully executed | optional |

## Field Template Variables
The [configs.csv](../master/cameras/paths.csv) file uses [mustache syntax](https://mustache.github.io/mustache.5.html) to connote variable values in each field. The current variables recognized include:

| Variable | Description |
| -------- | ----------- |
| ip_address | The local network IP address like `192.168.1.37` |
| wifi_ssid | The SSID of the local network |
| wifi_password | The password of the local network |

## Pull Requests

Ideally, test all submissions prior to submitting Pull Requests by searching the camera manual for the right commands and executing them locally via curl, or application of your preference.

Also keep in mind that disabling/resetting commands should have a different `command_id`,
i.e. `/form/setWlan/?ENABLE=1` would be assigned to `enable_wifi` while `/form/setWlan/?ENABLE=0` would be assined to `disable_wifi`.
