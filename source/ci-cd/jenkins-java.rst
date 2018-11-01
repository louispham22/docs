###########################
Build a Java app with Maven
###########################

This tutorial shows you how to use Jenkins to orchestrate building a simple Java application with Maven.

If you are a Java developer who uses Maven and who is new to CI/CD concepts, or you might be familiar whit these concepts but don’t know how to implement building your application using Jenkins, then this tutorial is for you.

The simple Java application (which you’ll obtain from a sample repository on GitHub) outputs the string "Hello world!" and is accompanied by a couple of unit tests to check that the main application works as expected. The results of these tests are saved to a JUnit XML report.

Prerequisites
=============
For this tutorial, you will require:
	- A macOS, Linux or Windows machine with:
		- 256 MB of RAM, although more than 512 is recommended.
		- 10 GB of drive space for Jenkins and your Docker images and containers.
	- The following software installed::
		- Docker - Read more about installing Docker in the Installing Docker section of the Installing Jenkins page.
		- Note: If you use Linux, this tutorial assumes that you are not running Docker commands as the root user, but instead with a single user account that also has access to the other tools used throughout this tutorial.
		- Git and optionally GitHub Desktop.

Run Jenkins in Docker
=====================

In this tutorial, you'll be running Jenkins as a Docker container from the jenkinsci/blueocean Docker image

To run Jenkins in Docker, follow the relevant instructions below for either macOS and Linux or Windows.

You can read more about Docker container and image concepts in the Docker and Downloading and running Jenkins in Docker sections of the Installing Jenkins page.

On macOS and Linux
==================
1. Open up a terminal window.
2. Run the jenkinsci/blueocean image as a container in Docker using the following docker run command (bearing in mind that this command automatically downloads the image if this hasn’t been done):

  :class:`docker run \
  --rm \
  -u root \
  -p 8080:8080 \
  -v jenkins-data:/var/jenkins_home \ 
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v "$HOME":/home \ 
  jenkinsci/blueocean`

Maps the /var/jenkins_home directory in the container to the Docker volume with the name jenkins-data. If this volume does not exist, then this docker run command will automatically create the volume for you.
Maps the $HOME directory on the host (i.e. your local) machine (usually the /Users/<your-username> directory) to the /home directory in the container.

Setup wizard
============

Before you can access Jenkins, there are a few quick "one-off" steps you’ll need to perform.

Unlocking Jenkins
When you first access a new Jenkins instance, you are asked to unlock it using an automatically-generated password.

1. After the 2 sets of asterisks appear in the terminal/command prompt window, browse to http://localhost:8080 and wait until the Unlock Jenkins page appears.

https://jenkins.io/doc/book/resources/tutorials/setup-jenkins-01-unlock-jenkins-page.jpg

2. From your terminal/command prompt window again, copy the automatically-generated alphanumeric password (between the 2 sets of asterisks).

https://jenkins.io/doc/book/resources/tutorials/setup-jenkins-02-copying-initial-admin-password.png

Copying initial admin password

On the Unlock Jenkins page, paste this password into the Administrator password field and click Continue.