# Pixverse Video Generation API

This service has implemented the integration of Pixverse AI, which can be used to generate videos and other content.

API home page: [Ace Data Cloud - Pixverse Video Generation](https://platform.acedata.cloud/services/74e74695-ceff-49d1-ac84-cfa876225ae8)

## Get Started


This article will introduce the integration instructions for the Pixverse Videos Generation API, which can generate official Pixverse videos by inputting custom parameters.

### Application and Usage

To use the Pixverse Videos Generation API, you can first visit the [Pixverse Videos Generation API](https://platform.acedata.cloud/documents/00f200b3-709d-4783-ac56-3d27cc70b73d) page and click the "Acquire" button to obtain the credentials needed for the request:

![](https://cdn.acedata.cloud/nyq0xz.png)

If you are not logged in or registered, you will be automatically redirected to the login page inviting you to register and log in. After logging in or registering, you will be automatically returned to the current page.

Upon the first application, there will be a free quota provided, allowing you to use the API for free.

### Basic Usage

You can generate videos based on prompts, for example, you can input `quiver`, as shown in the image:

<p><img src="https://cdn.acedata.cloud/azz8d3.png" width="500" class="m-auto"></p>

The generated code is as follows:

<p><img src="https://cdn.acedata.cloud/g5j3f2.png" width="500" class="m-auto"></p>

Main request parameters:

- `model`: The model for generating the video, default is `v3.5`.
- `action`: The action for generating the video, default is `generate`, optional `extend`.
- `prompt`: The prompt for generating the video (required).
- `style`: Optional video style.
- `motion`: Motion mode, default is normal.
- `quality`: Video clarity, default is `540p`.
- `duration`: Video duration, 5 or 8 seconds, default is 5.
- `image_url`: Reference image for the first frame, optional.
- `aspect_ratio`: Aspect ratio, default is `16:9`.
- `seed`: Optional, fixed random seed.
- `template_id`: Optional, specify template effects.
- `callback_url`: URL for callback results.

You can click the "Try" button to directly test the API, wait for 1-2 minutes, and the result is as follows:

```json
{
  "success": true,
  "task_id": "69e677ca-f1de-419f-99a4-cb39ea0cb5fc",
  "trace_id": "e544f904-ac13-4b42-a26e-2de69d9ac06b",
  "data": [
    {
      "id": 317982208110208,
      "first_frame": "",
      "video_width": 0,
      "video_height": 0,
      "prompt": "quiver",
      "model": "v3.5",
      "quality": "360p",
      "motion": "normal",
      "video_url": "https://media.pixverse.ai/pixverse%2Fmp4%2Fmedia%2Fweb%2F77e48783-3dc9-48ab-84a0-0e310ff9b83d_seed0.mp4",
      "template_id": 0,
      "template_name": "",
      "style": "",
      "aspect_ratio": "16:9",
      "duration": 5,
      "extended": 0,
      "last_frame": "",
      "seed": 0,
      "asset_id": 0,
      "asset_name": ""
    }
  ]
}
```

At this point, we have obtained the content of a video, including video ID, video link, video clarity, video duration, and other content.

Field descriptions are as follows:

- success: Whether the generation was successful, if successful then `true`, otherwise `false`
- task_id: The ID of this generation task
- trace_id: The tracking ID of this generation task
- data: A list containing detailed information about the generated video.
  - id: The unique ID of the generated video, which can be used for subsequent expansion generation
  - first_frame: The link to the first frame image of the video
  - last_frame: The link to the last frame image of the video
  - video_width: The width of the video result
  - video_height: The length of the video result
  - prompt: The prompt for this video generation task
  - model: The model used for this video generation task
  - video_url: The video link for this video generation task
  - template_id: The ID of the template effects used in the video
  - template_name: The name of the template effects used in the video
  - asset_id: The ID of the character used in the video
  - asset_name: The name of the character used in the video
  - style: The style of this video generation task
  - aspect_ratio: The size of this video
  - extended: Whether this video is an extended generation, 0 means it is not an extended generation, otherwise it is an extended generation

### Custom First and Last Frame Video Generation

If you want to customize the first and last frames for video generation, you can input the links to the first and last frame images:

At this time, the `frame` field can accept content similar to the following:

- First frame image
  <p><img src="https://cdn.acedata.cloud/c7zzmb.png" width="500" class="m-auto"></p>
- Last frame image
  <p><img src="https://cdn.acedata.cloud/fqd8br.png" width="500" class="m-auto"></p>

Next, we need to customize the song generation based on lyrics, title, and style, specifying the following content:

- action: The action for this video generation task, which can be either generate video `action` or extend video `extend`
- prompt: The prompt for this video generation task.
- frame: An array of video links for the first and last frames generated.

An example of the filled form is as follows:

<p><img src="https://cdn.acedata.cloud/4ea6pa.png" width="500" class="m-auto"></p>

After filling it out, the generated code is as follows:

<p><img src="https://cdn.acedata.cloud/yfzxxn.png" width="500" class="m-auto"></p>

Corresponding Shell code:

```python
curl -X POST 'https://api.acedata.cloud/pixverse/videos' \
-H 'accept: application/json' \
-H 'authorization: Bearer {token}' \
-H 'content-type: application/json' \
-d '{
  "action": "generate",
  "prompt": "gradation",
  "frame": ["https://cdn.acedata.cloud/c7zzmb.png","https://cdn.acedata.cloud/fqd8br.png"]
}'
```

Testing is allowed, and the generated effect is similar.

### Custom Video Template Effects Generation

If you want to use specific video template effects to generate videos, you only need to add a template ID field `template_id` to specify the template effects. We provide the following template effects, and the specific template effects are shown in the image below:

```json
[
    {
        "display_name": "Muscle Surge",
        "workflow_tag": "muscle_241128",
        "template_id": 308621408717184,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fwithbaby.gif",
        "thumbnail_video_path": "",
        "marker": "hot",
        "created_at": "2024-11-28T17:53:21Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "Show off your strong muscles and have everyone hooked.",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"成为肌肉猛男\",\"display_prompt\":\"体验猛男快乐\"}}",
        "example_list": "[{\"img_id\":113750602,\"img_url\":\"https://media.pixverse.ai/upload%2F920dc791-8c9f-4518-8761-82958a827190.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"},{\"img_id\":113750791,\"img_url\":\"https://media.pixverse.ai/upload%2Ff2853009-8238-4e0f-93ec-cfc68fee28b7.png\"}]",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Hug Your Love",
        "workflow_tag": "hug_love_241030",
        "template_id": 303624424723200,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fhug2.gif",
        "thumbnail_video_path": "",
        "marker": "hot",
        "created_at": "2024-10-31T12:07:47Z",
        "updated_at": "2025-01-06T05:32:42Z",
        "display_prompt": "Hug each other\t",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"爱的抱抱\",\"display_prompt\":\"互相拥抱在一起\"}}",
        "example_list": "[{\"img_id\":113741803,\"img_url\":\"https://media.pixverse.ai/upload%2Fb2626bc2-050d-4ea6-a864-e2054c012df5.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"}]",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Alive Art",
        "workflow_tag": "alive_art_241028",
        "template_id": 302325299721280,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Faliveart.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-10-24T03:55:29Z",
        "updated_at": "2025-01-06T05:32:53Z",
        "display_prompt": "The [OBJECT] comes to life and walks out of the [SCENE]",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"活灵活现\",\"display_prompt\":\"它活了！\"}}",
        "example_list": "",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Sheep Curls",
        "workflow_tag": "sheep_241208",
        "template_id": 310371322329472,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2FSheepCurls.gif",
        "thumbnail_video_path": "",
        "marker": "new",
        "created_at": "2024-12-08T15:14:11Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "Change hairstyle for a better mood",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"万物皆可羊毛卷\",\"display_prompt\":\"心情不好，换个发型看看\"}}",
        "example_list": "[{\"img_id\":113741803,\"img_url\":\"https://media.pixverse.ai/upload%2Fb2626bc2-050d-4ea6-a864-e2054c012df5.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"}]",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Sailor Moon",
        "workflow_tag": "meishaonv_241225",
        "template_id": 313359138372032,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fmeishaonv2.gif",
        "thumbnail_video_path": "",
        "marker": "",
        "created_at": "2024-12-25T12:29:05Z",
        "updated_at": "2025-01-06T05:32:33Z",
        "display_prompt": "Moon Prism Power, Make Up!",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"成为美少女战士\",\"display_prompt\":\"月之水晶力量，变身！\"}}",
        "example_list": "",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Black Myth: Wukong",
        "workflow_tag": "heiwukong_241225",
        "template_id": 313359209531840,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fmonkey.gif",
        "thumbnail_video_path": "",
        "marker": "",
        "created_at": "2024-12-25T12:29:40Z",
        "updated_at": "2025-01-06T05:32:25Z",
        "display_prompt": "I am Sun Wukong, the Victorious Fighting Buddha!",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"黑悟空引擎\",\"display_prompt\":\"放马西行，直面天命！\"}}",
        "example_list": "",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Santa's Secret Gifts",
        "workflow_tag": "santa_gift_241213",
        "template_id": 311521768592256,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fgift111.gif",
        "thumbnail_video_path": "",
        "marker": "new",
        "created_at": "2024-12-15T03:16:32Z",
        "updated_at": "2024-12-30T06:08:16Z",
        "display_prompt": "I want a：",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"圣诞礼物盲盒\",\"display_prompt\":\"我想要：\"}}",
        "example_list": "[{\"img_id\":113741803,\"img_url\":\"https://media.pixverse.ai/upload%2Fb2626bc2-050d-4ea6-a864-e2054c012df5.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"}]",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }
]
{
        "display_name": "Where is Santa?",
        "workflow_tag": "where_is_santa_241213",
        "template_id": 311521879229312,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fwheresanta.gif",
        "thumbnail_video_path": "",
        "marker": "new",
        "created_at": "2024-12-15T03:17:26Z",
        "updated_at": "2024-12-30T06:08:24Z",
        "display_prompt": "Discovering Santa Claus in the parallel world!",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"Where is Santa?\",\"display_prompt\":\"“Discover” Santa Claus all over the world\"}}",
        "example_list": "[{\"img_id\":119280295,\"img_url\":\"https://media.pixverse.ai/upload%2Fde34a072-325e-4d86-88d9-2daef292e1b4.jpeg\"},{\"img_id\":119280616,\"img_url\":\"https://media.pixverse.ai/upload%2F5b4da0a2-86c3-4204-adda-74bfa7c3d0d1.jpg\"}]",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Christmas OOTD",
        "workflow_tag": "tobe_santa_241219",
        "template_id": 312314911869312,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fbesanta33.gif",
        "thumbnail_video_path": "",
        "marker": "new",
        "created_at": "2024-12-19T14:51:09Z",
        "updated_at": "2024-12-30T06:08:08Z",
        "display_prompt": "Dress up as a Christmas star",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"Christmas Outfit\",\"display_prompt\":\"Test what Christmas outfit suits you\"}}",
        "example_list": "[{\"img_id\":113741803,\"img_url\":\"https://media.pixverse.ai/upload%2Fb2626bc2-050d-4ea6-a864-e2054c012df5.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"}]",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "We Are Venom!",
        "workflow_tag": "venom_241030",
        "template_id": 303624537709312,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2FWeAreVenom.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-10-31T12:08:42Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "Transform into a [BLACK] Venom",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"Venom Transformation!\",\"display_prompt\":\"Transform into [BLACK] Venom\"}}",
        "example_list": "[{\"img_id\":113750602,\"img_url\":\"https://media.pixverse.ai/upload%2F920dc791-8c9f-4518-8761-82958a827190.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"},{\"img_id\":113750791,\"img_url\":\"https://media.pixverse.ai/upload%2Ff2853009-8238-4e0f-93ec-cfc68fee28b7.png\"}]",
        "qualities": [
            "360p",
            "540p"
        ]
    }, {
        "display_name": "Hot Harley Quinn",
        "workflow_tag": "harley_quinn_241121",
        "template_id": 307489434436288,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2FHotHarleyQuinn.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-11-22T08:21:19Z",
        "updated_at": "2024-12-26T07:40:43Z",
        "display_prompt": "Transform into Harley Quinn, mastering allure and chaos",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"Harley Quinn Transformation\",\"display_prompt\":\"Transform into Harley Quinn, mastering allure and chaos\"}}",
        "example_list": "[{\"img_id\":113741803,\"img_url\":\"https://media.pixverse.ai/upload%2Fb2626bc2-050d-4ea6-a864-e2054c012df5.png\"},{\"img_id\":113742000,\"img_url\":\"https://media.pixverse.ai/upload%2F19090035-612e-40ed-9c8d-a7aaf781d492.png\"},{\"img_id\":113742074,\"img_url\":\"https://media.pixverse.ai/upload%2F50ed9020-7b58-4dd9-aa39-ff06b9e0df12.png\"}]",
        "qualities": [
            "360p",
            "540p"
        ]
    }, {
        "display_name": "Crazy Cat Woman",
        "workflow_tag": "cat_woman_241121",
        "template_id": 307489548427968,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2FCrazyCatWoman.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-11-22T08:22:15Z",
        "updated_at": "2024-12-26T07:40:24Z",
        "display_prompt": "Transform into a Crazy Cat Woman and slay",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"Crazy Cat Woman Transformation\",\"display_prompt\":\"Transform into a seductive cat woman, captivating everyone!\"}}",
        "example_list": "[{\"img_id\":113742074,\"img_url\":\"https://media.pixverse.ai/upload%2F50ed9020-7b58-4dd9-aa39-ff06b9e0df12.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"},{\"img_id\":113750791,\"img_url\":\"https://media.pixverse.ai/upload%2Ff2853009-8238-4e0f-93ec-cfc68fee28b7.png\"}]",
        "qualities": [
            "360p",
            "540p"
        ]
    }, {
        "display_name": "Wonder Woman",
        "workflow_tag": "wonder_woman_241202",
        "template_id": 309283958194560,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2FWonderWoman.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-12-02T11:45:11Z",
        "updated_at": "2024-12-26T07:40:35Z",
        "display_prompt": "Transform into Wonder Woman and conquer the impossible",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"Wonder Woman Transformation\",\"display_prompt\":\"Become Wonder Woman, conquering all impossibilities\"}}",
        "example_list": "[{\"img_id\":113742074,\"img_url\":\"https://media.pixverse.ai/upload%2F50ed9020-7b58-4dd9-aa39-ff06b9e0df12.png\"},{\"img_id\":113750791,\"img_url\":\"https://media.pixverse.ai/upload%2Ff2853009-8238-4e0f-93ec-cfc68fee28b7.png\"}]",
        "qualities": [
            "360p",
            "540p"
        ]
    },
{
        "display_name": "Hulk",
        "workflow_tag": "hulk_241106",
        "template_id": 304826314164992,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2FHulk.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-11-07T07:08:47Z",
        "updated_at": "2024-12-26T07:38:48Z",
        "display_prompt": "Unleash the Beast",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"召唤绿巨人\",\"display_prompt\":\"变身成绿巨人并捶爆一切\"}}",
        "example_list": "[{\"img_id\":113750602,\"img_url\":\"https://media.pixverse.ai/upload%2F920dc791-8c9f-4518-8761-82958a827190.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"},{\"img_id\":113750791,\"img_url\":\"https://media.pixverse.ai/upload%2Ff2853009-8238-4e0f-93ec-cfc68fee28b7.png\"}]",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Joker's Rebirth",
        "workflow_tag": "joker_241106",
        "template_id": 304826126435072,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_joker.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-11-07T07:07:16Z",
        "updated_at": "2024-12-26T07:38:54Z",
        "display_prompt": "Transform into a Joker",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"小丑重生\",\"display_prompt\":\"变身成小丑，诡异地微笑\"}}",
        "example_list": "[{\"img_id\":113750602,\"img_url\":\"https://media.pixverse.ai/upload%2F920dc791-8c9f-4518-8761-82958a827190.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"},{\"img_id\":113750791,\"img_url\":\"https://media.pixverse.ai/upload%2Ff2853009-8238-4e0f-93ec-cfc68fee28b7.png\"}]",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Batman",
        "workflow_tag": "bat_man_241106",
        "template_id": 304826374632192,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_batman.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-11-07T07:09:17Z",
        "updated_at": "2024-12-26T07:39:00Z",
        "display_prompt": "Transform into a Batman and embrace the night",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"蝙蝠侠归来\",\"display_prompt\":\"变身成蝙蝠侠并守护黑夜\"}}",
        "example_list": "[{\"img_id\":113741803,\"img_url\":\"https://media.pixverse.ai/upload%2Fb2626bc2-050d-4ea6-a864-e2054c012df5.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"}]",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Iron Man",
        "workflow_tag": "iron_man_241106",
        "template_id": 304826054394624,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_ironman.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-11-07T07:06:40Z",
        "updated_at": "2024-12-26T07:39:06Z",
        "display_prompt": "Activate Iron Mode",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"钢铁侠变身\",\"display_prompt\":\"激活钢铁模式\"}}",
        "example_list": "[{\"img_id\":113741803,\"img_url\":\"https://media.pixverse.ai/upload%2Fb2626bc2-050d-4ea6-a864-e2054c012df5.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"}]",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Hair Growth Magic",
        "workflow_tag": "hair_magic_241128",
        "template_id": 308552687706496,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_hairgrowth.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-11-28T08:34:06Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "Grow lots of hair. Never be bald.",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"发量王者\",\"display_prompt\":\"长出迷人秀发，永无秃头困扰。\"}}",
        "example_list": "[{\"img_id\":113750602,\"img_url\":\"https://media.pixverse.ai/upload%2F920dc791-8c9f-4518-8761-82958a827190.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"},{\"img_id\":113750791,\"img_url\":\"https://media.pixverse.ai/upload%2Ff2853009-8238-4e0f-93ec-cfc68fee28b7.png\"}]",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "COLORFUL Venom!",
        "workflow_tag": "random_venom_241104",
        "template_id": 304358279051648,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_colorfulvenom.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-11-04T15:39:54Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "Transform into a [COLORFUL] Venom",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"毒液！(彩色盲盒版)\",\"display_prompt\":\"变身成为【彩色】毒液\"}}",
        "example_list": "[{\"img_id\":113741803,\"img_url\":\"https://media.pixverse.ai/upload%2Fb2626bc2-050d-4ea6-a864-e2054c012df5.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"}]",
        "qualities": [
            "360p",
            "540p"
        ]
    },
{
        "display_name": "Who is Venom?",
        "workflow_tag": "who_is_venom_241112",
        "template_id": 305714097668480,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_whoisvenom.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-11-12T07:33:35Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "Which one of you guys is Venom? ",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"测测谁是毒液？\",\"display_prompt\":\"两人之中，必有一毒，速速现出原形\"}}",
        "example_list": "[{\"img_id\":111917190,\"img_url\":\"https://media.pixverse.ai/upload%2F6a6a0f6a-99be-4eac-83a1-9d265ca65823.png\"},{\"img_id\":111917753,\"img_url\":\"https://media.pixverse.ai/upload%2F079945d6-01aa-4688-9e9a-02e308c01db5.png\"},{\"img_id\":111917942,\"img_url\":\"https://media.pixverse.ai/upload%2F814307ed-4123-4f6b-a32e-4072b55378cb.png\"}]",
        "qualities": [
            "360p",
            "540p"
        ]
    }, {
        "display_name": "Get a Venom buddy",
        "workflow_tag": "baby_venom_241114",
        "template_id": 306059795500352,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_venombuddy.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-11-14T06:26:53Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "Your Venom buddy appears and gives you a hug",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"召唤毒液兄弟\",\"display_prompt\":\"你的毒液兄弟回到你身边，并与你深情相拥\"}}",
        "example_list": "[{\"img_id\":113741803,\"img_url\":\"https://media.pixverse.ai/upload%2Fb2626bc2-050d-4ea6-a864-e2054c012df5.png\"},{\"img_id\":113750690,\"img_url\":\"https://media.pixverse.ai/upload%2Fddd29e75-beeb-461c-9388-3e14c2709e73.png\"}]",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Wicked Shots",
        "workflow_tag": "wicked_paintings_241028",
        "template_id": 303788802773760,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_wickedshot.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-11-01T10:25:30Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "The [SUBJECT] in the picture smiles wickedly and starts firing",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"扫射一切\",\"display_prompt\":\"邪魅一笑，并掏出一把机关枪开始扫射\"}}",
        "example_list": "",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Squish It",
        "workflow_tag": "squish_it_241028",
        "template_id": 302325299692608,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_squishit.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-10-24T03:55:29Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "A pair of hands appears and squishes the [OBJECT] as if it's slime",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"捏捏更解压\",\"display_prompt\":\"变成可以捏捏的软泥\"}}",
        "example_list": "",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Lego Blast",
        "workflow_tag": "lego_blast_241028",
        "template_id": 302325299702848,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_legoblast.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-10-24T03:55:29Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "The [OBJECT] shatters into pieces of Legos",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"乐高大爆炸\",\"display_prompt\":\"爆炸并碎裂成一片片乐高积木\"}}",
        "example_list": "",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Leggy Run",
        "workflow_tag": "leggy_run_241028",
        "template_id": 302325299711040,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_leggyrun.gif",
        "thumbnail_video_path": "",
        "marker": "hot",
        "created_at": "2024-10-24T03:55:29Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "The [OBJECT] grows legs and runs away",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"全员腿精\",\"display_prompt\":\"长出了一双腿然后开始乱跑\"}}",
        "example_list": "",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Monster Invades",
        "workflow_tag": "monster_invasion_241028",
        "template_id": 302325299682368,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_monster.gif",
        "thumbnail_video_path": "",
        "marker": "default",
        "created_at": "2024-10-24T03:55:29Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "A monster suddenly appears in the [SCENE] and starts walking around",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"怪兽入侵\",\"display_prompt\":\"场景中突然出现了一只怪兽\"}}",
        "example_list": "",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }
```json
{
        "display_name": "Wizard Hat",
        "workflow_tag": "animal_wizard_241028",
        "template_id": 302325299661888,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_wizardhat.gif",
        "thumbnail_video_path": "",
        "marker": "hot",
        "created_at": "2024-10-24T03:55:29Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "The [SUBJECT] wears a magic wizard hat",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"戴上魔法帽\",\"display_prompt\":\"头顶出现了一顶可爱的魔法帽\"}}",
        "example_list": "",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Zombie Hand",
        "workflow_tag": "zombie_hand_241028",
        "template_id": 302325299672128,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_weirdhand.gif",
        "thumbnail_video_path": "",
        "marker": "hot",
        "created_at": "2024-10-24T03:55:29Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "A zombie hand appears in the [SCENE]",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"僵尸手出没\",\"display_prompt\":\"从图片中的场景中钻出一只僵尸的手\"}}",
        "example_list": "",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }, {
        "display_name": "Zombie Mode",
        "workflow_tag": "zombie_mode_241028",
        "template_id": 302325299651648,
        "thumbnail_path": "https://media.pixverse.ai/asset%2Ftemplate%2Fcapcut_zombiemode.gif",
        "thumbnail_video_path": "",
        "marker": "hot",
        "created_at": "2024-10-24T03:55:29Z",
        "updated_at": "2024-12-25T10:19:28Z",
        "display_prompt": "The [SUBJECT] suddenly transforms into a zombie.",
        "i18n_json": "{\"zh-CN\":{\"display_name\":\"坏了，我变僵尸了\",\"display_prompt\":\"突然变成僵尸\"}}",
        "example_list": "",
        "qualities": [
            "360p",
            "540p",
            "720p",
            "1080p"
        ]
    }
]
```

We can choose a `template_id` from above to generate a video. We take `302325299651648` as an example to generate a video, and the other parameters are similar to basic usage. The specific parameters are shown in the image below:

<p><img src="https://cdn.acedata.cloud/pwbyma.png" width="500" class="m-auto"></p>

After filling in, the automatically generated code is as follows:

<p><img src="https://cdn.acedata.cloud/gb09le.png" width="500" class="m-auto"></p>

The corresponding Python code:

```python
import requests

url = "https://api.acedata.cloud/pixverse/videos"

headers = {
    "accept": "application/json",
    "authorization": "Bearer {token}",
    "content-type": "application/json"
}

payload = {
    "action": "generate",
    "prompt": "A group of people began to dance",
    "template_id": 302325299651648,
    "image_url": "https://cdn.acedata.cloud/n3r1mc.png"
}

response = requests.post(url, json=payload, headers=headers)
print(response.text)
```

Clicking run, you can find that you will get a result as follows:

```json
{
  "success": true,
  "task_id": "cf127eee-d23d-44c9-945c-793e68f86720",
  "trace_id": "aa7ed21d-8363-4eeb-a46a-a120e31b4fde",
  "data": [
    {
      "id": 318162170958272,
      "first_frame": "",
      "video_width": 0,
      "video_height": 0,
      "prompt": "A group of people began to dance",
      "model": "v3.5",
      "quality": "360p",
      "motion": "normal",
      "video_url": "https://media.pixverse.ai/pixverse%2Fmp4%2Fmedia%2Fweb%2F18d7fef6-2e59-48a5-a655-046464f34603_seed0.mp4",
      "template_id": 302325299651648,
      "template_name": "Zombie Mode",
      "style": "",
      "aspect_ratio": "16:9",
      "duration": 5,
      "extended": 0,
      "last_frame": "",
      "seed": 0,
      "asset_id": 0,
      "asset_name": ""
    }
  ]
}
```

It can be seen that the result content is the same as the video template effect, which also realizes the function of generating videos using template effects.

### Continue to expand video generation function

If you want to expand the generated Pixverse video, you can set the parameter `action` to `extend`, and input the ID of the video to be expanded. The video ID can be obtained based on basic usage, as shown in the image below:

<p><img src="https://cdn.acedata.cloud/kwcdyg.png" width="500" class="m-auto"></p>

At this time, you can see that the video ID is:

```
"id": 317989274748288
```

> Note that the `id` in the video here is the ID of the generated video. If you do not know how to generate a video, you can refer to the basic usage above to generate a video.

Next, we must fill in the lyrics and style to customize the generated song, and we can specify the following content:

- action: The behavior of this video generation task, generally there are normal generation `generate` and extended video `extend`.
- prompt: The prompt for this video generation.
- video_id: The reference video ID for this expansion video task.

The sample input is as follows:

<p><img src="https://cdn.acedata.cloud/hio4x5.png" width="500" class="m-auto"></p>

After filling in, the automatically generated code is as follows:

<p><img src="https://cdn.acedata.cloud/ts5xif.png" width="500" class="m-auto"></p>

The corresponding Python code:

```python
import requests

url = "https://api.acedata.cloud/pixverse/videos"

headers = {
    "accept": "application/json",
    "authorization": "Bearer {token}",
    "content-type": "application/json"
}

payload = {
    "action": "extend",
    "prompt": "A group of people began to dance",
    "video_id": 317989274748288
}

response = requests.post(url, json=payload, headers=headers)
print(response.text)
```

Clicking run, you can find that you will get a result as follows:
```
```json
{
  "success": true,
  "task_id": "38b6d70d-eea2-40da-9f8b-945df93e831b",
  "trace_id": "b105bbb6-faf1-4d86-9c10-4b8a8e638d05",
  "data": [
    {
      "id": 318162960027008,
      "first_frame": "",
      "video_width": 0,
      "video_height": 0,
      "prompt": "A group of people began to dance",
      "model": "v3.5",
      "quality": "360p",
      "motion": "normal",
      "video_url": "https://media.pixverse.ai/pixverse%2Fmp4%2Fmedia%2Fweb%2F2368ad8b-81dc-4a2f-9b6c-e0ac205351f9_seed0.mp4",
      "template_id": 0,
      "template_name": "",
      "style": "",
      "aspect_ratio": "16:9",
      "duration": 5,
      "extended": 1,
      "last_frame": "",
      "seed": 0,
      "asset_id": 0,
      "asset_name": ""
    }
  ]
}
```

It can be seen that the result content is consistent with the above text, which also realizes the function of video extension generation.


## More

For more info, please check below APIs and integration documents.

| API | Path | Integration Guidance |
| ---- | ---- | ------------ |
| [Pixverse Video Generation API Integration Guide](http://platform.acedata.cloud/documents/00f200b3-709d-4783-ac56-3d27cc70b73d) | `/pixverse/videos` | [Pixverse Video Generation API Integration Guide](http://platform.acedata.cloud/documents/a5c7bf5a-18bf-4943-becc-cfe1356f90ec) |
| [Pixverse Tasks API](http://platform.acedata.cloud/documents/94d98778-9a98-4e27-bd68-e018a34fae11) | `/pixverse/tasks` | [Pixverse Tasks API Integration Guide](http://platform.acedata.cloud/documents/0ee1c397-2d5f-4a70-ae0f-4a49195dfe20) |
| [Pixverse Character API](http://platform.acedata.cloud/documents/32f3dd45-7000-49c2-a38e-285bd02ae334) | `/pixverse/character` | [Pixverse Character API Integration Guide](http://platform.acedata.cloud/documents/423a57f0-eed7-4539-8815-37411b9b43ae) |

Base URL: [https://api.acedata.cloud](https://api.acedata.cloud)

## Support

If you meet any issue, check our from [support info](https://platform.acedata.cloud/support).