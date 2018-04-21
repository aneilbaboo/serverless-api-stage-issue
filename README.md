This repo illustrates a problem when both the `serverless-domain-manager` and `serverless-api-stage` plugins are used at the same time.

This is a stripped down version of a serverless configuration which is for deploying different stages to different subdomains of a URL. E.g., something like `STAGE=foo sls deploy` will get deployed to `foo.yourdomain.com`.

# the problem
Deployment fails with:
```shell
...
Serverless: Uploading CloudFormation file to S3...
Serverless: Uploading artifacts...
Serverless: Uploading service .zip file to S3 (15.76 MB)...
Serverless: Validating template...
Serverless: Updating Stack...
Serverless: Checking Stack update progress...
..........................................
Serverless: Operation failed!

  Serverless Error ---------------------------------------

  An error occurred: pathmapping - Invalid stage identifier specified.

  Get Support --------------------------------------------
     Docs:          docs.serverless.com
     Bugs:          github.com/serverless/serverless/issues
     Forums:        forum.serverless.com
     Chat:          gitter.im/serverless/serverless

  Your Environment Information -----------------------------
     OS:                     darwin
     Node Version:           9.3.0
     Serverless Version:     1.26.1
```

To replicate the problem,

1. Make sure you have a Route53 domain provisioned

2. Install packages
```shell
yarn install
```

3. Attempt deploy
```shell
STAGE=xyzzy DOMAIN={your-domain-here} node_modules/.bin/sls deploy
```

You should receive the error: "pathmapping - Invalid stage identifier specified."