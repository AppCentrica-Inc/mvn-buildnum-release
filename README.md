This is a minimal implementation intended to demonstrate a Maven release and versioning strategy using the optimized for using a build server build number in a Continuous Deployment environment. A blog post describing it in more details can be found here:

    <insert URL when blog is published>

Running everything via Maven in a Bash shell to test the configuration looks like this:

    $ mvn versions:set -DgenerateBackupPoms=false -DnewVersion=0
    $ mvn install
    $ mvn scm:tag
    $ mvn deploy:deploy-file
            -DpomFile=pom.xml
            -Dfile=pom.xml
            -DrepositoryId=artifact_repository
            -Durl=http://localhost:8081/repository/maven-releases
    $ mvn deploy:deploy-file
            -DpomFile=child/pom.xml
            -Dfile=child/target/mvn-buildnum-release-child.war
            -DrepositoryId=artifact_repository
            -Durl=http://localhost:8081/repository/maven-releases
    $ mvn tomcat7:redeploy

After completing this you should be able to access the application at the following URL:

    http://localhost:8080/mvn-buildnum-release/index.html
