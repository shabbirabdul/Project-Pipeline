#Devops project 

###Build

####Jenkins Server setup 

1. Install Jenkins
   
   Download Jenkins.war and run it using the following command from terminal
   `java -jar jenkins.war  `

2. GitHub plugin installation

  In order to build projects that are hosted on GitHub repositories, our Jenkins installation has to have GitHub Plugin installed by following these steps:

  - Navigate to `http://localhost:8080/jenkins`
  - Click Manage Jenkins
  - Click Manage Plugins
  - Click the Available tab
  - In the Filter text field enter 'github'
  - In the Filter text field enter 'EC2'
  - Select GitHub Plugin, amazon-ec2-plugin and click "Download now and install after restart button" to install apropriate plugins

3. Maven and Git configuration

  Configure Jenkins to use Maven and Git client local installations by following these steps:

  - Navigate to http://localhost:8080/jenkins
  - Click Manage Jenkins
  - Click Configure System
  - In the JDK section click Add JDK button, check Install automatically checkbox 
  - In the Git section click Git Installations... button and enter Name and Path to Git executable values
  - In the MAVEN section check install automatically check box and select 3.1.2 MAVEN version
 
####Testing – Building public repository hosted on GitHub

  To test our configuration, we build one of the project hosted on GitHub, which uses maven. The project can be found at
  https://github.com/shabbirabdul/LilyPadCompass. 
  
  - Navigate to http://localhost:8080/jenkins
  - Click Click New Job
  - Select Build a free-style software project option, enter Job name value and click OK
  - In the Source Code Management section select Git option
  - Enter Repository URL – for this test we used https://github.com/shabbirabdul/LilyPadCompass.git
  - In the Build section select Invoke top-level Maven targets
  - Enter compile in the Goals field
  - Click Advanced... button
  - Enter LilyPadCompass/pom.xml in the POM field. You need to tell Jenkins where to find pom.xml file when looking from the root of the project.
  - Click Apply and then Save
  - On the next screen click Build Now button
  - In the Build History section a new build has appeared
  - To see how the project is being cloned and build: Move your mouse over it and select Console Output item

####Git Hook Configuration

   Git Hook allow you to notify Jenkins of a new commit. The following command is added to pre-push 
   
   `curl http://localhost:9191/job/Test/build?token=LONG_RANDOM_TOKEN`
   
   The value of the token in the project settings configurations will remain the same.
   Now, when a commit is pushed to github repository of the project, it will be build automatically.

####Dependencies set up and build script execution

   All the required dependencies are listed in pom.xml and the build server(Jenkins) will pick the build script configured in the project. The Pom.xml has public repos listed in the file, which picks the required dependencies necessary for clean build. The clean install command configured while building a job is:  

####Multiple Nodes
   
   We choose AWS EC2 to act as Jenkins slaves (2 nodes) and the master will be running on our machine. The AWS nodes have been configured to run when a build is triggered based on the tag values (A String to tell which node to run from). When a build is triggered with tag values mentioned, the slaves would be triggered automatically. 

####Build Status

   Jenkins provides a way of getting the status of the build by posting a HTTP post method. The response is returned in the form of a JSON object. 
   The below URL will give Response of the build status when triggered.
   
