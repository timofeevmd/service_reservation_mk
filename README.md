
## [infrastructure](#install-infrastructure)
1. [java-11](#java)
2. [maven](#maven)
3. [docker](#docker)
4. [jmeter-5.4.1](#jmeter)

## [services](#services)
1. [docker-compose.yml](#docker-compose)
2. [jmeter configuration](#jmeter-configuration)
   - [plugin manager](#INSTALL-PLUGIN-MANAGER)
   - [how start your fist recording on](#how-start-your-fist-recording-on)
   - [macOs](#macOs)
   - [linux](#Linux)
   - [windows](#Windows)


## install infrastructure
0. The working directory throughout the entire master class will be located in the root directory of your user account if you are using a Unix-like system, or on drive C if you are using Windows. This is where we will place the cloned project.
```bash
mkdir ~/projects/ &&
cd ~/projects/ &&
git clone https://github.com/timofeevmd/service_reservation_mk.git
```


1. ### java
    1. #### **macOs**
       ```bash
       brew install openjdk@11
       ```
        - Expected result
        ```bash
        java --version
        ```
       Output
        ```bash
        openjdk 11.0.26 2025-01-21
        OpenJDK Runtime Environment Homebrew (build 11.0.26+0)
        OpenJDK 64-Bit Server VM Homebrew (build 11.0.26+0, mixed mode)
       ```
      troubleshooting
      - if you had different java version, check the [link](https://stackoverflow.com/questions/21964709/how-to-set-or-change-the-default-java-jdk-version-on-macos) for switch between your jdk's 
   2. #### **linux**
        - [manual](https://www.digitalocean.com/community/tutorials/how-to-install-java-on-centos-and-fedora)
        - if manual is not work
        - `wget https://builds.openlogic.com/downloadJDK/openlogic-openjdk/11.0.26+4/openlogic-openjdk-11.0.26+4-linux-64.tar.gz`
        - if wget is not work try to download [openjdk-11-...](https://builds.openlogic.com/openjdk-downloads?field_java_parent_version_target_id=406&field_operating_system_target_id=426&field_architecture_target_id=391&field_java_package_target_id=396)
       ```bash
         sudo mkdir -p /opt/java &&
         cd /opt/java &&
         sudo tar -xvzf ~/openlogic-openjdk-11.0.26+4-linux-x64.tar.gz &&
         sudo mv openlogic-openjdk-11.0.26+4-linux-x64 java-11 &&
         sudo vim /etc/profile.d/java.sh
         ```
        - set of them
       ```bash
         export JAVA_HOME=/opt/java/java-11
         export PATH=$JAVA_HOME/bin:$PATH
         ```
        - `source /etc/profile.d/java.sh`
        - Expected result 
        ```bash
        java --version
        ```
        Output
        ```bash
        openjdk 11.0.26 2025-01-21
        OpenJDK Runtime Environment Homebrew (build 11.0.26+0)
        OpenJDK 64-Bit Server VM Homebrew (build 11.0.26+0, mixed mode)
        ```
      troubleshooting
       - if you had different java version, check the [link](https://stackoverflow.com/questions/21964709/how-to-set-or-change-the-default-java-jdk-version-on-macos) for switch between your jdk's
      
    3. #### **windows**
        - download [.zip](https://builds.openlogic.com/downloadJDK/openlogic-openjdk/11.0.26+4/openlogic-openjdk-11.0.26+4-windows-x64.zip)
        - Follow the installation wizard, keeping the default settings.
        - Note the installation path (usually C:\Program Files\Eclipse Adoptium\jdk-11 or C:\Program Files\Java\jdk-11).
        - Open Control Panel → System → Advanced system settings.
        - Go to the Advanced tab and click Environment Variables.
        - Under System Variables
        - Find the `JAVA_HOME` variable (if it does not exist, click New)
        - Set `JAVA_HOME=C:\Program Files\Eclipse Adoptium\jdk-11`
        - Find Path → click Edit → New
        - Set `%JAVA_HOME%\bin`
2. ### maven
    1. [manual](https://www.baeldung.com/install-maven-on-windows-linux-mac#bd-installing-maven-on-mac-os-x) for macOs/linux/windows
        - Expected result
       ```bash
       mvn --version
       ```
       Output
       ```bash
       Apache Maven 3.9.9 (8e8579a9e76f7d015ee5ec7bfcdc97d260186937)
       Maven home: /opt/homebrew/Cellar/maven/3.9.9/libexec
       Java version: 11.0.19, vendor: Oracle Corporation, runtime: /Library/Java/JavaVirtualMachines/jdk-11.jdk/Contents/Home
       Default locale: en_US, platform encoding: UTF-8
       OS name: "mac os x", version: "15.3.2", arch: "aarch64", family: "mac"
       ```
3. ### docker
    1. [manual](https://docs.docker.com/desktop/) for macOs/linux/windows
    - Expected result
        ```bash
        docker --version &&
        docker-compose --version
        ```
      Output like this
        ```bash
       Docker version 24.0.6, build ed223bc
       Docker Compose version v2.23.0-desktop.1
       ```
    
   troubleshooting
    - Error permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.48/containers/json?all=1": dial unix /var/run/docker.sock: connect: permission denied

      ```bash
      sudo groupadd docker &&
      sudo usermod -aG docker $USER &&
      newgrp docker &&
      reboot
      ```
4. ### jmeter
    1. **macOs**
       ```bash
       mkdir ~/tools/ &&
       cd ~/tools/ &&
       curl -OL https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-5.4.1.zip      
       unzip apache-jmeter-5.4.1.zip &&
       cd ./apache-jmeter-5.4.1/bin/ &&
       ./jmeter
       ```
    2. **linux**
       ```bash
       mkdir ~/tools/ &&
       cd ~/tools/ &&
       wget https://dlcdn.apache.org//jmeter/binaries/apache-jmeter-5.4.1.tgz &&
       tar -xvzf apache-jmeter-5.4.1.tgz &&
       cd ./apache-jmeter-5.4.1/bin/ &&
       ./jmeter
       ```
    3. **windows**
        - downloads [.zip](https://dlcdn.apache.org//jmeter/binaries/apache-jmeter-5.4.1.zip)
        - unzip .zpi arch
        - run jmeter.bat

## services
<p style="color: yellow"> WARNING </p>

0. open `.env` file on the root of project
    1. If your laptop has an Intel or Ryzen CPU, change `PLATFORM` parm to `linux/amd64`
    2. If your laptop has M1 or newer chip, change `PLATFORM` parm to `linux/arm64`

1. #### **docker-compose**

- from root directory start docker-compose reservation_service
   ```bash
    docker-compose -f docker-compose.yml up -d 
   ```
- check current state
    ```bash
    docker ps -a
     ```
- expected result
    ```bash
    CONTAINER ID   IMAGE                                     COMMAND                  CREATED      STATUS                      PORTS                                            NAMES
     5516036bb73b   michaelt1223/perf_sr_frontend:latest      "/docker-entrypoint.…"   5 days ago   Up 22 minutes               80/tcp, 0.0.0.0:3000->3000/tcp                   frontend
     7fde5b402724   michaelt1223/perf_sr_backend:latest       "java -jar app.jar"      5 days ago   Up 22 minutes               0.0.0.0:8080->8080/tcp                           backend
     f08d6be43900   postgres:latest                           "docker-entrypoint.s…"   5 days ago   Up 22 minutes (healthy)     0.0.0.0:5432->5432/tcp                           database
     ```
  
## **jmeter configuration**

---
### 1. INSTALL PLUGIN MANAGER

1. Download Plugin Manager JAR file from: https://jmeter-plugins.org/get/
2. Move the file into your JMeter directory: `~/tools/apache-jmeter-5.4.1/lib/ext/PluginsManager.jar`
3. Restart JMeter
4. After launch, open the menu: `Options → Plugins Manager`
---
### 2. INSTALL REQUIRED PLUGINS
#### 1. Custom Thread Groups
- Go to: `Options → Plugins Manager → Available Plugins`
- Find and install: `Custom Thread Groups`
- Includes:
- Stepping Thread Group
- Concurrency Thread Group
- Arrivals Thread Group
- Plugin page: https://jmeter-plugins.org/?search=jpgc-casutg

### 3. RESTART JMETER
After installing plugins:
- Restart JMeter to load the new components
- Check for:
- **Custom Thread Groups** under `Thread Groups`
- **Dummy Sampler** under `Samplers`
- **Parallel Controller** under `Logic Controllers`
---

### how start your fist recording

#### 0. On TestPlan
- add thread group
- add `test script recorder`
    - Port: `8888`
    - Target Controller: `Test Plan > Thread Group`
    - Grouping: `Put each group in a new transaction controller`
    - Click `Start` button -> JMeter generated security certificate and put it onto `~/tools/apache-jmeter-5.4.1/bin/`. Try to find `ApacheJMeterTemporaryRootCA.crt`

macOS
------------------

#### 1. SETUP CERTIFICATE
1. Open **Google Chrome**
2. Go to `Settings` → search for `certificates`
3. Navigate to:  
   **Privacy and Security** → **Security** → **Manage Certificates**
4. Click **Manage certificates from macOS**
5. Drag and drop the certificate file from: `~/tools/apache-jmeter-5.4.1/bin/ApacheJMeterTemporaryRootCA.crt`
6. Right-click → **Get Info**
7. Expand the **Trust** section
8. Set **Always trust**

---

#### 2. SETUP PROXY
1. Open **System Settings**
2. Go to **Network**
3. Select your current network → click **Details**
4. Open the **Proxies** tab
5. Enable the following:
- **Web Proxy (HTTP)**
- **Secure Web Proxy (HTTPS)**
6. Set both servers to:
- **Server**: `127.0.0.1`
- **Port**: `8888`
7. Save the settings

---

#### 3. in Google Chrome
1. Navigate to: `http://127.0.0.1.nip.io`
2. Open **DevTools** (F12) → go to the `Network` tab
3. Apply the filter: `Fetch/XHR`
4. Ensure requests go through JMeter

---

Linux
------------------

#### 1. SETUP CERTIFICATE
1. Open a terminal
2. Run the following command:
   ```bash
   sudo cp ~/tools/apache-jmeter-5.4.1/bin/ApacheJMeterTemporaryRootCA.crt /etc/pki/ca-trust/source/anchors/ &&
   sudo update-ca-trust
   ```

This will install the JMeter certificate into the system trust store

#### 2. SETUP PROXY
1. Open Settings
2. Go to Network
3. Select your active connection and click Settings
4. Open the Proxy tab
5. Enable Use proxy for this network
6. Set the following values:
    - **HTTP Proxy**: `0.0.0.0, Port: 8888`
    - **HTTPS Proxy**: `0.0.0.0, Port: 8888 `
7. Click Save

#### 3. in Firefox
1. Open: http://127.0.0.1.nip.io
2. Open DevTools (F12) → go to the Network tab ,
3. Apply the filter: `Fetch/XHR`
4. Ensure requests are being captured by JMeter

Windows
------------------

### 1. SETUP CERTIFICATE
1. Open **Google Chrome**
2. Go to `Settings` → search for `certificates`
3. Navigate to:  
   **Privacy and Security** → **Security** → **Manage Certificates**
4. In the window that opens, select the `Trusted Root Certification Authorities` tab
5. Click `Import...`
6. Choose the JMeter certificate located at:  
   `~/apache-jmeter-5.4.1/bin/ApacheJMeterTemporaryRootCA.crt`
7. During the import, select:  
   "Place all certificates in the following store" →  
   `Trusted Root Certification Authorities`
8. Confirm the installation → click `OK`

### 2. SETUP PROXY
1. Open **Control Panel** → **Internet Options**  
   *(or run `inetcpl.cpl` via Win+R)*
2. Go to the **Connections** tab → click **LAN settings**
3. Check the box: `Use a proxy server for your LAN`
4. Set **Address** to: `127.0.0.1`
5. Set **Port** to: `8888`
6. Click `OK`, then again `OK`

### 3. in Google Chrome
1. Navigate to: `http://127.0.0.1.nip.io`
2. Open **DevTools** (F12) → go to the `Network` tab
3. Apply the filter: `Fetch/XHR`
4. Verify that requests go through JMeter

YOOOOOHOOOO, now you can restart your `Test Script Recorder` and sniff the traffic throw the PROXY

### Command to start JMeter on non GUI mode

notice
directory `report` must not be created before start the performance test

```bash
./jmeter \
-n -t ~/projects/service_reservation_mk/docs/scenarious/max_throughput_final_scn.jmx \
-j ~/projects/service_reservation_mk/docs/scenarious/jmeter.log \
-l ~/projects/service_reservation_mk/docs/scenarious//results.jtl \
-e -o ~/projects/service_reservation_mk/docs/scenarious/report/
```
