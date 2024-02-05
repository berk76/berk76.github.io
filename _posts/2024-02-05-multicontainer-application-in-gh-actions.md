---
title: Running multicontainer application in GitHub Actions
date: 2024-02-05 21:00:00 +0100
categories: [programming]
tags: [github,docker]
---

GitHub Actions is one of the most amazing feature in GitHub. It allowes you to automate different tasks by creating different workflows in your pipeline. Github is offering 2000 Action minutes per month in Github Free plan which is more than sufficient for users like me.

I was curious if it would be even possible to use GitHub Actions for build and run multicontainer application (basically web application with database) and perform selenium test against it. So I decided to create small proof of concept (POC) project [Docker compose in Github actions](https://github.com/berk76/docker-compose-in-gha-poc).

I have created small bare bone Java application running in Tomcat server which is using [Firebird Sql](https://firebirdsql.org/) database. Then I have created simple [Docker Compose file](https://github.com/berk76/docker-compose-in-gha-poc/blob/master/docker-compose/poc.yml) which I tweaked on my local computer and tried to run it in GitHub Actions and surprisingly it was working!

So I tried to complete whole [pipeline](https://github.com/berk76/docker-compose-in-gha-poc/blob/master/.github/workflows/build.yml) which contains following steps:

1. Build Java Web application and produce WAR file
1. Build Docker image for Web application
1. Start multicontainer application in [docker compose](https://github.com/berk76/docker-compose-in-gha-poc/blob/master/docker-compose/poc.yml)
1. Restore database [testing content](https://github.com/berk76/docker-compose-in-gha-poc/blob/master/db-schema/database.sql) in database container
1. Install Google Chrome for testing (which includes selenium driver)
1. Run selenium test against application which produces screen shots
1. Archive screen shots (you can find them in the detail of each workflow in Actions menu)

Complete pipeline is [here](https://github.com/berk76/docker-compose-in-gha-poc/blob/master/.github/workflows/build.yml).

![Docker compose in Github actions POC](https://raw.githubusercontent.com/berk76/docker-compose-in-gha-poc/master/pic1.png)

This pipeline can be triggered on each commit or pull-request and each run of pipeline creates new clean and isolated testing environment. __You don't need any dedicated testing virtual machine or kubernetes cluster anymore and you can run as many test as you want all for free.__

Described POC proofs that GirHub Actions is very powerfull tool in which you can build, configure, run and test nontrivial multicontainer applications. This is not limited only to web applications with sql database neither to selenium tests.

Feel free to fork [this POC project](https://github.com/berk76/docker-compose-in-gha-poc) and do you our experiments. Please let me know in case you will find any improvement or other interesting complex scenario.
