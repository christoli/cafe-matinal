# Projet café matinal

## How to install


### Installation for Linux

#### Install java

At the time I am writing, cordova does not support java 10. We are going to install java 8
Run the following commands

> sudo add-apt-repository ppa:linuxuprising/java
> sudo apt update
> sudo apt install oracle-java8-installer

Configure java

> sudo apt install oracle-java8-set-default
> sudo update-alternatives --config javac
> sudo update-alternatives --config java




#### Install android sdk

You have 2 ways to install it : 

 -# Install android studio
 -# Download and install manually

Install android studio:

 - visit this page : https://developer.android.com/studio/
 - unzip the archive and move it to an appropriate location like /usr/local or /opt/
 - to start android studio, run studio.sh inside the android-studio folder

Full installation instruction here : https://developer.android.com/studio/install

Accept the licenses

> /opt/android-sdk/bin/sdkmanager --licenses --sdk_root=/opt/android-sdk/


Download the package and install the sdk manually, please visit this page : https://developer.android.com/studio/

#### Configure PATH variables

Add this lines to your ~/.bashrc file

export 

#### Install gradle

For instructions on installing gradle, please visit this site : https://gradle.org/install/


#### Check the cordova installation

Run this command : 

> ionic cordova requirements

### Trying to automate everything with docker

Trying to have the same image for all developpers with a docker image and container.
Got inspiration from [this github repo](https://github.com/mswag/docker-ionic/)




