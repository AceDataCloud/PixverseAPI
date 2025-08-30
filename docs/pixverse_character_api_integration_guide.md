# Pixverse Create Character ID API Integration Instructions

Pixverse allows us to upload reference images to set up characters, and then generate videos based on this character ID. This document explains the integration method for the relevant API.

The API has only one input parameter, which is `images`, a publicly accessible CDN image URL. This document will introduce the following character image as an example:

<p><img src="https://cdn.acedata.cloud/8bai0n.png" width="500" class="m-auto"></p>

Here, the `images` we input is `https://cdn.acedata.cloud/8bai0n.png`, which is a publicly accessible CDN address.

```bash
curl -X POST 'https://api.acedata.cloud/pixverse/character' \
-H 'accept: application/json' \
-H 'authorization: Bearer {token}' \
-H 'content-type: application/json' \
-d '{
  "images": ["https://cdn.acedata.cloud/8bai0n.png"]
}'
```

The result is as follows:

```
{
  "success": true,
  "task_id": "5b9c0493-0033-431b-a799-fb5e04b4ae19",
  "data": {
    "asset_id": 317383895242880
  }
}
```

As we can see, the `asset_id` field in `data` is the character ID after uploading the reference image.

With the character ID, we can use the [Pixverse Videos Generation API](https://platform.acedata.cloud/documents/00f200b3-709d-4783-ac56-3d27cc70b73d) to generate custom videos. For example, if we pass `action` as `generate` and `asset_id` as the returned character ID, we can generate a new video based on the character ID.