A way for you to define the infrastructure for your application through code(basically YAML & JSON file).
You can assign ec2 instance,security-groups & soon.., change their configuration & much more.

# Benefits
- We can use the same template with a little bit of tweak if we wants it again.(Saves lot of time).
- Declarative programming.(Don't have to worry about ordering & filtering).
- You can have separate file for each stack.(So its not a tightly coupled system).
    - EC2 stack
    - VPC stack
- Deleting a stack delete all the instrastructure attached to it.
- Rollback: Rolling back to previous working version in case of failure.
- Ability to troubleshot with the help of logs

# Working
- We have to store template first in S3. Then reference it in CloudFormation.
- We can keep different version of template.
> Note: To make changes new version must be deployed(Updating existing one won't do).

# Deployment
## Manual
    - Using console (CloudFormation Designer tool)
## Automated
    - Using YAML file to edit cofigs & deploy it using CLI

# Template Component
## Resource
E.g Ec2, ELB, VPC
### Characteristic
- They can reference each other in the template
- Around 224 types
- Resource Type Identified -> `AWS::aws-product-name::data-type-name` (E.g `AWS::EC2::Instance`)
## Parameters
Way to provide inputs to your templates. Its just like declaring a variable for your function.
### Characteristic
- Can be dynamic (E.g providing key-pair)
- Have multiple types (String, Number, List etc)
- Can put constraints
- Can ref another Resource using `key: !Ref anotherKeyId` (You will understand in second when u will look at any sample template).
e.g
```
Parameters:
    SecurityGroupDescription
        Description: Security Group Description Bla Bla
        Type: String
```
### Pseduo Parameters
They are some key:value(E.g `AWS::AccountId:1234567890` will refer to a pseudo account) pair which are already there for us. We can use these for mock testing kind of stuff
## Mapping
They are kind of static variables & can be different for the different environment (e.g. dev, prod, staging). Its just like chosing your env variables based on your environment type
If you are familiar with F.E this is like `sass`.
### Characteristic
- Quite Handy
- Uses `!FindInMap [MapName, TopLevelKey, SecondLevelKey]` to locate value for a key
e.g
```
Mappings:
    RegionMap:
        'ap-south-1': 
            '32': 'amiId1'
            '64': 'amiId2'
        'ap-south-2':
            '32': 'amiId1'
            '64': 'amiId2'
Resource:
    MyEC2:
        Properties:
            ImageId: !FindInMap [RegionMap, 'ap-south-1', 64]
```
## Output
Outputs allows us the export of our one component into another template.
E.g We can output the resultant id of the vpc we created in our template & import it in
other template.
```
Outputs:
    StackMyVPC:
        Description: 'Mera VPC'
        Value: !Ref MyAnotherVPC (Use of Ref)
        Export:
            Name: CanBeExportedVPC
```
```
Resource: 
    MyInstance:
        Type: AWS::EC2::Instance
        Properties:
            ImageId: 'BLABLA'
            VPC:
                - !ImportValue CanBeExportedVPC
```
### Characteristic
- Optional
- Can be viewed in console or CLI
- Uses `!ImportValue ExportedName` to locate value
> Note: You can't delete template if its component is being referenced in other template
> Note: The exported output name must be unique in the region.
## Conditional
Using conditionals statement in template for Resource, Condition & Output.
E.g the below statment set CreateProdResource to true if EnvType === Prod
```
Parameters:
    EnvType: 'prod'
Conditions:
    CreateProdResources: !Equals [!Ref EnvType, prod]
```
Use of Condition - We mount volume only if `CreateProdResources` is true
```
Resources:
    MountPoint:
        Type: 'AWS::EC2::VolumeAttachment'
        Condition: CreateProdResources
```
### Characteristic
- Can be used to create env based outputs from your template.
## MetaData
- Some metadata you want to attach to component

# Intrinsic Functions
- Must know list
    - Fn::Ref 
        - Used to Reference 
            - Parameter (Get value of paramter)
            - Resources (Get physical id of the resource)
    - Fn::GetAtt
        - Get attributes of a component
    - Fn::FindInMap
    - Fn::ImportValue
    - Fn::Join
        - Just like a join in String library (JS Ref)
        - E.g !Join [':', [a,b,c]] ->  `a:b:c`
    - Fn::Sub
        - Sub => Subsitute
        - E.g 
            !Sub 
                - String
                - { Var1Name: Var1Value, Var2Name: Var2Value }
            !Sub `String`

    - Condition Functions (Fn::If, Fn::Not, Fn::Equals etc).
- Fn can be shorthanded as `Fn::FunctionName` to `!FunctionName`

# ChageSets
Before deploying the template we can use changeSets to check what really has changed & finally after review can deploy it.

# Nested Stacks
They are just like isolating a common logic into a separate function & use it as many times as you need that logic. So its just using a common behaviral stack in other higher level stack.

# StackSets
When we want to create, update & delete stack across multiple accounts & regions
## Characteristic
- Only administrator can create stack.
- Trust account can use CRUD.
- Update on stackset will happen across every regions & accounts.

# Cloudformation Drift
CloudFormation gives you a feature to check if your template configuration stack has drifted somehow.(Some one might have manually added a new target group to load balancer).