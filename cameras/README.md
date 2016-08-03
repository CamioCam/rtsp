# rtsp
This repo contains RTSP url paths for cameras and NVRs. 

The OUI (*O*rganization *U*nique *I*dentifier) of the MAC address 
is used to help narrow the list of candidate camera/NVR models when
scanning the local network for devices. Even though multiple manufacturers
may share the same OUI, because they use the same supplier of network
interface cards/chipsets, the use of the OUI makes scanning faster.


## Fields
| Field | Description | Required |
| ----- | ----------- | -------- |
| company	| The name of the camera manufacturer, e.g. "Sharx" or "Amcrest" | required |
| type | `camera` for standalone IP cameras, or `nvr` for Network Video Recorders | required |
model	| The model name | required |
oui_regex	| The regular expression that matches the OUI of the MAC Address. It's OK to assume uppercase only with colon separators like `(00:80:F0)` | required |
rtsp_url	| The full url that reaches the H.264 RTSP video stream | required |
stream_names	| A `;` separated list of user-facing description of each stream, e.g `high-res 1080p; low-res 640p`. Defaults to `Stream #{{stream}}` | optional |
channel_names	| A `;` separated list of user-facing description of each stream, e.g `CAM1; CAM2`. Defaults to `Channel #{{channel}}` | optional |
video_encoding	| `H.264` and `MPEG4` are the only encodings currently  | required |
port	| The default network port of the RTSP stream, typically `554` | optional |
streams	| A `;` separated list containing all available streams like `0;1;2;3`  | optional |
channels	| For `NVRs`, a `;` separated list of all available channels. Each channel may or may not have more than one stream | optional |
low_res_stream	| The stream with the preferred low-bandwidth encoding | optional |
high_res_stream	| The stream with the preferred hi-bandwidth encoding | optional |
username	| The factory-default username | optional |
password	| The factory-default password | optional |
is_digest_auth_supported | `true` if Digest Authentication is supported (vs. Basic Authentication) | optional
user_manual_url | The url for the latest User Manual | optional |


## Field Template Variables
The [paths.csv](../master/paths.csv) file uses [mustache syntax](https://mustache.github.io/mustache.5.html) to connote variable values in each field. The current variables recognized include:

| Variable | Description |
| -------- | ----------- |
| ip_address | The local network IP address like `192.168.1.37` |
| username | The value supplied in the `username` field |
| password | The value supplied in the `password` field |
| port | The value supplied in the `port` field |
| stream | The stream string like `live_mpeg4.sdp`, `0`, `1`,... `31` |
| channel | The channel string like `0`, `1`,... `31` |
| #base64 | The start of a segment that must be Base64 encoded. For example, `{{#base64}}encode this{{/base64}}` will Base64 encode the portion `encode this`. |

## Pull Requests
Ideally, test all submissions prior to submitting Pull Requests:

1. Use [VLC](https://www.videolan.org/vlc/) to open the `rtsp_url` using the default values specified by `username`, `password` and `port`. For example, the tested url path would look like `rtsp://admin:1234@192.168.1.26:554/live/ch1` for `rtsp_url` for the `rtsp_url` template `rtsp://{{username}}:{{password}}@{{ip_address}}:{{port}}/live/ch{{channel}}`.
2. Create a branch to edit the [paths.csv](../master/paths.csv).
3. Submit a Pull Request for the master branch.

