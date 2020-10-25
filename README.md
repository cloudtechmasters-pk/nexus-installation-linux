# nexus-installation-linux

## Install Java:
    yum install java-1.8.0-openjdk-devel java-1.8.0-openjdk-devel –y
    cd /opt
## Download nexus tar file:
    wget https://sonatype-download.global.ssl.fastly.net/nexus/3/nexus-3.0.2-02-unix.tar.gz
## Extract tar file:
    tar xvzf nexus-3.0.2-02-unix.tar.gz
## Change name of Nexus file:
    mv nexus-3.0.2-02/ nexus
## Add nexus user: 
    useradd nexus
## Change owner ship for nexus file:
** Nexus does not recommend to run by root, as internally uses elastic search which does not recommend.  
    chown -R nexus:nexus nexus
## Open /opt/nexus/bin/nexus.rc file and update data like as below:
    run_as_user="nexus"
## Link file:
    ln -s /opt/nexus/bin/nexus /etc/init.d/nexus
## Login to nexus user:
    su - nexus
## Start nexus:
    service nexus start
## Check status of nexus:
    service nexus status
## Now give our domain name in UI and check whether Nexus opened or not with https:
    http://100.26.240.37:8081/
## Nexus credentials
    username: admin
    Password: admin123

## Configuration
1. Copy maven-release & mavem-snapshot URL's from default repos. 
2. Maven should know the artifactory it is connecting to. Need to provide artfactory UN & password in maven <b>/opt/apache-maven-3.6.3/conf/settings.xml </b>. Under <server> tag block. Need to add both snapshot & release blocks.
    <server>
      <id>maven-snapshots</id>
      <username>admin</username>
      <password>admin123</password>
    </server>

 <server>
      <id>maven-releases</id>
     <username>admin</username>
      <password>admin123</password>
    </server>
3. In the maven pom.xml, <Project> tag add anywhere, <distributionManagement> tag/element -> snapshot repository & release repo. If Project version is SNAPSHOT -> snapshot repository. 
cd /opt    
git clone <weekend>
Search -> maven deploy to nexus
<distributionManagement>
   <snapshotRepository>
      <id>maven-snapshots</id>
      <url>URL from above</url>
   </snapshotRepository>
    <repository>
      <id>maven-releases</id>
      <url>URL from above</url>
   </repository>
</distributionManagement>

4. mvn deploy * wil clean install internally


