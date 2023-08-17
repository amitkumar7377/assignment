ass-1
Create a .net  hello world web application, build, publish and drop the package artifacts.
Solution-

Created a yaml pipeline "web.yml" which is triggered whenever changes are pushed to the main branch. It uses a Windows agent (vmImage: 'windows-latest').
And performs the following steps:
It sets the build configuration variable to 'Release'.
It uses the UseDotNet task to install the .NET Core SDK version 3.x on the agent machine.
It uses the DotNetCoreCLI task to restore the NuGet packages.
It uses the DotNetCoreCLI task to build the .NET Core web application using the specified build configuration.
It uses the DotNetCoreCLI task to publish the application, creating the output in the $(Build.ArtifactStagingDirectory) directory.
It uses the PublishBuildArtifacts task to publish the build artifacts to the Azure DevOps pipeline, making them available for further steps or deployment.

ass-2
Push the package to azure git repo and download from azure git repo.

Solution-
By using the same yaml pipeline "web.yml",
After building and publishing the artifact, it is pushed to an Azure Git repository under a branch named "add-artifact".
The script then uses the DownloadPipelineArtifact task to download the latest build artifact from the specified Azure DevOps pipeline and stores it in the "downloaded" subdirectory of the agent's working directory.

ass-3

How to create looping with yaml script ?
Solution-
Taking an example of 2 yaml pipeline files,
1-"build_publish_drop.yml" template defines the loop behavior for building, publishing, and dropping artifacts.
2-The main pipeline file "azure_pipeline.yml" uses the template and provides the configurations for looping.


ass-4
What is variable groups in Azure  ?
Solution-
In Azure DevOps, a variable group is a way to define a set of variables that can be securely reused across multiple pipelines, releases, and environments.

To create a variable group:
Go to your Azure DevOps project.
Navigate to Project settings > Variable groups.
Click on the New variable group button.
Define the variables you want to include in the group along with their values.
Set the appropriate scope for the variable group (project or specific pipelines).
Save the variable group.

In YAML Pipeline,we can declare it as,

variables:
- group: MyVariableGroup


ass-5
What is service connection in Azure Devops ?
Solution-
Service connections can be used for various purposes, such as connecting to external version control systems, package registries, cloud providers, and more.
They provide a centralized and secure way to authenticate and authorize access to these services.
Service connections play a crucial role in maintaining security and managing access to external resources while automating your workflows in Azure DevOps.
We can give service connection to ARM(Azure resource manager), Github , Docker registry etc.
To create a service connection:
1-Go to your Azure DevOps project.
2-Navigate to Project settings > Service connections.
3-Click on the New service connection button.
4-Select the type of service connection you want to create and follow the prompts to provide the required credentials or tokens.
