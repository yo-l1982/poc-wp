# POC WP
Wordpress in docker POC with IAC and CI/CD pipeline using AWS.

## Local dev environment

## CI/CD Pipeline
### Git web hooks
If you already have a access token for previous AWS codpipelines you can reuse it in this pipeline and you can skip the below steps.  
In order to get cloudformation to set up the webhook between the pipeline and git you will need an accesss key from the github and provide it to cloudformation.  

#### Create git access token
From [https://docs.aws.amazon.com/codepipeline/latest/userguide/GitHub-create-personal-token-CLI.html](AWS documentation)
  
* In Github click you profile picture and chose `Settings`.
* Select `Developer settings` in the meny and then `Personal access tokens`.
* Generate new token.
* Leave a note with something related e.g. `AWS Codepipeline token`.
* Under `Select scopes`, select `admin:repo_hook` and `repo`.
* Select `Generate token` and save it for later use in `AWS Secrets manager`. 

#### Add token to AWS Secrets Manager
Place the github token in AWS Secrets manager.  
The key name and secret name should match the [Dynamic reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/dynamic-references.html) string in  
`cloudformation/pipeline/cfn-stack.yaml` e.g. {{resolve:secretsmanager:**CodepipelineGithubAccessToken**:SecretString:**token**}}  
* Go to AWS Secrets Manager and select `Secrets` in the menu.
* Select `Store new Secret`.
* Choose `Other type of secrets`.
* Add the generated token with the key name `token`, then choose `Next`.
* Give the `Secret name` `CodepipelineGithubAccessToken`, leave a tag `Billing` with value `shared` for billing cost management and a description eg. `Git hub access token for Codepipelines`, then choose `Next`.
* Choose `Next` to skip rotation.
* Review and choose `store`to save the token.

