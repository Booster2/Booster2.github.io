---
layout: home
---

![](figs/booster-rocket.png)

## What is Booster?

Lorum ipsum

## Booster Notation

dolor sit amet

## Screenshots

![The Booster Tool](figs/booster-tool.png)

![A Generated Script (In mysql workbench)](figs/booster-generated-db-script.png)

![The login for a generated system](figs/booster-system-login-window.png)

![The main Booster interface](figs/booster-system-main-interface.png)

![The Booster Object viewer](figs/booster-object-view.png)

![A Booster generated edit method](figs/booster-generated-method.png)

## Install Instructions

### Docker Image

- Install Docker
- Clone the Booster Docker repository
- Copy a Booster2 specification into files/
- build the Docker image
```docker build . -t `whoami`/booster2:proto```
- run the docker image
```docker run -p 80:8080  -v `pwd`/files:/files `whoami`/booster2:proto myboosterspec.boo2```
- (optional) copy a database populate script into files/
- navigate to [http://localhost:80/gwi](http://localhost:80/gwi) login to browse your data
- login and password are set to the system name

To get an Eclipse based Booster2 editor and translator, follow the developer steps below.

### Developers

- Install the Spoofax 2.0.0-beta Eclipse distribution
- Clone the Booster 2.0 repository
- Import the Booster2 folder (as a Maven project) into your Spoofax Eclipse
- install maven 3.3.9 and configure Eclipse to use it, the embedded Maven has a sl4j bug.
- (optional) Install Jave EE into your Eclipse 
- (optional) Install Tomcat and integrate with Eclipse 
- (optional) Install MySQL 5.6

## People

People who have contributed to the project.

- James Welch
- Daco Harkes
- Ed Crichton
- [Seyyed Shah](http://sshah.co.uk)

## Technology

- Metaborg Spoofax Language Workbench
- MySQL
- Apache Tomcat

## Funding

The development of Semantic Booster been supported by the [ALIGNED](http://aligned-project.eu/)
Project, a European Union Horizon 2020 Framework project. Number: #644055.


