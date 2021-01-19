# strapi-notes

## 1. Deploy on Platform.sh

After deploying the template, you will get a *production* instance of Strapi on the `master` environment. In production, you *cannot* create Content Types/Collections through the admin panel. You will need to create your admin user at this point. 

## 2. Branch

On a new environment updates, we can create a new Content Type called "Articles", that will be available at `/articles`.

## 3. Create content type (in admin UI) and it's fields

- Display name: `article`
   - (Short text) `title`, Required
   - (Rich text) `content`, Required
   - (Single Media) `image`, Required
   - (Date) `published_date`, Required
   
Save (restarts the server), and then add an article to the type.
   
## 4. Permissions

New content types are restricted to the public by default. In Settings/Roles/Public, enable `find`, and `findone` for Article. Save and restart the server. 

## 5. Test

Now you can test the endpoint `/articles`:

```json
# https://www.update-fe3qcpy-gokaumanzz7p6.eu-3.platformsh.site/articles
[
  {
    "id": 1,
    "title": "Test article",
    "content": "\nLorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam ut rhoncus nisi. Fusce mattis venenatis nulla ut cursus. Fusce ac arcu vel est luctus consectetur vitae at urna. Sed quis vestibulum dolor. Ut ut rutrum enim. Suspendisse nec aliquam enim. Praesent orci justo, pulvinar at venenatis nec, ultricies non urna.\n\nDonec rutrum nunc et ex pulvinar egestas. Pellentesque faucibus auctor est, et dictum est consectetur ut. Etiam id nunc dolor. In congue dolor vitae erat blandit, id pretium ligula blandit. Donec eget sapien ac turpis placerat luctus nec at leo. Nullam nunc odio, efficitur nec semper nec, pulvinar quis mauris. Phasellus sodales mattis massa at consectetur. Suspendisse malesuada lectus quis risus convallis, non ullamcorper massa commodo. Phasellus vel metus gravida, ornare purus a, varius metus. Curabitur id iaculis dolor.",
    "published_date": "2021-01-19",
    "published_at": "2021-01-19T15:19:09.048Z",
    "created_at": "2021-01-19T15:18:44.704Z",
    "updated_at": "2021-01-19T15:19:09.109Z",
    "image": {
      "id": 1,
      "name": "jimmy-dean-HmbLYd8-62I-unsplash.jpg",
      "alternativeText": "",
      "caption": "",
      "width": 6720,
      "height": 4480,
      "formats": {
        "large": {
          "ext": ".jpg",
          "url": "/uploads/large_jimmy_dean_Hmb_L_Yd8_62_I_unsplash_51b53ec8f3.jpg",
          "hash": "large_jimmy_dean_Hmb_L_Yd8_62_I_unsplash_51b53ec8f3",
          "mime": "image/jpeg",
          "name": "large_jimmy-dean-HmbLYd8-62I-unsplash.jpg",
          "path": null,
          "size": 76.64,
          "width": 1000,
          "height": 667
        },
        "small": {
          "ext": ".jpg",
          "url": "/uploads/small_jimmy_dean_Hmb_L_Yd8_62_I_unsplash_51b53ec8f3.jpg",
          "hash": "small_jimmy_dean_Hmb_L_Yd8_62_I_unsplash_51b53ec8f3",
          "mime": "image/jpeg",
          "name": "small_jimmy-dean-HmbLYd8-62I-unsplash.jpg",
          "path": null,
          "size": 27.67,
          "width": 500,
          "height": 333
        },
        "medium": {
          "ext": ".jpg",
          "url": "/uploads/medium_jimmy_dean_Hmb_L_Yd8_62_I_unsplash_51b53ec8f3.jpg",
          "hash": "medium_jimmy_dean_Hmb_L_Yd8_62_I_unsplash_51b53ec8f3",
          "mime": "image/jpeg",
          "name": "medium_jimmy-dean-HmbLYd8-62I-unsplash.jpg",
          "path": null,
          "size": 49.34,
          "width": 750,
          "height": 500
        },
        "thumbnail": {
          "ext": ".jpg",
          "url": "/uploads/thumbnail_jimmy_dean_Hmb_L_Yd8_62_I_unsplash_51b53ec8f3.jpg",
          "hash": "thumbnail_jimmy_dean_Hmb_L_Yd8_62_I_unsplash_51b53ec8f3",
          "mime": "image/jpeg",
          "name": "thumbnail_jimmy-dean-HmbLYd8-62I-unsplash.jpg",
          "path": null,
          "size": 8.83,
          "width": 234,
          "height": 156
        }
      },
      "hash": "jimmy_dean_Hmb_L_Yd8_62_I_unsplash_51b53ec8f3",
      "ext": ".jpg",
      "mime": "image/jpeg",
      "size": 3571.07,
      "url": "/uploads/jimmy_dean_Hmb_L_Yd8_62_I_unsplash_51b53ec8f3.jpg",
      "previewUrl": null,
      "provider": "local",
      "provider_metadata": null,
      "created_at": "2021-01-19T15:18:40.074Z",
      "updated_at": "2021-01-19T15:18:40.107Z"
    }
  }
]
```

As well as the single article endpoint using its id (1), `/articles/1`.

## 6. What happened?

When editing through the admin UI, Strapi writes a few files to the `api` mount in the container to define the new endpoint in a new folder `article`.

```
# app/api/article
config/
   routes.json
controllers/
   article.js
documentation/
   1.0.0/
      article.json
      overrides/
models
   article.js
   article.settings.json
services
    article.js
```
