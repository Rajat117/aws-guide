A way for you to define the infrastructure for your application through code(basically YAML & JSON file).
You can assign ec2 instance,security-groups & soon.., change their configuration & much more.

# Benefits
- We can use the same template with a little bit of twek if we wanted again.(Saves lot of time).
- Declarative programmin.(Don't have to worry about ordering & filtering).
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
Way to provide inputs to your templates
### Characteristic
- Can be dynamci (E.g providing key-pair)
- Have multiple Type,
- Can put Constrainsts
- Can ref another Resource usin `key: !Ref anotherKeyId` (You will understand in second when u will look at any sample template).
### Pseduo Parameters
They are some key:value(E.g `AWS::AccountId:1234567890` will refer to a pseudo account) pair which are already there for us. We can use these for mock testing kind of stuff
## Mapping
They are kind of static variables & can be differen for the different environment (e.g. dev, prod, staging). Its just like chosing your env variables based on your environment type
If you are familiar with F.E this is like `sass`.
### Characteristic
- Quite Handy
- Uses `!FindInMap [MapName, TopLevelKey, SecondLevelKey]` to locate value for a key
e.g
```
Mappings:
    RegionMap:
        'ap-south-1': 
            '32': 'amiId1',
            '64': 'amiId2'
Resource:
    MyEC2:
        Properties:
            ImageId: !FindInMap [RegionMap, 'ap-south-1', 64]
```
## Output
Outputs allows us the export our one component into another template.
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
> Note: You can't delete template if its component is being refernced in other template
## Conditional
Using conditionals statement in template
E.g the below statment set CreateProdResource to true if EnvType === Prod
```
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
- Some metadata u want to attach to component

# Intrinsic Functions
- Must know list
    - Fn::Ref
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

# StackSets
When we want to create, update & delete stack across multiple accounts & regions
## Characteristic
- Only administrator to create stack.
- Trust account do CRUD.
- Update will happen across every regions & accounts.