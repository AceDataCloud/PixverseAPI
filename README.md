# Pixverse Video Generation API

This service has implemented the integration of Pixverse AI, which can be used to generate videos and other content.

API home page: [Ace Data Cloud - Pixverse Video Generation](https://platform.acedata.cloud/services/74e74695-ceff-49d1-ac84-cfa876225ae8)

## Get Started


This article will introduce the integration instructions for the Pixverse Videos Generation API, which can generate official Pixverse videos by inputting custom parameters.

### Application and Usage

To use the Pixverse Videos Generation API, you can first visit the [Pixverse Videos Generation API](https://platform.acedata.cloud/documents/00f200b3-709d-4783-ac56-3d27cc70b73d) page and click the "Acquire" button to obtain the credentials needed for the request:

![](https://cdn.acedata.cloud/nyq0xz.png)

If you are not logged in or registered, you will be automatically redirected to the login page inviting you to register and log in. After logging in or registering, you will be automatically returned to the current page.

Upon your first application, there will be a free quota provided, allowing you to use the API for free.

### Basic Usage

You can generate videos based on prompts, for example, you can input `quiver`, as shown in the image:

<p><img src="https://cdn.acedata.cloud/azz8d3.png" width="500" class="m-auto"></p>

The generated code is as follows:

<p><img src="https://cdn.acedata.cloud/g5j3f2.png" width="500" class="m-auto"></p>

You can click the "Try" button to directly test the API, and after waiting for 1-2 minutes, the result is as follows:

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

At this point, we have obtained the content of a video, including video ID, video link, video resolution, video duration, and other details.

The field descriptions are as follows:

- success: Indicates whether the generation was successful; if successful, it is `true`, otherwise it is `false`.
- task_id: The ID of this generation task.
- trace_id: The tracking ID of this generation task.
- data: A list containing detailed information about the generated video.
  - id: The unique ID of the generated video, which can be used for further generation.
  - first_frame: The link to the first frame image of the video.
  - last_frame: The link to the last frame image of the video.
  - video_width: The width of the resulting video.
  - video_height: The height of the resulting video.
  - prompt: The prompt for this video generation task.
  - model: The model used for this video generation task.
  - video_url: The link to the video generated in this task.
  - template_id: The ID of the template effect used in the video.
  - template_name: The name of the template effect used in the video.
  - asset_id: The ID of the character used in the video.
  - asset_name: The name of the character used in the video.
  - style: The style of this video generation task.
  - aspect_ratio: The size ratio of this video.
  - extended: Indicates whether this video is an extended generation; 0 means it is not an extended generation, otherwise it is an extended generation.

### Custom First and Last Frame Video Generation

If you want to customize the first and last frames for video generation, you can input the links to the first and last frame images:

At this point, the `frame` field can accept content like the following:

- First frame image
  <p><img src="https://cdn.acedata.cloud/c7zzmb.png" width="500" class="m-auto"></p>
- Last frame image
  <p><img src="https://cdn.acedata.cloud/fqd8br.png" width="500" class="m-auto"></p>

Next, we need to customize the song generation based on lyrics, title, and style, specifying the following content:

- action: The action for this video generation task, which can be either generate video `action` or extend video `extend`.
- prompt: The prompt for this video generation task.
- frame: An array of links to the first and last frame images for this video generation.

An example of the input is as follows:

<p><img src="https://cdn.acedata.cloud/4ea6pa.png" width="500" class="m-auto"></p>

After filling it out, the generated code is as follows:

<p><img src="https://cdn.acedata.cloud/yfzxxn.png" width="500" class="m-auto"></p>

The corresponding Shell code:

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


## More

For more info, please check below APIs and integration documents

| API | Path | Integration Document |
| ---- | ---- | ------------ |
| [Pixverse Video Generation API Integration Guide](http://platform.acedata.cloud/documents/00f200b3-709d-4783-ac56-3d27cc70b73d) | `/pixverse/videos` | [Pixverse Video Generation API Integration Guide](http://platform.acedata.cloud/documents/a5c7bf5a-18bf-4943-becc-cfe1356f90ec) |
| [Pixverse Tasks API](http://platform.acedata.cloud/documents/94d98778-9a98-4e27-bd68-e018a34fae11) | `/pixverse/tasks` | [Pixverse Tasks API Integration Guide](http://platform.acedata.cloud/documents/0ee1c397-2d5f-4a70-ae0f-4a49195dfe20) |
| [Pixverse Character API](http://platform.acedata.cloud/documents/32f3dd45-7000-49c2-a38e-285bd02ae334) | `/pixverse/character` | [Pixverse Character API Integration Guide](http://platform.acedata.cloud/documents/423a57f0-eed7-4539-8815-37411b9b43ae) |

Base URL: [https://api.acedata.cloud](https://api.acedata.cloud)

## Support 

If you meet any issue, check our from [support info](https://platform.acedata.cloud/support).