# Project-Pipeline
Devops project pipeline for building project

Download Jenkins war and run it using the following command from terminal

java -jar jenkins.war

Jenkins GitHub plugin installation

In order to build projects that are hosted on a GitHub repository our Jenkins installation has to have GitHub Plugin installed. Follow this steps:

  Navigate to http://localhost:8080/jenkins
  Click Manage Jenkins
  Click Manage Plugins
  Click the Available tab
  In the Filter text field enter 'githu'
  In the Filter text field enter 'EC2'
  Select GitHub Plugin, amazon-ec2-plugin and click Download now and install after restart button. Appropriate plugins   are being installed

Jenkins Maven and Git configuration

To configure Jenkins to use Maven and Git client local installations. The steps are:

 Navigate to http://localhost:8080/jenkins
 Click Manage Jenkins
 Click Configure System
 In the JDK section click Add JDK button, check Install automatically checkbox 
 In the Git section click Git Installations... button and enter Name and Path to Git executable values
 In the MAVEN section check install automatically check box and select 3.1.2 MAVEN version
 
Testing – Building public repository hosted on GitHub

To our configuration. We  build one of the project hosted on GitHub. This projects uses maven. It can be found at https://github.com/shabbirabdul/LilyPadCompass. Here are the steps:

  Navigate to http://localhost:8080/jenkins
  Click Click New Job
  Select Build a free-style software project option, enter Job name value and click OK
  In the Source Code Management section select Git option
  Enter Repository URL – for this test we used https://github.com/shabbirabdul/LilyPadCompass.git
  In the Build section select Invoke top-level Maven targets
  Enter compile in the Goals field
  Click Advanced... button
  Enter LilyPadCompass/pom.xml in the POM field

You need to tell Jenkins where to find pom.xml file when looking from the root of the project.

 Click Apply and then Save
 On the next screen click Build Now button
 In the Build History section a new build has appeared
 Move your mouse over it and select Console Output item – you can see how project is being cloned and build.

Git Hook Configuration:
 We can notify Jenkins of a new commit. 
 The following command is added to pre-push 
 curl http://localhost:9191/job/Test/build?token=LONG_RANDOM_TOKEN
 the value of the token in the project settings configurations will remain the same.
 Now, when a commit is pushed to github the project is build automatically.

Dependencies set up and build script execution:
All the required dependencies are 
 
 
 
