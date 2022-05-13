This is just a slight change to [strapi-provider-upload-aws-s3](https://www.npmjs.com/package/strapi-provider-upload-aws-s3)

package.json:

```
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
    provider: 'aws-s3-cloudfront',
    providerOptions: {
      accessKeyId: env('AWS_S3_KEY'),
      secretAccessKey: env('AWS_S3_SECRET'),
      region: env('AWS_S3_REGION'),
      params: {
        Bucket: env('AWS_S3_BUCKET'),
      },
      cdn: env('AWS_CLOUDFRONT'),
      ACL: "public-read"  // OPTIONAL: if files are distributed via CDN, S3 bucket should be private, this field should be left empty.     
    },
  },
  //...
};
```