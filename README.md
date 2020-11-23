# CI Pipeline Practical Project Readme

## Contents
* [Aims](#aims)
* [Benefits Of Cloud Solutions and CI](#benefits-of-cloud-solutions-and-ci)
* [Architecture](#architecture)
* [CI Pipeline](#ci-pipeline)
* [Project Tracking](#project-tracking)
* [Testing](#testing)
* [Known Issues](#known-issues)
* [Future Improvements](#future-improvements)
* [Author](#author)

## Aims
This project encapsulates the following concepts: 
* Continuous Integration
* Containerisation
* Configuration Management
* Cloud Solutions
* Infrastructure Management
* Orchestration

They are used to deploy a simple Flask application comprising of two services in a microservice architecture, and which was already provided, in a Continuous Intergation pipeline.

In order to achieve this, the following technologies are used:
* CI Server: Jenkins
* Containerisation: Docker
* Configuration Management: Ansible
* Cloud Solutions: AWS EC2, VPC, RDS ad EKS
* Infrastructure Management: Terraform
* Orchestration Tool: Kubernetes
* Reverse Proxy: NGINX

In addition, Git and GitHub were used as the version control system, and a Jira Kanban board was used for project planning.

## Benefits Of Cloud Solutions and CI
There are many benefits to deploying applications in a cloud environment. As well as reduced set up costs, scalability, and the ability to hand over a significant part of the security responsibilities over to the cloud provider, the cloud provides an environment for 

CI:

The cloud and CI technologies utilised in the context of this project are described in more detail below. 

### Ansible

Ansible is an open-source software provisioning, configuration management, and application-deployment tool.
It runs on and can configure many Unix-like systems, as well as Microsoft Windows.

### Jenkins

![jenkins][jenkins]

### Terraform


## Architecture
![architecture][architecture]

Pictured above is the continuous integration pipeline with the associated frameworks and services related to them. This pipeline allows for rapid and simple development-to-deployment by automating the integration process, i.e. I can produce code on my local machine and push it to GitHub, which will automatically push the new code to Jenkins via a webhook to be automatically installed on the cloud VM. From there, tests are automatically run and reports are produced. A testing environment for the app is also run in debugger mode, allowing for dynamic testing.

This process is handled by a Jenkins 'pipeline' job with distinct build stages. The design of this type of job means that if a previous build stage fails, the job will fail altogether and provide you with detailed information as to where this occurred. The more modular you make this system, the easier it is to pinpoint where your code is failing. As pictured below, the four build stages are:
* 'Checkout SCM' (pull code from Git respository)
* 'Build' (would be more accurately named 'Installation' as Python doesn't require building, in the strictest sense)
* 'Test' (run pytest, produce coverage report) 
* 'Run' (start the flask-app service on the local VM, belonging to systemctl)



Once the app is considered stable, it is then pushed to a separate VM for deployment. This service is run using the Python-based HTTP web server Gunicorn, which is designed around the concept of 'workers' who split the CPU resources of the VM equally. When users connect to the server, a worker is assigned to that connection with their dedicated resources, allowing the server to run faster for each user.

## CI Pipeline


## Project Planning and Tracking
A Jira Kanban board was used to plan and track the progress of the project. While this type of project tracking software is usually used for projects involving user stories, in the context of this project it was a highly useful tool to break down the deployment of the CI pipeline into smaller technical steps. 

Below are pictured the epics associated with the project, as well as a burndown chart for one of the four sprints.
![kanban][kanban]

![burndown][burndown]

You can find the link to this board here: https://badamiec.atlassian.net/jira/software/projects/PPCP/boards/4/roadmap

Past sprints and burndown charts can be accessed in the Reports section along with past issues, child issues and estimated story points. 




The board has been designed such that elements of the project move from left to right from their point of conception to being finished and fully implemented. Each card is also colour-coded according to which element of the project it pertains. From left to right, these lists are:
* *Project Requirements*
   A list of requirements set out in the brief in order for this to be a successful project.
* *Project Resources*
   List of relevant resources for quick access.
* *User Stories*
   Any functionality that is implemented into the project first begins as a user story. This keeps the development of every element of the web app focused on the user experience first.
* *Planning*
   The initial stages where a specific element (e.g. a block of code, a server, etc.) is being considered for implementation.
* *In Progress*
   Once the element has had any code written for it/exists in any way, it is placed in the 'in progress' list.
* *Testing*
   Once the element has been created, it moves to the 'testing' list, where its functionality is tested.
* *Finished*
   Any element that is considered to be finished (i.e. works according to its specification) lives in this list.

## Testing
An important step in the CI pipeline is testing. The Jenkins pipeline in this project is designed in such a way that when a change is made to the source code, tests are ran and must succeed in order for the pipeline to proceed with the building and pushing of updated docker images to Docker Hub. 
pytest is used to run the tests on the app. Tests were provided for both the backend and frontend of the flask app, and pytest generated a coverage report as a console output (pictured below) which informed the developer about which tests failed and which passed.

Successful frontend report:

![frontendtest][frontendtest]

Successful backend report:

![backendtest][backendtest]

The testing stages make use of the '| grep passed' command and the fact that a Jenkins pipeline stage will fail if the last console command in the stage is unsuccessful. If the test fails in either the backend or the frontend, the grep command will not find any line containing 'passed' and will instead show FAILURES, causing the pipeline to skip the later steps. No updated images are pushed to Docker Hub and the Kubernetes cluster pods and services are not configured. A failed test coverage report is shown below. 

![failures][failures]




## Known Issues


## Future Improvements


## Author
Basia Adamiec

[jenkins]: https://i.imgur.com/Ez2Pxsz.png

[architecture]: https://i.imgur.com/wEEHRHN.png

[kanban]: https://i.imgur.com/94l3cn6.png
[burndown]: https://i.imgur.com/2XwEDaP.png

[frontendtest]: https://i.imgur.com/wz3MkW1.png
[backendtest]: https://i.imgur.com/dOb6OZe.png
[failures]: https://i.imgur.com/qULC3iT.png






