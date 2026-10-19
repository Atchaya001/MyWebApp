# Configuring Jenkins to Work with Java, Git and Maven

## Stage 1: Create a Maven Web Application Project

Using an IDE like Eclipse, we can create a simple Web Application in Maven. The following steps are used to build this web application.

**Step 1:** Click on File → New → Maven Project. The New Maven Project window will appear. Click Next without selecting any archetype. Select `maven-archetype-webapp` in the next window. Click Next and provide the Group Id and Artifact Id.

**Step 2:** In the Project Explorer window, right-click on the project and select Properties → Java Build Path. Click on the Libraries tab, select JRE System Library and edit it by giving the path of JDK. Java must be installed prior to building the Maven web application. Click Finish, then Apply and Close.

**Step 3:** The project structure of the Maven Web Application is displayed. Edit the `index.jsp` file.

**Step 4:** Edit `pom.xml` by adding dependencies. Add the Jakarta Servlet dependency in the `pom.xml` file. The dependency code can be obtained from mvnrepository.com.

**Step 5:** Right-click on the project name in Project Explorer and select Run As → Maven install. This will build the web application. The Build Success message will be displayed in the Console window.

**Step 6:** Right-click on the project name and select Run As → Run on Server. Configure the Tomcat folder installed on your local machine. Once the Tomcat server gets started, the output can be viewed in the web browser.

## Stage 2: Pushing the Maven Web Application on Git

The prerequisite is to have an account on GitHub. Create a repository with the same name as the Maven project.

**Step 1:** Sign in to GitHub.com by entering your username and password. Give the repository name, click New and create the repository.

**Step 2:** Click Settings → Developer Settings → Personal access tokens. Click Generate New Token to create a token. Select the repo checkbox and click Generate Token.

**Step 3:** In Eclipse IDE, click Window → Show View → Other. Select Git Repositories.

**Step 4:** On GitHub.com, copy the URL link of your repository.

**Step 5:** Inside Eclipse, click Clone a Git Repository. Enter the repository URL and click Next. Select the local destination directory and click Finish. Right-click the project and select Team → Share Project.

Click Window → Show View → Other and select Git Staging. Drag `index.jsp` and `pom.xml` from Unstaged Changes to Staged Changes. Enter a commit message and click Commit and Push.

Enter your GitHub username/email and personal access token when prompted. Then push the application.

**Step 6:** Refresh GitHub.com in the web browser. The web application will be visible on GitHub.

## Stage 3: Performing CI-CD using Jenkins

Open the Jenkins page using a web browser. Enter the username and password.

**Step 1:** Click Manage Jenkins. Select Plugins and install the Deploy to Container plugin. This plugin allows the web application to be deployed to the Tomcat server.

**Step 2:** Click New Item to create a job. Enter the job name, preferably the same as the web application name. Select Freestyle project and click OK.

**Step 3:** In the Description box, enter the project description. Select the GitHub project option and enter the URL of the repository created in Stage 2.

**Step 4:** Under Source Code Management, select Git and paste the URL of the GitHub repository. If the repository is public, credentials are not required. For a private repository, provide the credentials.

**Step 5:** If the branch of the GitHub repository is master, keep it as it is. Otherwise, specify the branch name.

**Step 6:** In the Build Trigger section, select Poll SCM and enter five stars with spaces in between. This triggers a Jenkins build when changes are made to the GitHub repository. Jenkins checks the repository every minute.

**Step 7:** Under Build Steps, add two build steps.

- First Step: Execute Windows batch command as `cd MyWebApp`. This switches to the MyWebApp folder.
- Second Step: Select Invoke top-level Maven target. Select the Maven version and enter the Maven command to clean, package or build. Under Advanced, specify the path for `pom.xml` if required.

**Step 8:** Under Post Build Actions, select Deploy war/ear to a container. Specify the WAR file path, for example `MyWebApp/target/MyWebApp.war`. Select the Tomcat container, add Tomcat credentials and enter the Tomcat URL.

Finally, click Apply and Save.

**Step 9:** Start the local Tomcat server. On the Jenkins page, click Build Now to build the automation. Check the Console Output for a successful build.

**Step 10:** Open the web browser and enter the URL of the web application.

**Step 11:** If changes are made to the repository on GitHub, Jenkins generates a build automatically. Refreshing the web application URL displays the changes.

## Conclusion

Thus, Jenkins facilitates Continuous Integration and Continuous Development by automating the build and deployment process.
