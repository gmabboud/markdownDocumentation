
# Setting up Kuksa.val Server for Testing and Active Use

*Garret Abboud 02/17/2024*

## Local Test

1. Clone these five repositories into separate files:  
   a. kuksa.val: https://github.com/eclipse/kuksa.val  
   b. kuksa-can-provider: https://github.com/eclipse-kuksa/kuksa-can-provider  
   c. UKSC dbc2vssMapping: https://github.com/KentuckySolarCar/dbc2vssMapping  
   d. flutter: https://github.com/flutter/flutter  
   e. flutter dashboard: https://github.com/KentuckySolarCar/flutter_dashboard
2. Follow the repository README’s to ensure you have all setup requirements, you
   will also need Docker installed for your OS so that you can make the
   kuksa.val container.  
   a. https://www.docker.com/get-started/
   b. You will also need Dart installed to run flutter.
3. Create an empty directory user/kuksaval.config to contain the configurations
   for the kuksa.val server. Run this command 
   ```
   docker run -it --rm --net=host -v
   $HOME/kuksaval.config:/config  -p 127.0.0.1:8090:8090 -e LOG_LEVEL=ALL ghcr.io/eclipse/kuksa.val/kuksa-val:master
   ```
   to test if your container will
   boot and populate that directory.
4. Configure all of the software stack  
   a. Within kuksa-can-provider import the current dbc file, .json mapping file,
   and the can replay file you want to use. Open config/dbc_feeder.ini and
   configure that for the server, making sure the mapping(json), dbcfile,
   candumpfile, and dbc_default_files point correctly.
   b. Within kuksaval.config put the correct .json file from dbc2vssMapping in
   the directory. Open config.ini and make sure that either you changed the name
   of your .json to vss.json replacing the one already there or change the topic
   to the prefix name of your .json. (you may also need to add insecure = true
   to get around the certificate check if thats giving you problems)
   c. Ensure that your flutter dashboard app will run. See mac issues below if
   needed.
5. Start up your kuksa.val server container.  
   a. Ensure that the docker daemon is running either desktop or cli.
   b. Enter the kuksa.val directory and run this command to start the server:
   ```
   docker run -it --rm -v $HOME/kuksaval.config:/config  -p 127.0.0.1:8090:8090 -e LOG_LEVEL=ALL ghcr.io/eclipse/kuksa.val/kuksa-val:0.2.1-amd64
   ```
   c. Doesn’t necessarily have to be run from the kuksa.val directory.
6. Start up the flutter dashboard.
   a. Enter the flutter_dashboard directory
   b. Run this command: 
   ```
   flutter run lib/main.dart
   ```
7. Start the can provider replay.
   a. Renter kuksa-can-provider directory b. Run the dbcfeeder.py python
   program: *python3 dbcfeeder.py* c. If the feeder script says that your SSL
   certificate has expired make new ones using kuksa-common and put them in a
   new certs folder in kuksa.config/certs. The generation script is
   *genCerts.sh*

## Databroker stuff
Command we want:
docker run --rm -it -v $HOME/kuksaval.config:/config -p 55556:55555 ghcr.io/eclipse-kuksa kuksa-databroker:main --insecure --vss config/vss.json
## MacOS Issues
Platform for flutter might need to be created: (within flutter_dashboard
directory) *flutter create --platforms macos .*

Probably need to give entitlement to flutter for local test: (within
flutter_dashboard directory) macos/Runner/DebugProfile.entitlements add this:
`<key>com.apple.security.network.client</key>`
`<true/>`
