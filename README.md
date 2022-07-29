# Chirpstack LoRaWAN Network Server Stack running on balena

The ChirpStack open-source LoRaWAN Network Server stack provides open-source components for LoRaWAN networks. Together they form a ready-to-use solution including an user-friendly web-interface for device management and APIs for integration. Deploy this project on a Raspberry Pi with a LoRa concentrator running with balena.io


## Getting started 

### Hardware

* Raspberry Pi 3 / 4 or [balenaFin](https://www.balena.io/fin/)
* SD card in case of the RPi 3 / 4
* Tested with [RAK 2287 Concentrator](https://store.rakwireless.com/products/rak2287-lpwan-gateway-concentrator-module) with [RAK 2287 Pi Hat](https://store.rakwireless.com/products/rak2287-pi-hat)

### Software

* A balenaCloud account ([sign up here](https://dashboard.balena-cloud.com/) up to 10 devices for free)
* [balenaEtcher](https://balena.io/etcher)

Once all of this is ready, you are able to deploy this repository following instructions below.


## Deploy the code

### Via [Balena Deploy](https://www.balena.io/docs/learn/deploy/deploy-with-balena-button/)

Running this project is as simple as deploying it to a balenaCloud application. You can do it in just one click by using the button below:

[![](https://www.balena.io/deploy.png)](https://dashboard.balena-cloud.com/deploy?repoUrl=https://github.com/mpous/chirpstack-balena)

Follow instructions, click Add a Device and flash an SD card with that OS image dowloaded from balenaCloud. Enjoy the magic 🌟Over-The-Air🌟!


### Via [Balena-Cli](https://www.balena.io/docs/reference/balena-cli/)

If you are a balena CLI expert, feel free to use balena CLI.

- Sign up on [balena.io](https://dashboard.balena.io/signup)
- Create a new application on balenaCloud.
- Clone this repository to your local workspace.
- Using [Balena CLI](https://www.balena.io/docs/reference/cli/), push the code with `balena push <application-name>`
- See the magic happening, your device is getting updated 🌟Over-The-Air🌟!


## Configure the Chirpstack LoRaWAN Network Server

Once the Chirpstack application have been deployed properly on your device it's time to set up the Chirpstack Network Server.

![chirpstack-balena](https://user-images.githubusercontent.com/173156/181758981-7a9ae1eb-6050-47b4-8239-f81ad764a02f.png)


### Access to the Chirpstack Network Server

Type on your browser `http://<your local ip address>:8080` or use the balenaCloud Public URL using the port 8080.

![chirpstack-balena-login](https://user-images.githubusercontent.com/173156/181758752-c66b3258-e946-4e77-bb39-fb1f41c3e029.png)

Log in use as username and passowr `admin / admin`.

![chirpstack-balena-organizations](https://user-images.githubusercontent.com/173156/181758862-7bb02f02-8c31-49b7-a628-d72241b67c6a.png)


### Create a Network-Server

Go to `Network-servers` and click `+ ADD`.

<img width="1904" alt="chirpstack-network-server-configuration" src="https://user-images.githubusercontent.com/173156/181759559-c70e43b0-3683-40f8-9c16-369662fd62a6.png">

Type the `Network-server name` that you preffer and add as a `Network-server server` with `chirpstack-network-server:8000` which is the name of the LoRaWAN Network Server service running on the device.


### Create Gateway-profiles

Go to `Gateway-profiles`and click `+ CREATE`.

<img width="1904" alt="chirpstack-gateway-profiles-balena" src="https://user-images.githubusercontent.com/173156/181760580-382e9e20-c2ad-4f91-ae52-63cce1927502.png">

Add a name to the Gateway profile. I used the recommended value of `Sats interval` (30 seconds) and I also used the default `Enabled channels`with `0, 1, 2` values. Finally select the `Network-server` that you previously created.


### Create Service-profiles

Now go to `Service-profiles` and click `+ CREATE`.

<img width="1904" alt="chirpstack-service-profile-balena" src="https://user-images.githubusercontent.com/173156/181761221-e7af6040-2d71-4c64-ad14-1c9a30cd1eb7.png">

Add a `Service profile` name and select the `Network server` that you created previously. I checked `Add gateway meta-data`and checked as well `Enable network geolocation`. I also used `Device-status request frequency` with `0`, `Minimum allowed data-rata` to `0` and `Maximum allowed data-rate` to `5`.


### Create a Gateway

Time to set up the Gateway for your LoRaWAN stack.



