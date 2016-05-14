# rtsp
This repo contains RTSP url paths for cameras and NVRs.

## Fields
| Field | Description | Required |
| ----- | ----------- | -------- |
| company	| The name of the company associated with the OUI | required |
| type | _camera_ for standalone IP cameras, or _nvr_ for Network Video Recorders | required |
model	| The model name | required |
oui_regex	| The regular expression that matches the OUI of the MAC Address | required |
rtsp_url	| The full url that reaches the H.264 RTSP video stream | required |
stream_name_template	| A user-facing description of a particular stream_number | optional |
video_encoding	| _H.264_ is the only encoding supported by CamioBox currently  | required |
port	| The default network port of the RTSP stream, typically _554_ | optional |
min_stream_number	| The lowest channel/stream number (e.g. _0_ or _1_) | optional |
max_stream_number	| The highest channel/stream number (e.g. _15_ or _16_) | optional |
low_res_stream_number	| The stream_number with the preferred low-bandwidth encoding | optional |
high_res_stream_number	| The stream_number with the preferred hi-bandwidth encoding | optional |
username	| The factory-default username | optional |
password	| The factory-default password | optional |
user_manual_url | The url for the latest User Manual | optional |


## Field Template Variables
The [paths.csv](../blob/master/paths.csv) file uses [mustache syntax](https://mustache.github.io/mustache.5.html) to connote variable values in each field. The current variables recognized include:
| Variable | Description |
| -------- | ----------- |
| ip_address | The local network IP address like _192.168.1.37 |
| username | The value supplied in the username field |
| password | The value supplied in the password field |
| port | The value supplied in the port field |
| stream_number | The channel/stream number like _0_, _1_,... _31_ |
| #base64 | The start of a segment that must be Base64 encoded. For example, {{#base64}}encode this{{/base64}} will Base64 encode the portion _encode this_. |

## Pull Requests
Ideally, test all submissions prior to submitting Pull Requests:
1. Use [VLC](https://www.videolan.org/vlc/) to open the _rtsp_url_ using the default values specified by _username_, _password_ and _port_.
2. Create a branch to edit the [paths.csv](../blob/master/paths.csv).
3. Submit a Pull Request for the master branch.

