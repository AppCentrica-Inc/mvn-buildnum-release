This is a minimal implementation of a Maven project using a build server build number for the version number. Though primarily intended for a Continuous Deployment environment that requires a fully automated release stategy, it could be used anywhere a simple and reliable Maven release process is desired. A blog post describing it in more details can be found here:

    <insert URL when blog is published>

Running everything via Maven in a Bash shell to test the configuration looks like this:

    $ mvn versions:set -DgenerateBackupPoms=false -DnewVersion=0
    $ mvn install
    $ mvn scm:tag
    $ mvn deploy:deploy-file -DpomFile=pom.xml -Dfile=pom.xml -DrepositoryId=artifact_repository -Durl=http://localhost:8081/repository/maven-releases
    $ mvn deploy:deploy-file -DpomFile=child/pom.xml -Dfile=child/target/mvn-buildnum-release-child.war -DrepositoryId=artifact_repository -Durl=http://localhost:8081/repository/maven-releases
    $ mvn tomcat7:redeploy

The commands above assume a development/test environment with default local installations of Sonatype Nexus Open Source and Apache Tomcat, it may be necessary to change there URL's to match your local environment. After completing these commands you should be able to access the deployed application at the following URL:

    http://localhost:8080/mvn-buildnum-release/index.html
