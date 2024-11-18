# API developers

## 1. Authentication <a href="#id-1.-authentication" id="id-1.-authentication"></a>

* First, you access the Figma application, select the **App management** menu then select **the Credential tab:**

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FZRNS0qTtcF0qF74wXSlr%252Fimage.png%3Falt%3Dmedia%26token%3Df1d2d071-2dbf-4759-b2e0-a70b1745a0ca&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=bb9ed51c&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* Next, you enter **the Username** and select the corresponding permission **group** (here you group the **Sigma Livestream Full** permission ):

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252F0kzsCs1F9obsluOgveq7%252Fimage.png%3Falt%3Dmedia%26token%3Dca1883a2-df48-458d-aa28-52b8acfc1ab4&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=2582b9dc&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* After you select **Submit , the Sigma** system will generate **a Username** and **Secret Key** . You need to save this password or download the **credential** file by selecting **Download as .env file** .

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FxUMiqevtVz602FMrutNi%252Fimage.png%3Falt%3Dmedia%26token%3Dc25d20a3-ed93-475b-939f-fe4852165efc&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=a23935e&#x26;sv=1" alt=""><figcaption></figcaption></figure>

* After having **Username** and **Secret Key** , you use **Base64Encode** tool to create **token for Authorization** header with the following syntax:

```bash
Authorization: Basic Base64Encode(<Username>:<Secret Key>)
```

* Finally, you get **App ID** information by selecting the **App management menu,** selecting the **General** tab , then you can see **App ID** information as shown below.

<figure><img src="https://docs.vngcloud.vn/~gitbook/image?url=https%3A%2F%2F3672463924-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FB0NrrrdJdpYOYzRkbWp5%252Fuploads%252FbRtqxsdqO1CemO72Hzqo%252Fimage.png%3Falt%3Dmedia%26token%3D98a3bd0b-6f9e-4678-abce-f718e453d3c9&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=9ef4bd31&#x26;sv=1" alt=""><figcaption></figcaption></figure>

## 2. API Create live transcode channel <a href="#id-2.-api-tao-kenh-live-transcode" id="id-2.-api-tao-kenh-live-transcode"></a>

To create a live transcode channel with the following settings:

* Ultra-low-latency
* Available in 03 profiles 1080p, 720p, 480p
* Catchup live session saved to S3 storage _(Note: re-enter channel name and S3 configuration)_

You can use the following API:

```bash
curl --location 'https://api.sigma.video/api/livestream/channels' \
--header 'X-App-Id: <app_id>' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic <token>' \
--data '{
    "name": "<channel_name>",
    "description": null,
    "tags": [],
    "transcodeProfile": [
        "fbffbd08-ed7f-4a51-aabd-3132ac863bb5",
        "54a3d4db-a827-45ae-b6be-1faa21c2e7c6",
        "33a26869-0a1b-49a4-8303-1284ac8fd034"
    ],
    "type": "transcode",
    "mode": "ultra-low-latency",
    "stopTimeout": 30,
    "catchup": true,
    "record": false,
    "outputFormat": "hls",
    "machine": {
        "enabled": true,
        "machineId": "94e98078-b9cb-4d44-b16e-369fdb81da35",
        "machineType": "SIGMA_MACHINE"
    },
    "destinationCatchup": {
        "type": "s3",
        "s3": {
            "accessKey": "<s3_access_key>",
            "bucket": "<bucket_name>",
            "endpoint": "<s3_end_point>",
            "secretKey": "<s3_secrect_key>",
            "region": "<s3_region>",
            "segmentPrefix": null
        }
    }
}'
```

If the API call is successful, the **HTTP Response** code will be **201** , along with the response body being a json object in which the most important information is the id of the newly created channel as in the example below. This **ID** is used in the APIs to start/stop live sessions or delete channels.

```bash
{
    "id": "42efeee4-e94e-4444-b0a6-90850413519d",
    "name": "Channel_02",
    "description": null,
    …
}
```

## 3. Get information of a channel <a href="#id-3.-get-thong-tin-cua-mot-channel" id="id-3.-get-thong-tin-cua-mot-channel"></a>

After creating a channel, you can get the details of a channel by calling the following API:

```bash
curl --location 'https://api.sigma.video/api/livestream/channels/<channel_id>' \
--header 'X-App-Id: <app_id>' \
--header 'Authorization: Basic <token>'
```

If the API call is successful, the HTTP Response code will be **200** . It contains some important information such as:

* `currentSessionId`: if the channel is in a livestream session, we will receive the session id.
* For channels with catchup for VOD configured to be saved to S3, the endpoint to access the master.m3u8 file will look like this:`<s3>/sigma-livestream/<session_id>/catchup/master-catchup.m3u8`
* `rtmpServer`: rtmp url to push stream.
* `streamToken`: stream key.
* `liveStreamUrl`: URL to watch live.

The received data will be as follows:b

```bash
{
    "id": "42efeee4-e94e-4444-b0a6-90850413519d",
    "name": "Channel_02",
    "description": null,
    "tags": [],
    "appId": "0c787e24-87a3-47da-a131-e8310f35aff7",
    "inputId": "e5418288-37be-4d0f-8221-f0c5e99efe5b",
    "transcodeProfile": […],
    "type": "transcode",
    "mode": "ultra-low-latency",
    "stopTimeout": 30,
    "catchup": true,
    "destinationCatchup": {
        "type": "s3",
        "s3": { … }
    },
    "record": false,
    "outputFormat": "hls",
    "status": "active",
    "machine": { … },
    "createdAt": "2024-07-22T10:34:36.772Z",
    "updatedAt": "2024-07-23T06:15:31.729Z",
    "currentSessionId": "977cc345-d771-4223-9306-07c2b9d49a34",
    "input": {
        "streamToken":"42efe-a050270cbbab47cbfacd-3519d",
        "rtmpServer":"rtmp://103.245.251.51:1935/livestream"
    },
    "liveStreamUrl": http://103.245.251.51:8080/manifest/42efeee4-e94e-4444-b0a6-90850413519d/master.m3u8,

} 
```

## 4. API start live channel <a href="#id-4.-api-start-live-channel" id="id-4.-api-start-live-channel"></a>

Use the API as follows to start a live channel:

```bash
curl --location --request PATCH 'https://api.sigma.video/api/livestream/channels/<channel_id>/start' \
--header 'X-App-Id: <app_id>' \
--header 'Authorization: Basic <token>'
```

If the API call is successful, the HTTP Response code will be **200** .

## 5. API stop live channel <a href="#id-5.-api-stop-live-channel" id="id-5.-api-stop-live-channel"></a>

Use the API as follows to stop a live channel:

```bash
curl --location --request DELETE 'https://api.sigma.video/api/livestream/channels/<channel_id>/stop' \
--header 'X-App-Id: <app_id>' \
--header 'Authorization: Basic <token>'
```

If the API call is successful, the HTTP Response code will be **200** .

## 6. Delete a channel <a href="#id-6.-xoa-mot-channel" id="id-6.-xoa-mot-channel"></a>

To delete a channel, use the API as follows:

```bash
curl --location 'https://api.sigma.video/api/livestream/sessions?q={"channelId":"<channel_id>"}&sort=updatedAt|desc&page=1&perPage=100' \
--header 'X-App-Id: <app_id>' \
--header 'Authorization: Basic <token>'
```

If the API call is successful, the HTTP Response code will be **200** .

## 7. List live sessions of a channel <a href="#id-7.-liet-ke-danh-sach-live-session-cua-mot-channel" id="id-7.-liet-ke-danh-sach-live-session-cua-mot-channel"></a>

Each livestream session of a channel will be tracked as a session. We can use the following API to get a list of sessions of a channel:

```bash
curl --location 'https://api.sigma.video/api/livestream/sessions?q={"channelId":"<channel_id>"}&sort=updatedAt|desc&page=1&perPage=100' \
--header 'X-App-Id: <app_id>' \
--header 'Authorization: Basic <token>'
```

If the API call is successful, the HTTP Response code will be 200. The result will be as shown in the following sample:

```bash
{
    "data": [
        {
            "name": "Channel_02_2024-07-22-11:33:50",
            "status": "ended",
            "appId": "0c787e24-87a3-47da-a131-e8310f35aff7",
            "recordUrls": [],
            "clientInfo": {
                "action": "on_publish",
                "stream": "42efe-a050270cbbab47cbfacd-3519d",
                "ip": "103.245.252.19",
                "client_id": "y1799srf",
                "param": "",
                "tcUrl": "rtmp://103.245.251.51:1935/livestream",
                "ips": [],
                "app": "livestream",
                "stream_id": "vid-4024822"
            },
            "duration": 40,
            "isCreateTask": true,
            "channelId": "42efeee4-e94e-4444-b0a6-90850413519d",
            "channel": {
                "id": "42efeee4-e94e-4444-b0a6-90850413519d",
                "name": "Channel_02",
                ...
            },
            "id": "5017085c-d828-491d-837f-2160df3e07c1",
            "events": [],
            "createdAt": "2024-07-22T11:33:50.903Z",
            "updatedAt": "2024-07-22T11:35:02.898Z",
            "startedAt": "2024-07-22T11:34:20.064Z",
            "finishedAt": "2024-07-22T11:35:02.898Z"
        },
        {
            "name": "Channel_02_2024-07-22-11:32:35",
            "status": "ended",
            "appId": "0c787e24-87a3-47da-a131-e8310f35aff7",
            "recordUrls": [],
            "clientInfo": {
                "action": "on_publish",
                "stream": "42efe-a050270cbbab47cbfacd-3519d",
                "ip": "103.245.252.19",
                "client_id": "ii05j356",
                "param": "",
                "tcUrl": "rtmp://103.245.251.51:1935/livestream",
                "ips": [],
                "app": "livestream",
                "stream_id": "vid-2wx9608"
            },
            "duration": 10,
            "isCreateTask": true,
            "channelId": "42efeee4-e94e-4444-b0a6-90850413519d",
            "channel": {
                "id": "42efeee4-e94e-4444-b0a6-90850413519d",
                "name": "Channel_02"
				...
            },
            "events": [],
            "createdAt": "2024-07-22T11:32:35.675Z",
            "updatedAt": "2024-07-22T11:33:19.362Z",
            "startedAt": "2024-07-22T11:33:05.117Z",
            "finishedAt": "2024-07-22T11:33:19.362Z"
        }
    ],
    "total": 2,
    "count": 2,
    "page": 1,
    "perPage": 100
}
```

## 8. View the status of a session <a href="#id-8.-xem-status-cua-mot-session" id="id-8.-xem-status-cua-mot-session"></a>

We can get the active status of a live session by calling the following API:

```bash
curl --location 'https://api.sigma.video/api/livestream/sessions/<session_id>/status' \
--header 'X-App-Id: <app_id>' \
--header 'Authorization: Basic <token>'
```

If the API call is successful, the HTTP Response code will be 200. The result will be as shown in the following sample:

```bash
{"status":"live"}
```

## 9. List the events of a session <a href="#id-9.-liet-ke-danh-sach-event-cua-mot-session" id="id-9.-liet-ke-danh-sach-event-cua-mot-session"></a>

During the operation of a session, actions such as: initialize, stop, start, signal interrupted, signal restored, etc. will be generated and tracked as events. We can use the API below to get a list of events:

```bash
curl --location 'https://api.sigma.video/api/livestream/events?q={"$and":[{"sessionId":"<session_id>"}]}&sort=updatedAt|desc&page=1&perPage=100' \
--header 'X-App-Id: <app_id>' \
--header 'Authorization: Basic <token>'
```

If the API call is successful, the HTTP Response code will be 200. The result will be as shown in the following sample:

```bash
{
    "data": [
        {
            "actor": "user",
            "action": "ended",
            "sessionId": "5017085c-d828-491d-837f-2160df3e07c1",
            "id": "3b393448-65a8-4258-a418-2bfaa8cda40d",
            "createdAt": "2024-07-22T11:35:02.901Z",
            "updatedAt": "2024-07-22T11:35:02.901Z",
            "message": "Kênh đã kết thúc"
        },
        {
            "action": "stable",
            "sessionId": "5017085c-d828-491d-837f-2160df3e07c1",
            "id": "66df86b4-c0ed-4db7-868c-a12ca1830c58",
            "createdAt": "2024-07-22T11:34:20.063Z",
            "updatedAt": "2024-07-22T11:34:20.063Z",
            "message": "Kênh ổn định"
        }
	]
}
```
