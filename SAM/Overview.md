Server Application Model
A framework for developing & deploying serverless applications

# Characteristic
- The Configuration is a YAML code
- Can generate complex CloudFormation from simple SAM YAML file.
- Supports anything from CloudFormation: Outputs, Mappings, Parameters etc.
- Only 2 commands are needed to deploy to AWS.
    - aws cloudformation package / sam package
    - aws cloudformation deploy / sam deploy
- Can use CodeDeploy to deploy Lambda functions
- Can help u run Lambda, API Gateway. DynamoDB locally

# Pints to Remember
- Transform: 'AWS::Serverless-2016-10-31'

# Write Code Using
- AWS::Serverless::Function
- AWS::Serverless::Api
- AWS::Serverless::SimpleTable
