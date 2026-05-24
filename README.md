# Building-an-AI-Driven-Threat-Hunting-Workflow-with-Security-Onion

# Table of Contents

1.  [Inspiration](#orgec7f558)
2.  [Components](#org68d66c8)
3.  [Setup](#org0d29280)
    1.  [Security Onion](#org0b8c995)
    2.  [Elasticsearch MCP](#org9979551)
    3.  [AI Agent](#org0f8f1fa)
4.  [Testing the workflow](#org6e0273c)
5.  [Results](#org713e19c)
6.  [Closing thoughts](#orgdd4fadc)



<a id="orgec7f558"></a>

# Inspiration

-   A senior analyst at my workplace sent me an article that explained a similar workflow using Security Onion and the Elasticsearch MCP server: <https://medium.com/@uhtavi0/security-operations-with-elasticsearch-mcp-and-security-onion-26c3819bebd6>
-   I was instantly interested because I am already a huge fan of Security Onion. My implementation varies a little bit from the original article,
    but it did help serve as a reference point to getting this set up.


<a id="org68d66c8"></a>

# Components

-   Security Onion Virtual Machine.
    -   I used a Security Onion import node for this project.

-   Docker Engine and Docker Compose.
    -   Used to containerize and deploy the Elasticsearch MCP server.

-   Coding agent of your choice.
    -   For this workflow, I chose opencode.

-   LLM of your choice.


<a id="org0d29280"></a>

# Setup

-   I recommed reading over the official documentation for each component before setting up this workflow. The installs are straightforward.
-   The following steps will serve as a high-level overview on how I set up my environment. For the technical implementation details, refer to
    the documentation.


<a id="org0b8c995"></a>

## Security Onion

-   The Security Onion does not have the &ldquo;elasticsearch<sub>rest</sub>&rdquo; firewall hostgroup by default. I manually added the group and add the IP I wanted
    to allow access to Elasticsearch. It is also to important to allow UDP port 9200 as well in the portgroup.

-   Once the firewall configurations were completed, I navigated to Kibana -> Security -> API keys.
-   I created the API key that would later be used by the Elasticsearch MCP server for authentication.


<a id="org9979551"></a>

## Elasticsearch MCP

-   I creted a working directory containing:
    -   A &rsquo;.env&rsquo; file
    -   A &rsquo;docker-compose.yml&rsquo; file

-   The .env file stored:
    -   Elasticsearch URL
    -   Elasticsearch API key
    -   Elasticsearch credentials

-   I then deployed the MCP server using Docker Compose.

-   The compose file used for this project can be found here: <https://github.com/cr7258/elasticsearch-mcp-server/blob/main/docker-compose-elasticsearch.yml>


<a id="org0f8f1fa"></a>

## AI Agent

-   I used opencode as my AI coding agent for this project and referenced the official documentation heavily for installation and configuration.

-   Once installed, I configured:
    -   The Elasticsearch MCP server connection
    -   My preferred LLMs


<a id="org6e0273c"></a>

# Testing the workflow

-   To validate my workflow, these are the steps I took:
    1.  Start my Security Onion virtual machine.
    2.  Import a pcap containing known malicious activity.
    3.  Launch opencode which automatically starts the Docker container and connects to the MCP server.
    4.  Query the LLM based on findings obserced within the PCAP data.
    5.  Cross reference the AI-generated analysis against telemetry within Security Onion to validate accuracy.


<a id="org713e19c"></a>

# Results


<a id="orgdd4fadc"></a>

# Closing thoughts

-   This project was a lot of fun and a big learning experience with MCP servers and workflow automation. I look forward to experimenting with other tools
    and platforms to build similar workflows. Give this a shot and thank you for reading!

