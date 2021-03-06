# telerising API
Get advanced access to Zattoo internet streams

## About this project
This API provides channel playlists to playback streams on all compatible devices.

#### Zattoo Unlimited: Advantages
* Ad free channel switch, unlimited streaming on big screens (also in Zattoo Free)
* Watch Zattoo streams anonymously (Wilmaa)
* tvHeadend: Set PVR timers, unrestricted timeshift mode (also in Zattoo Free/Premium)
* All devices with M3U playlist support can handle Zattoo streams
* Download Zattoo recordings to local/external storage (watch recordings offline on all devices)
* Download Wilmaa recordings worldwide to local/external storage (also in Wilmaa Free)
* DE+CH: Watch Live TV without VPN/Proxy (Zattoo Premium/Ultimate subscription required)
* DE+CH: Choose your bandwidth on your own (API supports streams up to Full HD)
* Choose the Zattoo server on your own (better support for DNS services, use Zattoo DE+CH simultaneously)

#### The following providers (domain names) are supported:
* Zattoo: zattoo.com
* Wilmaa: wilmaa.com
* 1&1 TV: www.1und1.tv
* swb TV: tvonline.swb-gruppe.de
* NetCologne: nettv.netcologne.de
* EWE TV: tvonline.ewe.de
* Salt: tv.salt.ch
* Quickline TV: mobiltv.quickline.com
* M-Net: tvplus.m-net.de
* Waly.tv: player.waly.tv
* Lampert: www.meinewelt.cc
* BBV TV: www.bbv-tv.net
* VTX TV: www.vtxtv.ch
* myVision TV: www.myvisiontv.ch
* glattvision: iptv.glattvision.ch
* SAK TV: www.saktv.ch
* quantum TV: www.quantum-tv.com
* eir TV: tv.eir.ie

#### Supported platforms
* any Linux-based OS, e.g. Ubuntu, Debian
* not tested: Windows, Mac OS (Perl script only)

## The power of open source
You are welcome to test the script on your machine.
* If any errors occur, please open an issue on the GitHub project page.
* Help me by providing bug fixes etc. via pull requests.

## Disclaimer
All scripts provided by this project are licensed under GPL 3.0.
This includes a limitation of liability. The license also states that it does not provide any warranty.

## Support my work
If you like my script, please [![Paypal Donation Page](https://www.paypalobjects.com/en_US/i/btn/btn_donate_SM.gif)](https://paypal.me/sunsettrack4) - thank you! :-)

# Installation (Linux)

## Perl script
Please run the commands below to setup the script. "Sudo" is not required on user "root".

```bash
# Install all recommended applications:
sudo apt-get install perl nano libwww-perl net-tools build-essential wget unzip

# Install CPAN modules
sudo cpan install JSON
sudo cpan install Data::Dumper
sudo cpan install Time::Piece
sudo cpan install LWP
sudo cpan install LWP::Simple
sudo cpan install LWP::UserAgent
sudo cpan install LWP::Protocol::https
sudo cpan install HTTP::Daemon
sudo cpan install HTTP::Status
sudo cpan install HTTP::Request::Params
sudo cpan install HTTP::Request::Common
sudo cpan install HTTP::Cookies
sudo cpan install HTML::TreeBuilder
sudo cpan install URI::Escape
sudo cpan install IO::Interface::Simple
sudo cpan install IO::Socket::SSL
sudo cpan install Mozilla::CA
sudo cpan install Encode
sudo cpan install POSIX
sudo cpan install utf8

# Create any directory in your desired location, e.g.:
mkdir ~/telerising

# Download the .zip file and extract the files into your folder:
wget https://github.com/sunsettrack4/telerising/archive/v0.2.7.zip

# Unzip the file:
unzip v0.2.7.zip

# Move all script files to the created folder
mv ~/telerising-0.2.7/* ~/telerising/

# Set system-wide permissions to the folder and its related files
sudo chmod 0777 ~/telerising
sudo chmod 0777 ~/telerising/*

# Create login file (see reference below)
cd ~/telerising
nano userfile.json

# Run the Zattoo script from your script folder to start the API
perl zattoo.pl & disown
```
#### Login file to be placed in script folder
The variables "provider", "login" and "password" are required values, the other ones are optional.
```
{
  "provider": "zattoo.com",
  "login": "firstname.lastname@example.com",
  "password": "mypassword123",
  "interface": "eth0",
  "server": "fr5-0",
  "ffmpeg_lib": "/usr/bin/ffmpeg",
  "port": "8080",
  "ssl_mode": "1",
  "youth_protection_pin": "1234"
}

```
.

# How to use this API (query strings)

## Examples

#### Get channels.m3u to stream via VLC
```
http://<host-ip>:<port>/?file=channels.m3u&bw=5000&platform=hls
```

#### Get channels.m3u to stream via VLC (favorites only)
```
http://<host-ip>:<port>/?file=channels.m3u&bw=5000&platform=hls&favorites=true
```

#### Get channels.m3u to stream via ffmpeg pipe (Zattoo DE ==> 720p50)
```
http://<host-ip>:<port>/?file=channels.m3u&bw=5000&platform=hls5&ffmpeg=true
```


## Parameters

#### Filename (required to get M3U list)
```
file=channels.m3u - get channel list
file=recordings.m3u - get full list of recordings saved on Zattoo PVR cloud
```

#### Channel ID (required to stream Live TV channel)
```
channel=<id>
```

#### Recording ID (required to stream PVR recording)
```
recording=<id>
```

#### Bandwidth (required)
```
bw=8000 - 1080p50 FULL HD
bw=4999 - 1080p25 FULL HD
bw=5000 - 720p50 HD
bw=3000 - 720p25 HD
bw=2999 - 576p50 SD
bw=1500 - 432p25 SD
```

#### Platform (required)
```
platform=hls - for: VLC, IPTV Simple
platform=hls5 - for: ffmpeg, tvHeadend
```

#### Additional strings (optional, * can be combined)
```
favorites=true * - create M3U with favorite channels only (Zattoo)
ffmpeg=true * - create pipe:// references to be used for tvHeadend
dolby=true * - use Dolby audio (HLS5 only)
audio2=true * - use 2nd audio stream (HLS5 only)
remove=true - remove recording
```

#### Custom server list
```
fr5-0
fr5-1
fr5-2
fr5-3
fr5-4
fr5-5
zh2-0
zh2-1
zh2-2
zh2-3
zh2-4
zh2-5
zh2-6
zh2-7
zh2-8
zh2-9
zba6-0
zba6-1
zba6-2
1und1-fra1902-1
1und1-fra1902-2
1und1-fra1902-3
1und1-fra1902-4
1und1-hhb1000-1
1und1-hhb1000-2
1und1-hhb1000-3
1und1-hhb1000-4
1und1-dus1901-1
1und1-dus1901-2
1und1-dus1901-3
1und1-dus1901-4
1und1-ess1901-1
1und1-ess1901-2
matterlau1-0
matterlau1-1
matterzrh1-0
matterzrh1-1
```

## Further support
Contact me for support via email: sunsettrack4@gmail.com

FAQ section to follow :-)
