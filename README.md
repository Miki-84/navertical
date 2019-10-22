# NaverticAl

NaverticAl is extension for every Microsoft Dynamics 365 Busines Central developer.

## Features

* Create new AL App folder from template by using "Navertical:Go!" command.
* Create/Remove docker environment
* Compile AL App with dependencies
* Install AL Apps with dependencies
* Uninstall AL Apps with dependencies

## How to use

1. Create new AL App folder by using `navertical:Go!`
    This command will:
    * Ask for empty folder path
    * Ask for new App name (suggested the empty folder name)
    * Ask for new Repository URL
    * Clone template repository
    * Update the app.json with new id and app name (including dependency of TestApp)
    * Rename Workspace file based on App name
    * Open the Workspace
2. Create Docker environment by using `navertical:Create environment`
    This command will:
    * Create new docker container with name and image based on the settings in Settings.ps1
    * Make alc.exe compiler available from outside the container to allow compilation of the apps (may be will be changed later to compile inside container)
    * Import Test objects in the container to allow run App Tests
3. Add dependency Apps into Dependencies folder as GIT Submodules (preffered) or directly
4. Compile the Apps with `navertical:Compile App Tree`
    This command will:
    * Download system application app packages
    * Download App packages for dependencies when source code is not found in the App folder tree (MISSING FUNCTIONALITY)
    * Compile Apps in order to fullfill dependencies
    * Sign the Apps with CodeSigning certificate if `navertical.CertPath` is set
5. Publish the Apps with `navertical:Publish App Tree`
    This command will:
    * Install the Apps in order to fullfill the dependencies
    * Publish the Apps
6. To unpublish the Apps you can use `navertical:Unpublish App Tree`
7. To remove environment you can use `navertical:Remove Environment`

## Azure Pipeline

If you want to have CI pipeline created in your Azure DevOps, just push the App repository to your Azure Repository. If the Pipeline is not created automaticaly, go to your Azure Build Pipelines, click New, and select the repo. The Pipeline will be created automatically for you. If you want to change something in the pipeline, edit the  `Azure-pipelines.yml` file accordingly. By pushing new version to the Azure Repo, new definition of the pipeline will be automatically used.

## Requirements

All needed powershell scripts are installed by the extension ([navcontainerhelper](https://github.com/Microsoft/navcontainerhelper) and [NVRAppDevOps](https://github.com/kine/NVRAppDevOps)).

## Related projects

As a template for new AL App is used [MSDyn365BC_AppTemplate](https://github.com/kine/MSDyn365BC_AppTemplate) which uses [MSDyn365BC_Yaml](https://github.com/kine/MSDyn365BC_Yaml) for Azure Pipeline creation.

## Extension Settings

This extension contributes the following settings:

* `navertical.CertPath`: set to path to CodeSigning certificate
* `navertical.IgnoreVerification`: set to false to enable signature verification when installing the apps

## Known Issues

Missing possibility to pull missing dependencies from package server.

## Release Notes

### 0.2.0

Added selection of branch to clone in NaverticAL: GO!. This allows multiple template versions to exists (e.g. BC version or localization).

### 0.1.1

Removed unused configurations
Downgraded dependency event-stream to version 3.3.4 to remove malicious dependency

### 0.1.0

Fixed bug when reopening NaverticAl terminal, it used default terminal shell instead powershell (if different used)

### 0.0.2

Updated dependencies

### 0.0.1

Initial public release of the extension
