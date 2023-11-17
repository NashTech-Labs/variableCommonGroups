Variable Groups in Azure DevOps are logical containers that store key-value pairs and also allow you to manage and share variables across multiple pipelines and projects using a single pipeline.
This template will create and update the variable group.

### Pipeline Requirements

The pipeline requires the following parameters to be defined:
#### Parameters:

| Name  | type | Default | Values | Optional/Required | Comments |
| ------------- | :-------------: | :------------- | ------------- | ------------- | ------------- |
| organization | string | 'GitHUb' | | Required | It will be name of your Azure DevOps organization |
| projectName | string | 'Github' | | Required | It is mandatory to have a project name of your Organization |
| varGroupName | string | 'templateCommonVariables'' | | Required | Name of the variable group that you want to be updated in your Ado Library. |
| jsonInput | string | 'input.json' | | Required | Location of JSON file that contains variables for the variable group. |
| adoUserAccessToken | string | $(vg.Ado.userAccessToken) | | Required | ADO Personal Access Token to access variable group |


 These parameters provide multiple use case options for the pipeline.

#### Variables Group

The pipeline requires the following Variable group to be defined:


## Use Cases:- 

1:  Creating  the common variable group: : 
```yaml
variables:
- group: templateCommonVariables

resources:
  repositories:
    - repository: Variables
      type: github
      name: GitHubServiceConnection
      ref: <respective branch name>
      endpoint: 'GitHub'

steps:
  - template: variableGroup.yml@Variables
      parameters:
      organisation: DCTEng
      projectName: GitHub
      varGroupName: 'templateCommonVariables'
      jsonInput: 'Input.json'
      
```

2:  Updating the common variable group:

```yaml
variables:
- group: templateCommonVariables

resources:
  repositories:
    - repository: Variables
      type: GitHub
      name: GitHub
      ref: <respective branch name>
      endpoint: 'GitHub'

steps:
  - template: frameWork/common/pipeline/variableGroup.yml@Variables
      parameters:
      organisation: GitHub
      projectName: GitHub
      varGroupName: 'templateCommonVariables'
      jsonInput: 'Input.json'
      
```
