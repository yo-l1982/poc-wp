# POC WP
Wordpress in docker POC with IAC and CI/CD pipeline using AWS.

## Local dev environment

## CI/CD Pipeline
### git web hooks
If you already have a access token for previous AWS codpipelines you can reuse it in this pipeline and you can skip the below steps.  
In order to get cloudformation to set up the webhook between the pipeline and git you will need an accesss key from the github and provide it to cloudformation.  

#### Create access token
https://docs.aws.amazon.com/codepipeline/latest/userguide/GitHub-create-personal-token-CLI.html  
  
* In Github click you profile picture and chose `Settings`.
* Select `Developer settings` in the meny and then `Personal access tokens`.
* Generate new token.
* Leave a note with something related ex. `AWS Codepipeline token`.
* Under `Select scopes`, select `admin:repo_hook` and `repo`.
* Select `Generate token` and save it for later use in `AWS Secrets manager`. 

#### Add token to AWS Secrets Manager
Place this token in AWS Secrets manager.  
* Go to AWS Secrets Manager and select `Secrets` in the menu.
* Select `Store new Secret`.
* Choose `Other type of secrets`.
* Add the token with the key name `CodepipelineGithubAccessToken`. This keyname should match the key specified in the CFN template located in `cloudformation/pipeline/cfn-stack.yaml`.


