This is just a slight change to [strapi-provider-upload-aws-s3](https://www.npmjs.com/package/strapi-provider-upload-aws-s3)

package.json:

```json
{
  ...

  "dependencies": {
    "strapi-provider-upload-aws-s3-cloudfront": "3.6.4"
  }

  ...

}
```

config/plugins.js:

```js
module.exports = ({ env }) => {
  //...
  upload: {
    provider: 'strapi-provider-upload-aws-s3-cloudfront',
    providerOptions: {
      accessKeyId: env('AWS_S3_KEY'),
      secretAccessKey: env('AWS_S3_SECRET'),
      region: env('AWS_S3_REGION'),
      params: {
        Bucket: env('AWS_S3_BUCKET'),
      },
      // Fully qualified URL with trailing backslash:
      cdn: env('AWS_CLOUDFRONT') // eg: "https://abc123tuvwxyz.cloudfront.net/"
    },
  },
  //...
};
```

config/middlewares.js:

```js
module.exports = [
  {
    name: "strapi::security",
    config: {
      contentSecurityPolicy: {
        useDefaults: true,
        directives: {
          "connect-src": ["'self'", "https:"],
          "img-src": [
            "'self'",
            "data:",
            "blob:",
            "abc123tuvwxyz.cloudfront.net", // Enter your cloudfront domain here
          ],
          "media-src": [
            "'self'",
            "data:",
            "blob:",
            "abc123tuvwxyz.cloudfront.net", // Enter your cloudfront domain here
          ],
          upgradeInsecureRequests: null,
        },
      },
    },
  },
  "strapi::errors",
];
```