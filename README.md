# docker-kodi-server

Run Kodi using docker as a server

This will allow you to
* serves files through the Kodi UPnP Library to your UPnP client/players (such as Kodi or Chromecast).
* Web access every time , or use with some tools like [htpc-manager](http://htpc.io/)
* Trigger library scan When you want using api or from sickbeard/sickrage/couchpotato/sonarr/radarr/...

### Preqrequisites:
* Docker (Follow the [installation instructions](https://docs.docker.com/))
* A [shared Library with mysql](https://kodi.wiki/view/MySQL) is higly recommended to shared library ( If you don't use UPnP) 

### Quick start

1. Prepare a full kodi profile with the regular GUI version ( windows or linux )

If you require web access, make sure to enable this, and set the port to **8089**.
Because 8080 is default for http proxy , this docker image expose 8089

Advices for the profile:
* You don't need any display , personnaly I disable all menu and told kodi to start on settings
* As software fake display is use , every graphic change is cpu cost , disable library update progess ( Settings / Media / Library : Hide progress of library updates)
* Only configure scrapers , and set addons on auto update

2. Make a copy of the ~/.kodi directory ( destination  doesn't matter , this is just an example)

        $ cp -r ~./kodi ~/kodi-server-profile

2. Use prebuild docker image ([see here](https://hub.docker.com/r/celedhrim/kodi-server/))

  For the last stable version,

        $ docker pull celedhrim/kodi-server

  For a specific version,

        $ docker pull celedhrim/kodi-server:branchname


  | branchname           | Kodi branch | Kodi version | Ubuntu version       |
  |----------------------|-------------|--------------|----------------------|
  | `lastest` ( default) | nexus       | 20.1         | 22.10 (Kinetic Kudu) |
  | `helix`              | helix       | 14.2         | 14.04 (Trusty Tahr)  |
  | `isengard`           | isengard    | 15.2         | 14.04 (Trusty Tahr)  |
  | `jarvis`             | jarvis      | 16.1         | 16.04 (Xenial Xerus) |
  | `krypton`            | krypton     | 17.6         | Archlinux            |
  | `leia`               | leia        | 18.9         | 18.04 (Bionic Beaver)|
  | `matrix`             | matrix      | 19.4         | 18.04 (Bionic Beaver)|
  | `nexus`              | nexus       | 20.1         | 22.10 (Kinetic Kudu) |
  | `experimental`       | krypton     | 17.0rc2      | 18.04 (Bionic Beaver)|

3. Run the image ( change the **/path/to/kodi-server-profile**)

        $ docker run -d --restart="always" --net=host -v /path/to/kodi-server-profile:/usr/share/kodi/portable_data celedhrim/kodi-server

   or if use specific branch

        $ docker run -d --restart="always" --net=host -v /path/to/kodi-server-profile:/usr/share/kodi/portable_data celedhrim/kodi-server:branchname




### Build the container yourself
    $ git clone https://github.com/Celedhrim/docker-kodi-server.git
    $ cd docker-kodi-server
    $ git checkout branchname
    $ docker build --rm=true -t $(whoami)/kodi-server .

Then proceed with the Quick start section.
