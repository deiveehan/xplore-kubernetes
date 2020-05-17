## Jenkins to Kubernetes deployment


### Setup Jenkins
This is already explained in the other read me files. 

### Steps to configure Jenkins to point to Git.

1. Create a fork of the project. 

2. Create an API key that will allow Jenkins to interact with Git.
    Go to Github settings..
    
    Settings->DeveloperSettings->Personal access tokens
    
    a. Generate a new token and allow permissions for repo-hook. This will allow jenkins to utilize git api to create web hooks.

        provide access for admin:repo_hook
        (write) & (read)
    
    b. Copy the token once it is generated. 
    
3. Jenkins plugin installation
    
    Ensure you have the following plugins installed
    - Git
    - Github
    - Github authentication
    - Gradle (if rquired)
    
4. Configure API key of Git in Jenkins

    Go to Manage Jenkins -> System configuration

    Go to Github section and Add new Github server. 
If you dont have this option, recheck if you have installed the plugin correctly and restart 

    Add the Credentials as secret text instead of username and password. 

                                                                                
    
    
