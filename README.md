# readme-template

# INTRODUCTION


Logo Executive is your partner in logo exploration. Our platform boasts a collection of APIs designed to simplify the process of obtaining company logos.
Generate API keys and access logos in various sizes and formats, all while staying in control of your budget. Elevate your brand with Logo Executive!


# How to run this project

git clone https://github.com/TeamShiksha/logoexecutive.git

cd logoexecutive

pnpm install

pnpm start



# Steps to Upload CloudFormation Template and Set Up AWS Cloud

- Make sure you have your own AWS account. If not sign up [here](https://aws.amazon.com/free)
- Download the `cft_dev_test_logoexecutive.yml` file from [here](https://github.com/TeamShiksha/logoexecutive/tree/dev/server/templates)
- Run the commands given below in git bash to generate public and private RSA keys for cloudformation template.

     ```bash
     openssl genrsa -out private_key.pem 2048
     openssl rsa -pubout -in private_key.pem -out public_key.pem
     ```
- The RSA private key in `private_key.pem` can be used for `CLOUD_FRONT_PRIVATE_KEY` in the environmental variables.
- Visit [AWS CloudFormation service](https://ap-southeast-2.console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/getting-started).
- Click on the `Create Stack` button.
- On the Create Stack page, select `Upload a template file`.
- Choose the `cft_dev_test_logoexecutive.yml` file you downloaded earlier, and click on `Next`.

![Specify Stack Details](../images/uploadstack.png)

- Provide a `Stack Name`.
- Inside `CDNPathInS3`, type `assets`. You can also choose other folder names where you want to keep the images.
- Inside `EncodedRSAPublicKey`, paste the public key generated earlier.
- Click on `Next`.

![Specify Stack Options](../images/setparameters.png)

- On the `Review` page, check the checkbox inside the `Capabilities` section.
- Click on `Submit`. You stack will start creating resources now.
- Wait until the stack creation status becomes `CREATE_COMPLETE`.
- Now go to the `Output` section of the stack, and you can find `BUCKET_NAME, BUCKET_REGION, KEY, DISTRIBUTION_DOMAIN and CLOUD_FRONT_KEYPAIR_ID` of the environmental variables seperated by comma(,).
- Go to the `Resources` section of the stack, and click on the `IAMUser` created. This will redirect you to the IAM console of the user created. Under the `Security credentials` section scroll to `Keys` and click `Create access key`.
- Select `Other` under `Access key best practices & alternatives`, and click `Next`.
- Provide `Description tag value` and click `Create access key`. Now you have got two more environmental values for `ACCESS_KEY` and `SECRET_ACCESS_KEY`.
