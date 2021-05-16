# Tech stack for CICD (Coninous Integration & Continuous Delivery)
- [x] Code
- [x] Build
- [x] Test
- [x] Deploy
- [x] Provision

# CodeCommit
A Managed version control (just like GitHub)
## Characteristic
- Follows the same command as git.
  - Just paste your SSH keys to the `SSH Keys For AWS CodeCommit` pannel in IAM user tab.
- Private repos
- No size limit
- Scalable
- AWS security benefits
- No restriction over integration with other third-parties (like Jenkins, CodeBuild).
- Managed & Hosted by AWS.

## Security
- Authentication
  - SSH
  - HTTPS
    - Use API's using AWS CLI authentication helper 
    - Or
  - There is a IAM user tab in which there is a panel to download git credentials.
  - MFA
- Authorization
  - IAM policies manage role/user rights to repository
- Encryptuon
  - By Default, at rest encryption using KMS
  - In-Flight using HTTPS or SSH
- Cross Account Access
  - Using IAM role & AWS STS (with AsssumeRole API)

## Notification
For nitification we can use
- AWS SNS
- AWS Lambda function
- AWS CloudWatch Event Rules - More focues on PR's & comments on commits
  - CloudWatch event goes into SNS topic
### Use Cases
- Deletion of branch
- Pushes that happens in master branch
- Using Lambda functions as a hook to trigger functions (Like code analysis).
- Trigger for PR's (CRUD)
- For comment on commits

# CodePipeline
Pipelines is a set of instructions to commit, build, test, deploy & provision your code. Pielines are made of stages. (Stages can be sequential or parallel).
## Workflow (Rough idea - It is rather more complicated underneath)
The pipeline stages create outputs (called artifacts - in AWS term) & store them in S3. On next stage, it pulls the previous build output & store its output S3 again & so on untill the last stage
## Characteristic
- Visual workflow
- Source Can be : Github/CodeCommit/S3
- Build Can be: CodeBuild/Jenkins etc
- Deploy Can be: AWS CodeDeploy/BeanStalk/CloudFormation/ECS etc
## Points to be noted
- Each build stage generate a cloudWatch Event (You see what I'm implying here - Using SNS notification to have an update).
- If CodePipeline fails a stage, it shows that output in console.
- AWS CloudTrail is also there.
- Make Sure `IAM Service Role` attached has enough permissions(Reason for - Failed to perform action in any build).
  
> Note: Action group go within stages (There can be multiple action within a stage).

# CodeBuild
Building & Testing the application (Kind of dockerfile)
## Characteristic
- Fully managed service.
- Pay per use
- Leverages docker under the hood (So possiblity to use custom extended docker images.)
- Source Code can be: GitHub/CodeCommit/CodePipeline/S3.
- Output logs to S3 & AWS CloudWatch.
- File to write instruction for build is called `buildspec.yaml`.
- Metrics to monitor statistics.
- Ability to reproduce codebuild locally for further troubleshooting.
- Build can be defined in CodePipeline or CodeBuild itself.
- S3 can be used to cache build artificats or dependencies of your application.
## BuildSpec
- Location - Root
- Env Variables
  - Plain Text Variables
  - Secure Secrets: Using SSM parameter store.
- Phases (Sequential processing)
  - Install
  - Pre Build
  - Build
  - Post Build
- Can set Timeout & Queue Timeout(For how much time it can stay in queue). `Min = 5 min` | `Max = 8 hrs`
> Note: By Default CodeBuild containers are launched outside the VPC & containers get terminated after doing build test.

# CodeDeploy
Each Ec2 instances runs an CodeDeploy agent which continuously poll for CodeDeploy to get notified of the changes.<br>
Makes use of `appspec.yaml`
## AppSec
- Location - Root
- Hooks (Phase) 
  - ApplicationStop
  - DownloadBundle
  - BeforeInstall
  - AfterInstall
  - ApplicationStart
  - ValidateService
