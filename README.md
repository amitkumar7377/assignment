The pipeline is triggered whenever changes are pushed to the main branch. It uses a Windows agent (vmImage: 'windows-latest').
And performs the following steps:
It sets the build configuration variable to 'Release'.
It uses the UseDotNet task to install the .NET Core SDK version 3.x on the agent machine.
It uses the DotNetCoreCLI task to restore the NuGet packages.
It uses the DotNetCoreCLI task to build the .NET Core web application using the specified build configuration.
It uses the DotNetCoreCLI task to publish the application, creating the output in the $(Build.ArtifactStagingDirectory) directory.
It uses the PublishBuildArtifacts task to publish the build artifacts to the Azure DevOps pipeline, making them available for further steps or deployment.
After building and publishing the artifact, it is pushed to an Azure Git repository under a branch named "add-artifact".
The script then uses the DownloadPipelineArtifact task to download the latest build artifact from the specified Azure DevOps pipeline and stores it in the "downloaded" subdirectory of the agent's working directory.
