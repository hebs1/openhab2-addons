# Onkyo Binding

This binding integrates the Onkyo AV receivers.

## Introduction

Binding should be compatible with Onkyo AV receivers which support ISCP (Integra Serial Control Protocol) over Ethernet (eISCP).

## Supported Things

This binding supports only one thing: The Onkyo AV Receiver.  All supported Onkyo devices are registered as an audio sink in the framework.

## Discovery

This binding can discover the supported Onkyo AV Receivers. At the moment only the following models are supported:

-   TX-NR414
-   TX-NR509
-   TX-NR515
-   TX-NR525
-   TX-NR535
-   TX-NR555
-   TX-NR535
-   TX-NR616
-   TX-NR626
-   TX-NR636
-   TX-NR646
-   TX-NR656
-   TX-NR717
-   TX-NR727
-   TX-NR737
-   TX-NR747
-   TX-NR818
-   TX-NR828
-   TX-NR838

This binding also discover the supported newer Pioneer AV Reveicers (since 2015)

-   VSX-1131

## Binding Configuration

The binding can auto-discover the Onkyo AVRs present on your local network.
The auto-discovery is enabled by default.
To disable it, you can create a file in the services directory called onkyo.cfg with the following content:

```text
org.openhab.onkyo:enableAutoDiscovery=false
```

This configuration parameter only controls the Onkyo AVR auto-discovery process, not the openHAB auto-discovery.
Moreover, if the openHAB auto-discovery is disabled, the Onkyo AVR auto-discovery is disabled too.


The binding has the following configuration options, which can be set for "binding:onkyo":

| Parameter   | Name         | Description                                                              | Required |
|-------------|--------------|--------------------------------------------------------------------------|----------|
| callbackUrl | Callback URL | URL to use for playing notification sounds, e.g. <http://192.168.0.2:8080> | no       |

## Thing Configuration

The Onkyo AVR thing requires the ip address and the port to access it on.
In the code `avr-livingroom` refers to the user defined unique id of your Onkyo device. A second device could be called avr2.
In the thing file, this looks e.g. like

Model specific

```text
onkyo:TX-NR818:avr-livingroom [ipAddress="192.168.1.100", port=60128]
```

or

Generic model

```text
onkyo:onkyoAVR:avr-livingroom [ipAddress="192.168.1.100", port=60128]
```

Optionally you can specify the refresh interval by refreshInterval parameter.

```text
onkyo:onkyoAVR:avr-livingroom [ipAddress="192.168.1.100", port=60128, refreshInterval=30]
```

Maximum volume level can also be configured by volumeLimit parameter.
This prevent setting receiver volume level too high, which could damage your speakers or receiver.

```text
onkyo:onkyoAVR:avr-livingroom [ipAddress="192.168.1.100", port=60128, volumeLimit=50]
```

Binding then automatically scale the volume level in both directions (100% = 50 = 100%).

Newer Pioneer AV Reveicers (since 2015) have volume range from decimal 0 to 200 (Hex 00 to C8) in steps of 0.5dB.
(e.g. Pioneer VSX-1131 volume range is -82dB to 0dB -> decimal 0 to 164; Hex 00 to A4)
Maximum volume level can be configured by volumedbLimit parameter.
This prevent setting receiver volume level too high, which could damage your speakers or receiver.

```text
onkyo:onkyoAVR:avr-livingroom [ipAddress="192.168.1.100", port=60128, volumedbLimit=-20]
```

Binding then automatically scale the max volume level to -20dB.

## Channels

The Onkyo AVR supports the following channels (some channels are model specific):

| Channel Type ID           | Item Type | Description                                                                                                      |
|---------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| zone1#power               | Switch    | Power on/off your device                                                                                         |
| zone1#mute                | Switch    | Mute/unmute zone 1                                                                                               |
| zone1#input               | Number    | The input for zone 1                                                                                             |
| zone1#volume              | Dimmer    | Volume of zone 1                                                                                                 |
| zone1#volumedb            | Number    | Volume (dB) of zone 1                                                                                            |
| zone2#power               | Switch    | Power on/off zone 2                                                                                              |
| zone2#mute                | Switch    | Mute/unmute zone 2                                                                                               |
| zone2#input               | Number    | The input for zone 2                                                                                             |
| zone2#volume              | Dimmer    | Volume of zone 2                                                                                                 |
| zone2#volumedb            | Number    | Volume (dB) of zone 2                                                                                            |
| zone3#power               | Switch    | Power on/off zone 3                                                                                              |
| zone3#mute                | Switch    | Mute/unmute zone 3                                                                                               |
| zone3#input               | Number    | The input for zone 3                                                                                             |
| zone3#volume              | Dimmer    | Volume of zone 3                                                                                                 |
| zone3#volumedb            | Number    | Volume (dB) of zone 3                                                                                            |
| player#control            | Player    | Control the Zone Player, e.g.  play/pause/next/previous/ffward/rewind (available if playing from Network or USB) |
| player#title              | String    | Title of the current song (available if playing from Network or USB)                                             |
| player#album              | String    | Album name of the current song (available if playing from Network or USB)                                        |
| player#artist             | String    | Artist name of the current song (available if playing from Network or USB)                                       |
| player#currentPlayingTime | String    | Current playing time of the current song (available if playing from Network or USB)                              |
| player#listenmode         | Number    | Current listening mode e.g. Stereo, 5.1ch Surround,..                                                            |
| player#playuri            | String    | Plays the URI provided to the channel                                                                            |
| player#albumArt           | Image     | Image of the current album art of the current song                                                               |
| player#albumArtUrl        | String    | Url to the current album art of the current song                                                                 |
| netmenu#title             | String    | Title of the current NET service                                                                                 |
| netmenu#control           | String    | Control the USB/Net Menu, e.g. Up/Down/Select/Back/PageUp/PageDown/Select&lsqb0-9&rsqb                                   |
| netmenu#selection         | Number    | The number of the currently selected USB/Net Menu entry (0-9)                                                    |
| netmenu#item0             | String    | The text of USB/Net Menu entry 0                                                                                 |
| netmenu#item1             | String    | The text of USB/Net Menu entry 1                                                                                 |
| netmenu#item2             | String    | The text of USB/Net Menu entry 2                                                                                 |
| netmenu#item3             | String    | The text of USB/Net Menu entry 3                                                                                 |
| netmenu#item4             | String    | The text of USB/Net Menu entry 4                                                                                 |
| netmenu#item5             | String    | The text of USB/Net Menu entry 5                                                                                 |
| netmenu#item6             | String    | The text of USB/Net Menu entry 6                                                                                 |
| netmenu#item7             | String    | The text of USB/Net Menu entry 7                                                                                 |
| netmenu#item8             | String    | The text of USB/Net Menu entry 8                                                                                 |
| netmenu#item9             | String    | The text of USB/Net Menu entry 9                                                                                 |

## Input Source Mapping

Here after are the ID values of the input sources:

-   00: DVR/VCR
-   01: SATELLITE/CABLE
-   02: GAME
-   03: AUX
-   04: GAME
-   05: PC
-   16: BLURAY/DVD
-   32: TAPE1
-   33: TAPE2
-   34: PHONO
-   35: CD
-   36: FM
-   37: AM
-   38: TUNER
-   39: MUSICSERVER
-   40: INTERNETRADIO
-   41: USB
-   42: USB_BACK
-   43: NETWORK
-   45: AIRPLAY
-   48: MULTICH
-   50: SIRIUS

## Item Configuration

demo.items

```java
Switch avrLrZ1_Power    "Power"       <switch>      { channel="onkyo:onkyoAVR:avr-livingroom:zone1#power" }
Switch avrLrZ1_Mute     "Mute"        <soundvolume> { channel="onkyo:onkyoAVR:avr-livingroom:zone1#mute" }
Number avrLrZ1_Input    "Input [%s]"  <text>        { channel="onkyo:onkyoAVR:avr-livingroom:zone1#input" }
Dimmer avrLrZ1_Volume   "Volume [%d]" <soundvolume> { channel="onkyo:onkyoAVR:avr-livingroom:zone1#volume" }
Number avrLrZ1_Volumedb "Volume [%.1f dB]" <soundvolume> { channel="onkyo:onkyoAVR:avr-livingroom:zone1#volumedb" }

Switch avrLrZ2_Power    "Power [%s]"  <switch>      { channel="onkyo:onkyoAVR:avr-livingroom:zone2#power" }
Switch avrLrZ2_Mute     "Mute [%s]"                 { channel="onkyo:onkyoAVR:avr-livingroom:zone2#mute" }
Number avrLrZ2_Input    "Input [%s]"  <text>        { channel="onkyo:onkyoAVR:avr-livingroom:zone2#input" }
Dimmer avrLrZ2_Volume   "Volume [%s]" <soundvolume> { channel="onkyo:onkyoAVR:avr-livingroom:zone2#volume" }
Number avrLrZ2_Volumedb "Volume [%.1f dB]" <soundvolume> { channel="onkyo:onkyoAVR:avr-livingroom:zone2#volumedb" }

Player avrLrPlayer_Control            "Control"                 <text>        { channel="onkyo:onkyoAVR:avr-livingroom:player#control" }
String avrLrPlayer_Title              "Title [%s]"              <text>        { channel="onkyo:onkyoAVR:avr-livingroom:player#title" }
String avrLrPlayer_Album              "Album [%s]"              <text>        { channel="onkyo:onkyoAVR:avr-livingroom:player#album" }
String avrLrPlayer_Artist             "Artist [%s]"             <parents_2_5> { channel="onkyo:onkyoAVR:avr-livingroom:player#artist" }
String avrLrPlayer_CurrentPlayingTime "CurrentPlayingTime [%s]" <clock>       { channel="onkyo:onkyoAVR:avr-livingroom:player#currentPlayingTime" }
Number avrLrPlayer_Listenmode         "Listenmode [%d]"         <text>        { channel="onkyo:onkyoAVR:avr-livingroom:player#listenmode" }
String avrLrPlayer_PlayURI            "PlayURI [%s]"            <text>        { channel="onkyo:onkyoAVR:avr-livingroom:player#playuri" }
Image  avrLrPlayer_AlbumArt           "AlbumArt [%s]"           <text>        { channel="onkyo:onkyoAVR:avr-livingroom:player#albumArt" }
String avrLrPlayer_AlbumArtUrl        "AlbumArtUrl [%s]"        <text>        { channel="onkyo:onkyoAVR:avr-livingroom:player#albumArtUrl" }

String avrLrNet_Title     "Title [%s]"     <text>   { channel="onkyo:onkyoAVR:avr-livingroom:netmenu#title" }
String avrLrNet_Control   "Control"        <text>   { channel="onkyo:onkyoAVR:avr-livingroom:netmenu#control" }
Number avrLrNet_Selection "Selection [%d]" <text>   { channel="onkyo:onkyoAVR:avr-livingroom:netmenu#selection" }
String avrLrNet_Item0     "Item0 [%s]"     <text>   { channel="onkyo:onkyoAVR:avr-livingroom:netmenu#item0" }
String avrLrNet_Item1     "Item1 [%s]"     <text>   { channel="onkyo:onkyoAVR:avr-livingroom:netmenu#item1" }
String avrLrNet_Item2     "Item2 [%s]"     <text>   { channel="onkyo:onkyoAVR:avr-livingroom:netmenu#item2" }
String avrLrNet_Item3     "Item3 [%s]"     <text>   { channel="onkyo:onkyoAVR:avr-livingroom:netmenu#item3" }
String avrLrNet_Item4     "Item4 [%s]"     <text>   { channel="onkyo:onkyoAVR:avr-livingroom:netmenu#item4" }
String avrLrNet_Item5     "Item5 [%s]"     <text>   { channel="onkyo:onkyoAVR:avr-livingroom:netmenu#item5" }
String avrLrNet_Item6     "Item6 [%s]"     <text>   { channel="onkyo:onkyoAVR:avr-livingroom:netmenu#item6" }
String avrLrNet_Item7     "Item7 [%s]"     <text>   { channel="onkyo:onkyoAVR:avr-livingroom:netmenu#item7" }
String avrLrNet_Item8     "Item8 [%s]"     <text>   { channel="onkyo:onkyoAVR:avr-livingroom:netmenu#item8" }
String avrLrNet_Item9     "Item9 [%s]"     <text>   { channel="onkyo:onkyoAVR:avr-livingroom:netmenu#item9" }
```

## Sitemap Configuration

demo.sitemap

```perl
sitemap demo label="Onkyo AVR"
{
    Frame label="Zone1" {
        Switch    item=avrLrZ1_Power
        Switch    item=avrLrZ1_Mute
        Selection item=avrLrZ1_Input  mappings=[ 0='DVR/VCR', 1='SATELLITE/CABLE', 2='GAME', 3='AUX', 4='GAME', 5='PC', 16='BLURAY/DVD', 32='TAPE1', 33='TAPE2', 34='PHONO', 35='CD', 36='FM', 37='AM', 38='TUNER', 39='MUSICSERVER', 40='INTERNETRADIO', 41='USB', 42='USB_BACK', 43='NETWORK', 45='AIRPLAY', 48='MULTICH', 50='SIRIUS' ]
        Slider    item=avrLrZ1_Volume
		Setpoint  item=avrLrZ1_Volumedb label="Volume [%.1f dB]" minValue=-82 maxValue=0 step=0.5
    }

    Frame label="Zone 2" {
        Switch    item=avrLrZ2_Power
        Switch    item=avrLrZ2_Mute
        Selection item=avrLrZ2_Input  mappings=[ 0='DVR/VCR', 1='SATELLITE/CABLE', 2='GAME', 3='AUX', 4='GAME', 5='PC', 16='BLURAY/DVD', 32='TAPE1', 33='TAPE2', 34='PHONO', 35='CD', 36='FM', 37='AM', 38='TUNER', 39='MUSICSERVER', 40='INTERNETRADIO', 41='USB', 42='USB_BACK', 43='NETWORK', 45='AIRPLAY', 48='MULTICH', 50='SIRIUS' ]
        Slider    item=avrLrZ2_Volume
		Setpoint  item=avrLrZ2_Volumedb label="Volume [%.1f dB]" minValue=-82 maxValue=0 step=0.5
    }

    Frame label="Player" {
        Default   item=avrLrPlayer_Control
        Text      item=avrLrPlayer_Title
        Text      item=avrLrPlayer_Album
        Text      item=avrLrPlayer_Artist
        Text      item=avrLrPlayer_CurrentPlayingTime
        Selection item=avrLrPlayer_Listenmode mappings=[0=Stereo, 1=Direct, 2=Surround, 15=Mono, 31="Whole House", 66="THX Cinema"]
    }
    Frame label="NetMenu" {
        Text      item=avrLrNet_Title
        Selection item=avrLrNet_Control   mappings=[ Up='Up', Down='Down', Select='Select', Back='Back', PageUp='PageUp', PageDown='PageDow', Select0='Select0', Select1='Select1', Select2='Select2', Select3='Select3', Select4='Select4', Select5='Select5', Select6='Select6', Select7='Select7', Select8='Select8', Select9='Select9' ]
        Selection item=avrLrNet_Selection mappings=[ 0='Item0', 1='Item1', 2='Item2', 3='Item3', 4='Item4', 5='Item5', 6='Item6', 7='Item7', 8='Item8', 9='Item9' ]
        Text      item=avrLrNet_Item0
        Text      item=avrLrNet_Item1
        Text      item=avrLrNet_Item2
        Text      item=avrLrNet_Item3
        Text      item=avrLrNet_Item4
        Text      item=avrLrNet_Item5
        Text      item=avrLrNet_Item6
        Text      item=avrLrNet_Item7
        Text      item=avrLrNet_Item8
        Text      item=avrLrNet_Item9
    }
}
```

## Audio Support

All supported Onkyo AVRs are registered as an audio sink in the framework.
Audio streams are sent to the `playuri` channel.
