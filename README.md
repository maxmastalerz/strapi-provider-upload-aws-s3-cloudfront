This is just a slight change to [strapi-provider-upload-aws-s3](https://www.npmjs.com/package/strapi-provider-upload-aws-s3)

package.json:

```
{
  ...

  "dependencies": {
    "strapi-provider-upload-aws-s3-cloudfront": "0.0.1"
  }

  ...

}
```

config/plugins.js:

```
module.exports = ({ env }) => {
  //...
  upload: {
    provider: 'aws-s3-cloudfront',
    providerOptions: {
      accessKeyId: env('AWS_S3_KEY'),
      secretAccessKey: env('AWS_S3_SECRET'),
      region: env('AWS_S3_REGION'),
      params: {
        Bucket: env('AWS_S3_BUCKET'),
      },
      cdn: env('AWS_CLOUDFRONT')
    },
  },
  //...
};
```