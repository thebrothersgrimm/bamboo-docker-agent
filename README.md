# Bamboo Docker Agent
This Dockerfile is based on the official [atlassian/bamboo-java-agent](https://hub.docker.com/r/atlassian/bamboo-java-agent/). The source image is built with OpenJDK v7, but v8 is required by later versions of Bamboo server so new bootstrap files can be updated.

The issue with the offical image presents as follows:
```
WrapperSimpleApp: Unable to locate the class com.atlassian.bamboo.agent.bootstrap.AgentBootstrap: java.lang.UnsupportedClassVersionError: com/atlassian/bamboo/agent/bootstrap/AgentBootstrap : Unsupported major.minor version 52.0
```

This version is tested with Atlassian Bamboo version 5.12.3.1.

### Running
The official guide suggests using the path http://hostname:8085/bamboo for BAMBOO_SERVER but it never worked against my server instance. It might be the way it was setup but if it doesn't work for you then try using that.

#### Simple
```bash
docker run -e HOME=/root/ -e BAMBOO_SERVER=http://hostname:8085  -it cizer/bamboo-docker-agent
```

#### Attaching docker from host
The following command allows you to execute docker commands from the container's host meaning you do not need to install docker on the agent.
```bash
docker run -e HOME=/root/ -e BAMBOO_SERVER=http://hostname:8085 -v /usr/bin/docker:/usr/bin/docker -v /usr/bin/docker-compose:/usr/bin/docker-compose -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/docker/aufs:/var/lib/docker/aufs -v /var/lib/docker:/var/lib/docker -it cizer/bamboo-docker-agent
```
