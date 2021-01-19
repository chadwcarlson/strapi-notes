# strapi-notes

- [0. Summary](#0-summary)
- [1. Deploy on Platform.sh](#1-deploy-on-platformsh)
- [2. Branch](#2-branch)
- [3. Create content type (in admin UI) and it's fields](#3-create-content-type-in-admin-ui-and-its-fields)
- [4. Permissions](#4-permissions)
- [5. Test](#5-test)
- [6. What happened?](#6-what-happened)
   - [`config`](#config)
   - [`controller`](#controller)
   - [`documentation`](#documentation)
   - [`models`](#models)
   - [`services`](#services)
- [7. What this means for merging](#7-what-this-means-for-merging)

## 0. Summary

- Strapi has two running modes, `production` and `development`.
- Our template is configured to run in `production` mode on Master, and in `development` on non-production environments.
- Strapi does not allow the creation of new Content Types (or Collections) in `production`, only in `development`.
- Strapi API endpoints are defined in an `api` subdirectory (included in the template). The admin UI allows you to create new content types (in `development`) at runtime, so `api` is defined as a mount for the template.
- Merging Content Types isn't possible, since Content Type data is written to the `api` mount, and pieces of Content written to the database. 
- Merging a tested Content Type into production means *reproducing* the API code written to `api` at runtime locally and committing that to the repo. Pieces of content data will still need to be added to the production database. 

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

```txt
# app/api/article
.
└── article
    ├── config
    │   └── routes.json
    ├── controllers
    │   └── article.js
    ├── documentation
    │   └── 1.0.0
    │       ├── article.json
    │       └── overrides
    ├── models
    │   ├── article.js
    │   └── article.settings.json
    └── services
        └── article.js
```

### `config`

```json
# config/routes.json
{
  "routes": [
    {
      "method": "GET",
      "path": "/articles",
      "handler": "article.find",
      "config": {
        "policies": []
      }
    },
    {
      "method": "GET",
      "path": "/articles/count",
      "handler": "article.count",
      "config": {
        "policies": []
      }
    },
    {
      "method": "GET",
      "path": "/articles/:id",
      "handler": "article.findOne",
      "config": {
        "policies": []
      }
    },
    {
      "method": "POST",
      "path": "/articles",
      "handler": "article.create",
      "config": {
        "policies": []
      }
    },
    {
      "method": "PUT",
      "path": "/articles/:id",
      "handler": "article.update",
      "config": {
        "policies": []
      }
    },
    {
      "method": "DELETE",
      "path": "/articles/:id",
      "handler": "article.delete",
      "config": {
        "policies": []
      }
    }
  ]
}
```

### `controller`

```js
# controller/article.js
'use strict';

/**
 * Read the documentation (https://strapi.io/documentation/developer-docs/latest/concepts/controllers.html#core-controllers)
 * to customize this controller
 */

module.exports = {};
```

### `documentation`

An OpenAPI specification is created for the `articles` content type. An `overrides` subdirectory is also included (to override meta information, such as linked site, author, etc.).

### `models`

```js
# article.js
'use strict';

/**
 * Read the documentation (https://strapi.io/documentation/developer-docs/latest/concepts/models.html#lifecycle-hooks)
 * to customize this model
 */

module.exports = {};
```

```json
# article.settings.json
{
  "kind": "collectionType",
  "collectionName": "articles",
  "info": {
    "name": "article"
  },
  "options": {
    "increments": true,
    "timestamps": true,
    "draftAndPublish": true
  },
  "attributes": {
    "title": {
      "type": "string",
      "required": true
    },
    "content": {
      "type": "richtext",
      "required": true
    },
    "image": {
      "model": "file",
      "via": "related",
      "allowedTypes": [
        "files",
        "images",
        "videos"
      ],
      "plugin": "upload",
      "required": true
    },
    "published_date": {
      "type": "date",
      "required": true
    }
  }
}
```

### `services`

```js
# article.js
'use strict';

/**
 * Read the documentation (https://strapi.io/documentation/developer-docs/latest/concepts/services.html#core-services)
 * to customize this service
 */

module.exports = {};
```

## 7. What this means for merging

> **Recap:**
> - Content Types are written (from the admin UI) to named subdirectories on the mount `api` at runtime. This data is not merged into `master` on merges. Requesting `articles` on master post-merge will give the response `Not Found`.
> - Once a Content Type is created, pieces of content data for that type are stored in the database (PostgreSQL in the template).
> - Similar things will also be the case for defining Webhooks and custom components.

So, in general, any data edited through the admin UI at runtime on a development branch will not end up in master. It will write to the current `api` mount on that environment, and to the current database. That means, if you actually want to merge a new Content Type, you will need to download the mount. 

```bash
$ platform mount:download -p <Project ID> -e <Env name> --mount api --target api
```

[In our template](https://github.com/platformsh-templates/strapi), the `api` subdirectory is already committed, so the `article` content type data will be added in the right place in the repository within `api`:

```text
.
├── .editorconfig
├── .env.example
├── .eslintignore
├── .eslintrc
├── .git
├── .gitignore
├── .platform
│   ├── routes.yaml
│   └── services.yaml
├── .platform.app.yaml
├── README.md
├── api
│   └── article
├── config
│   ├── database.js
│   ├── functions
│   └── server.js
├── extensions
│   ├── .gitkeep
│   └── documentation
├── favicon.ico
├── node_modules
├── package-lock.json
├── package.json
├── public
│   ├── robots.txt
│   └── uploads
└── yarn.lock
```

In the template's `.platform.app.yaml`, we have the copy-paste juggle already for mounts, which will place our now committed `articles` content type into the mount.

```yaml
hooks:
    build: |
        # Download dependencies and build Strapi.
        yarn
        yarn build
        # Local development will commit changes to subdirectories that will become mounts on
        # Platform.sh and overwritten during deployments. To prevent that, set aside during builds.    
        if [ -n "$(ls -A api)" ]; then
            mkdir api-tmp && mv api/* api-tmp
        fi
    deploy: |
        # Copy overrides back to where they need to be.   
        if [ -n "$(ls -A api-tmp)" ]; then
            cp -r api-tmp/* api
        fi
```

So, we can commit our `api/articles` subdirectory, push and then merge.

```bash
$ git add . && git commit -m "Commit article Content Type." && git push origin updates
...
$ platform merge master
```

Now if we request `/articles` on Master, we get 

```
{"statusCode":403,"error":"Forbidden","message":"Forbidden"}
```

So we have the `/articles` Content Type, but:

- There are no published Articles in that Content Type
- Permissions are still locked for public requests

We can then follow the previous steps to:

- Add an Article
- Publish that article
- Enable Public permissions for `find` and `findone` on the `/articles` endpoint

If we just enable public permissions without adding content, the response becomes empty:

```
[]
```

Add and publish an article on Master, and you'll be all set with the same article on your production instance.
