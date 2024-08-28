# Eidolon Chatbot Recipe

This project shows an example of a multi-llm multimedia enabled chatbot. Not all LLMs support multimedia, let alone 
mid-conversation brain-boosts. This can cause issues when swapping out components. Thankfully Eidolon's 
AgentProcessingUnit abstracts away those concepts so you can enable multimedia, json output, and function calling on 
even the smallest llm.

## Core Concepts
1. Customizing the AgentProcessingUnit
2. Running the UI

## Directory Structure

- `resources`: This directory contains additional resources for the project. An example agent is provided for reference.
- `components`: This directory is where any custom code should be placed.

## Running the Server in Docker

First you need to clone the project and navigate to the project directory:

```bash
git clone https://github.com/eidolon-ai/eidolon-chatbot.git
cd eidolon-chatbot
```

Then run the server using docker, use the following command:

```bash
make docker-serve
```

The first time you run this command, you may be prompted to enter credentials that the machine needs 
to run (ie, OpenAI API Key).

This command will download the dependencies required to run your agent machine and start the Eidolon http server in 
"dev-mode".

If the server starts successfully, you should see the following output:
```
Starting Server...
INFO:     Started server process [34623]
INFO:     Waiting for application startup.
INFO - Building machine 'local_dev'
...
INFO - Server Started in 1.50s
```

## Running the server in K8s

### Prerequisites

WARNING: This will work for local k8s environments only. See [Readme.md in the k8s directory](./k8s/Readme.md) if you are using this against a cloud based k8s environment.

To use kubernetes for local development, you will need to have the following installed:
* [Docker](https://docs.docker.com/get-docker/)
* [Kubernetes](https://kubernetes.io/docs/tasks/tools/)
* [Helm](https://helm.sh/docs/intro/install/)

Clone the project and navigate to the project directory:

```bash
git clone https://github.com/eidolon-ai/agent-machine.git
cd agent-machine
```

### Installation

Make sure your kubernetes environment is set up properly and install the Eidolon k8s operator.

```bash
make k8s-operator
```

This will install the Eidolon operator in your k8s cluster. **This only needs to be done once.**

Next install the Eidolon resources. This will create an Eidolon machine and an Eidolon agent in your cluster, start them, and tail the logs:

```bash
make k8s-serve
```

If the server starts successfully, you should see the following output:
```
Deployment is ready. Tailing logs from new pods...
INFO:     Started server process [1]
INFO:     Waiting for application startup.
INFO - Building machine 'local-dev'
INFO - Starting agent 'hello-world'
INFO - Server Started in 0.86s
```
