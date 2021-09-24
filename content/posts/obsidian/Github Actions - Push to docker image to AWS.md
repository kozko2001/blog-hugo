
---
title: Github Actions - Push to docker image to AWS
date: 2021-09-24 00:00:00
---
---

We all know the benefits of pushing code automatically to production, here is a small guide on how to do it with Github actions and AWS.

The high level steps are:

1. Create a docker image repository in AWS ( ECR )
2. Create a single user in AWS that only has permissions to add images to the ECR
3. Configure login of the pipeline into AWS
4. Configure the pipeline to do the push


### Step 1 - Create a docker image repository

For use of all this code, we are going to use `AWS-CDK` a library to create infrastructure from our code.

to install `cdk ` we need to have npm:
- `npm install -g cdk`
- `cd my-project`
- `cdk init --language python`
- `source .venv/bin/activate` 

with that done, you should have now a `my_project_stack.py` file in our file system, here is where we define our infrastructure.

we should add :
```python
repository = ecr.Repository(self, "name-of-the-registry")
```

then in the terminal we execute `cdk deploy`, and voila! we have a new ecr repository in our AWS account.

### Step 2 - Create user to push to registry

we should create a new aws user...
```python
user = iam.User(self, "MY_PROJECT_GITHUB_ACTIONS_PUSH_ECR")
```

and give it permission to read and write to the repository...

```python
repository.add_to_resource_policy(
	iam.PolicyStatement(
		effect=iam.Effect.ALLOW,
		actions=[
			"ecr:GetAuthorizationToken",
			"ecr:BatchCheckLayerAvailability",
			"ecr:GetDownloadUrlForLayer",
			"ecr:GetRepositoryPolicy",
			"ecr:DescribeRepositories",
			"ecr:ListImages",
			"ecr:DescribeImages",
			"ecr:BatchGetImage",
			"ecr:GetLifecyclePolicy",
			"ecr:GetLifecyclePolicyPreview",
			"ecr:ListTagsForResource",
			"ecr:DescribeImageScanFindings",
			"ecr:InitiateLayerUpload",
			"ecr:UploadLayerPart",
			"ecr:CompleteLayerUpload",
			"ecr:PutImage",
		],
		principals=[user],
	)
)
```

execute `cdk deploy`, and we should have the correct user with the correct permissions

### Step 3 - Configure github actions

First, we need  to make be able to use this user from the API, for that we need to:

1. Login into the aws console.
2. Go to the IAM page (where the users are defined).
3. Go to the details of the user we created
4. Select the tab `Security Credentials`
5. Create and access key, write it down somewhere the `access key` and the `access_secret`

now in our github project, we must setup 2 secrets.
1. `AWS_ACCESS_KEY_ID` with the access key
2. `AWS_SECRET_ACCESS_KEY`with the secret

And now we can add the github workflow in our codebase.

create a file in `.github/workflow/publish-docker.yml` with the following content:

```yaml
name: Publish docker image
  on:
    push:
      branches: main
jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v1
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: eu-west-1
    - name: Login to Amazon ECR
      id: login-ecr
      uses: aws-actions/amazon-ecr-login@v1
```

be aware of changing the `aws-region` and the `main` branch if not suits your project.

after you do a push, you should see in the Actions tab of your github project, that the pipeline is executed and is green.

### Step4 - Configure the pipeline to  push!

Once you are logged in AWS inside the pipeline, most of the heavy lifting is already done. 
Now we just want to create a new step in the pipeline that builds the image and pushes to the ECR.

```
    - name: Build, tag, and push the image to Amazon ECR
      id: build-image
      env:
        ECR_REGISTRY: ${{ steps.login-ecr.outputs.registry }}
        ECR_REPOSITORY: ${{ secrets.REPO_NAME }}
        IMAGE_TAG: latest
      run: |
        # Build a docker container and push it to ECR
        docker build -t $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG .
        echo "Pushing image to ECR..."
        docker push $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG
        echo "::set-output name=image::$ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG"
```

Before you push, make sure to create a new secret named `REPO_NAME` with the URI of the ECR repository (is one of the properties you see in the AWS console)


### Conclusions

Having best practices is a little bit more hard, than doing manually. But 

1. You don't depend on specific computer setup to do it
2. It's a piece of cognitive load that we don't have to think about anymore, you push your code and gets deployed.

And now with Github Actions, it's free and managed for us.