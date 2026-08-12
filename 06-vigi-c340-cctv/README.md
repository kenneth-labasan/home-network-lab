# TP-Link VIGI C340 PoE CCTV Installation and Configuration
## Overview
This lab documents the installation and configuration of a **TP-Link VIGI C340 PoE security camera** on my home network.

The camera was connected through a PoE switch, configured for continuous recording using a **128 GB microSD card**, integrated with the VIGI mobile application, and tested for local recording playback and download through a Windows PC.

One of the main objectives was to determine whether recordings stored on the microSD card could be copied to another device **without physically removing the microSD card from the camera**.

This was successfully accomplished using the **VIGI PC Client over the local network**.

## Lab Objectives
- Prepare and terminate the Ethernet cable for the camera.
- Install the C340 using Power over Ethernet (PoE).
- Discover and initialize the camera.
- Configure the 128 GB microSD card.
- Configure 24/7 continuous recording.
- Optimize video and audio settings.
- Configure date and time synchronization.
- Upgrade the camera firmware.
- Verify the camera's IPv4 configuration.
- Practice DHCP address reservation on the ER605.
- Bind the camera to a TP-Link ID.
- Configure and test the VIGI mobile application.
- Test local web access.
- Test recorded video playback.
- Download recordings without removing the microSD card.
- Compare the different VIGI management applications.
- Troubleshoot local PC Client connectivity.

## Equipment

### Hardware
- TP-Link VIGI C340 PoE Camera
- 128 GB microSD card
- TP-Link ER605 Gateway
- TP-Link TL-SG108PE PoE Switch
- Custom Ethernet cable
- RJ45 connectors
- RJ45 crimping tool
- Windows PC/laptop
- Smartphone

### Software
- VIGI Config Tool
- VIGI Security Manager / VMS
- VIGI PC Client
- VIGI mobile application
- Web browser
- TP-Link ER605 web management interface

# 1. Ethernet Cable Preparation
A custom Ethernet cable was prepared to connect the VIGI C340 to the PoE switch.

The Ethernet cable was terminated using the **T568B wiring standard**.

### T568B Pin Order
1. White/Orange
2. Orange
3. White/Green
4. Blue
5. White/Blue
6. Green
7. White/Brown
8. Brown

After termination, one end of the cable was connected to the PoE switch.

### Problem Encountered - Weatherproof Ethernet Connector
After initially terminating the Ethernet cable, I discovered that the VIGI C340 includes a **protective/weatherproof Ethernet connector housing** for the camera's network connection.

The weatherproof connector components needed to be placed onto the Ethernet cable **before installing the RJ45 connector**.

Because I had already terminated the Ethernet cable, the RJ45 connector prevented the weatherproof housing from being installed correctly.

### Resolution
I:

1. Cut off the previously installed RJ45 connector.
2. Slid the C340 weatherproof connector components onto the Ethernet cable in the correct order.
3. Arranged the Ethernet conductors again using the T568B standard.
4. Installed and crimped a new RJ45 connector.
5. Connected the Ethernet cable to the camera.
6. Assembled the weatherproof housing around the camera's Ethernet connection.
7. Connected the other end to the PoE switch.
8. Verified that the camera received both power and network connectivity.

### Lesson Learned
Before terminating a custom Ethernet cable for an outdoor PoE camera, inspect the camera's weatherproof connector assembly first.

If the weatherproof components cannot pass over an installed RJ45 connector, they must be placed onto the Ethernet cable **before the RJ45 connector is terminated**.

This prevents unnecessary cutting and re-termination of the cable.

# 2. Power over Ethernet Connection
The VIGI C340 supports **Power over Ethernet (PoE)**.

The camera was connected to a PoE-capable port on the TP-Link TL-SG108PE switch.

This allowed a single Ethernet cable to provide:

- Electrical power
- Network connectivity

No separate power adapter was required for the camera.

### Connection Path
```text
ER605 Gateway
      |
      |
TL-SG108PE PoE Switch
      |
      | Ethernet + PoE
      |
VIGI C340
```

The camera powered on successfully after being connected to the PoE switch.

# 3. Camera Discovery
The **VIGI Config Tool** was used to discover the camera on the local network.

The C340 appeared automatically.

Initial information included:

| Setting | Value |
|---|---|
| Model | VIGI C340 |
| IPv4 Address | 192.168.0.107 |
| Status | Uninitialized |

This confirmed that communication between the camera and the local network was working.

# 4. Camera Initialization
The camera initially appeared as:

```text
Uninitialized
```

The initialization process was started through the VIGI software.

During initialization:

1. An administrator password was created.
2. Country/Region was set to Philippines.
3. Time zone was configured for UTC+08:00.
4. Language was configured as English.
5. Power-line frequency was configured.
6. Password protection settings were completed.

After initialization, the camera changed to:

```text
Online
```

This confirmed that the C340 was successfully initialized.

# 5. microSD Card Initialization
A **128 GB microSD card** was installed in the C340.

The camera announced that the SD card needed to be formatted.

Under:

```text
Storage
└── Storage Management
```

the microSD card initially appeared as:

```text
Status: Uninitialized
Capacity: 0B / 0B
```

The microSD card was formatted through the camera management interface.

After formatting, the camera successfully recognized the storage.

# 6. Storage Configuration
The following storage settings were configured:

| Setting | Configuration |
|---|---|
| Storage | 128 GB microSD |
| Record Stream | Main Stream |
| Circular Write | Enabled |
| Record Audio | Enabled |
| Recording Expiration | Disabled |

## Circular Write
Circular Write allows the camera to automatically overwrite the **oldest recordings when the microSD card becomes full**.

This means that manual deletion is normally unnecessary.

The camera can continue recording as long as the microSD card remains healthy.

# 7. Recording Schedule
The recording schedule was configured for:

```text
Continuous Recording
24 Hours
7 Days Per Week
```

Continuous recording was enabled for:

- Monday
- Tuesday
- Wednesday
- Thursday
- Friday
- Saturday
- Sunday

This allows the camera to continuously store footage on the microSD card.

Motion detection was also enabled so detected events could be identified separately during playback.

# 8. Video Configuration
The Main Stream video settings were configured for a balance between image quality and storage usage.

| Setting | Configuration |
|---|---|
| Stream Type | Main Stream |
| Resolution | 2560 × 1440 |
| Frame Rate | 15 FPS |
| Bit Rate Type | VBR |
| Maximum Bit Rate | 3584 Kbps |
| Video Encoding | H.265 |
| Smart Coding | Enabled |
| Image Quality | Medium |

## H.265 Video Encoding
H.265 was selected instead of H.264.

H.265 provides more efficient video compression, allowing the camera to maintain good video quality while reducing storage requirements.

This is particularly useful because the camera records continuously to a **128 GB microSD card**.

## Frame Rate
The frame rate was changed from:

```text
25 FPS
```

to:

```text
15 FPS
```

For general surveillance, 15 FPS provides sufficiently smooth video while reducing storage consumption compared with 25 FPS.

## Variable Bit Rate
The Bit Rate Type was configured as:

```text
VBR
```

VBR stands for **Variable Bit Rate**.

Instead of constantly using the same amount of data, the camera can use:

- Less data when the scene is relatively static.
- More data when additional image detail or movement is present.

This helps improve storage efficiency.

# 9. Audio Configuration
Audio recording was enabled.

The following settings were used:

| Setting | Configuration |
|---|---|
| Output Volume | 80 |
| System Volume | 100 |
| Audio Coding | G711alaw |
| Audio Input | MicIn |
| Input Volume | 80 |
| Noise Filtering | Enabled |
| Audio Switch | Enabled |

Noise filtering was enabled to help reduce unnecessary environmental noise.

The microphone input volume can be adjusted later after the camera is permanently mounted and tested in its actual environment.

# 10. Advanced Stream Settings
The Advanced Stream settings were reviewed.

## Video/Audio DSCP
```text
Video/Audio DSCP: 0
```

The default value was retained because no special Quality of Service prioritization was required.

DSCP stands for **Differentiated Services Code Point** and can be used to prioritize specific types of network traffic.

## SRTP
```text
SRTP: Disabled
```

Secure Real-time Transport Protocol was left disabled.

Enabling SRTP encrypts the video stream but can introduce compatibility issues with some third-party clients and Network Video Recorders.

It was not required for the current lab.

# 11. Date and Time Configuration
Accurate timestamps are important for surveillance recordings.

The following settings were verified:

| Setting | Configuration |
|---|---|
| Time Zone | UTC+08:00 |
| Time Settings | NTP |
| Server Address | Auto |
| Synchronization Interval | 60 Minutes |

NTP stands for **Network Time Protocol**.

NTP allows the camera to periodically synchronize its clock automatically.

The Philippines does not currently use Daylight Saving Time.

# 12. Firmware Upgrade
During configuration, a newer firmware version was detected.

The C340 was upgraded to:

```text
2.2.3 Build 260624 Rel.34889n
```

During the upgrade:

- The Ethernet cable remained connected.
- The PoE switch remained powered.
- The camera was not manually restarted.
- Power was not interrupted.

The camera automatically restarted after the upgrade.

The new firmware version was then verified successfully.

# 13. Network Configuration
The C340 received its IPv4 configuration through DHCP.

The following configuration was observed:

| Setting | Value |
|---|---|
| IPv4 Mode | Dynamic IP |
| IPv4 Address | 192.168.0.107 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.0.1 |
| Preferred DNS | 192.168.0.1 |
| IPv6 | Disabled |

The ER605 at:

```text
192.168.0.1
```

acts as the gateway for the camera.

# 14. DHCP Address Reservation
The TP-Link ER605 management interface was opened.

The following location was used:

```text
Network
└── LAN
    └── Address Reservation
```

The C340 was identified using its current DHCP address and MAC address.

This was my **first practical experience configuring a DHCP reservation on a physical network**.

## Dynamic IP vs Static IP vs DHCP Reservation
### Dynamic IP
With normal DHCP, the DHCP server automatically provides an available IP address.

The address may potentially change later.

### Static IP
With a static IP address, the network configuration is manually entered directly into the device.

### DHCP Reservation
With DHCP reservation, the device continues requesting its configuration through DHCP.

However, the DHCP server recognizes the device using its **MAC address** and consistently provides the reserved IP address.

This provides predictable addressing while still allowing the network configuration to remain centrally managed.

For the current installation, the existing:

```text
192.168.0.107
```

address was retained.

The CCTV addressing scheme can be reorganized later if additional cameras are installed.

# 15. TP-Link ID and Cloud Service

The camera initially displayed:

```text
This device is not bound.
```

The C340 was then bound to a TP-Link ID.

The VIGI mobile application was used to scan the QR code displayed by the camera management interface.

After binding, the camera became available through the VIGI mobile application.

# 16. VIGI Mobile Application
The following functions were tested successfully:

- Live View
- Playback
- Motion event playback
- Return from Playback to Live View
- Remote camera access
- Recording download

Downloading recordings through the VIGI mobile application was straightforward.

No significant problems were encountered when downloading footage through the mobile application.

# 17. Local Web Access
The camera was also accessed directly through its IPv4 address:

```text
https://192.168.0.107
```

The web interface provided access to:

- Live View
- Playback
- Camera settings

Recorded footage stored on the microSD card could be played through the local network.

Motion events were also visible in the playback interface.

This confirmed that the microSD recordings were accessible across the network without physically removing the card.

# 18. FTP Investigation
While searching for a method to copy recordings to the PC, the camera's FTP configuration was investigated.

The following settings were available:

```text
Network
└── FTP Settings
    ├── Server
    └── Upload
```

It was determined that this functionality is designed primarily for the **camera to upload data to an external FTP server**.

It does not provide normal direct browsing of existing microSD recordings from the PC.

FTP was therefore not required for the intended backup workflow.

## Lesson Learned
Not every file-transfer feature provides direct access to stored files.

The FTP functionality in this configuration is an **upload destination for the camera**, rather than a method of mounting or browsing the microSD card as a network drive.

# 19. Understanding the VIGI Software
One challenge during the lab was determining which VIGI application should be used for each task.

The following applications were encountered:

## VIGI Config Tool
Useful for:

- Discovering VIGI devices
- Initializing devices
- Basic configuration
- Network configuration
- Firmware management

## VIGI Security Manager / VMS
Useful for:

- Camera management
- Live monitoring
- Configuration
- Surveillance management

## VIGI PC Client
Useful for:

- Live View
- Playback
- Local camera access
- Recording management
- Downloading/exporting recorded footage

Although these applications share several functions, the **VIGI PC Client provided the easiest PC workflow for downloading recordings from the camera**.

# 20. Problem Finding the VIGI PC Client
Initially, I could not find the VIGI PC Client on the VIGI download page.

## Cause
The website redirected me to the regional version of the VIGI support/download page.

The regional page did not list the PC Client among the available applications.

## Resolution
Instead of using the regional redirect, I accessed another official VIGI download page that listed the PC Client.

I was then able to download and install the application successfully.

## Lesson Learned
Software availability can differ between regional vendor support websites.

If an expected utility is missing from an official regional page, other official vendor support/download pages should be checked before assuming that the application is unavailable.

# 21. VIGI PC Client Offline Problem
After installing VIGI PC Client, the C340 was detected.

The application correctly displayed information including:

- Device name
- VIGI C340 model
- IP address
- MAC address
- Firmware version

However, the camera showed:

```text
Status: Offline
```

Live View also returned an error indicating that the device was offline.

Re-adding the camera did not resolve the problem.

# 22. Troubleshooting the Offline Status
Even though VIGI PC Client reported the camera as offline, other evidence showed that the camera itself was functioning correctly.

The following were already working:

- Camera received PoE power.
- Camera had an IPv4 address.
- ER605 could see the camera.
- Direct web access worked.
- VIGI mobile Live View worked.
- Mobile playback worked.
- microSD recordings were available.

Therefore, the camera itself was **not actually offline from the network**.

This suggested that the problem was related to the VIGI PC Client connection or operating mode rather than the physical network.

# 23. Resolution - Use Without Login
VIGI PC Client was switched to:

```text
Use Without Login
```

After switching to local access, the PC Client successfully communicated with the C340 through the local network.

The camera became accessible for playback and recording downloads.

## Important Troubleshooting Lesson
An application reporting a device as **Offline** does not automatically mean the physical device or network connection is down.

Troubleshooting should verify each layer independently.

In this case:

```text
Physical connection        WORKING
PoE power                  WORKING
Ethernet connection        WORKING
IPv4 addressing            WORKING
Gateway communication      WORKING
Web interface              WORKING
Mobile application         WORKING
PC Client account mode     PROBLEM
```

The failure existed at the application/access layer.

Switching VIGI PC Client to local operation using **Use Without Login** resolved the issue.

# 24. Downloading Recordings Without Removing the microSD Card
One of the main goals of the project was to determine whether recordings could be copied from the camera without physically removing the microSD card.

This was successfully accomplished.

Using:
```text
VIGI PC Client
      ↓
Use Without Login
      ↓
Playback
      ↓
Download
```

recordings stored on the C340 microSD card could be downloaded directly to the Windows PC.

### Recording Transfer Path
```text
VIGI C340
    ↓
128 GB microSD
    ↓
Ethernet
    ↓
TL-SG108PE PoE Switch
    ↓
Local Network
    ↓
Windows PC
    ↓
VIGI PC Client
    ↓
Downloaded Recording
```

The microSD card therefore **does not need to be removed from the camera to back up recordings**.

This will be particularly useful after the camera is permanently installed in a difficult-to-reach location.

---

# 25. Mobile vs PC Recording Download
Both methods were tested.

## VIGI Mobile Application
The mobile application provided an easily accessible Download function.

This method is convenient for:

- Short clips
- Quick incident review
- Saving footage directly to a phone

No significant problems were encountered with mobile downloads.

## VIGI PC Client
The PC Client is more appropriate when:

- Recordings need to be stored on a PC.
- Larger recordings need to be downloaded.
- Footage will be transferred to external storage.
- Multiple recordings need to be archived.

For my intended backup workflow, the **VIGI PC Client is the preferred method**.

# Problems Encountered and Resolutions
| Problem | Cause | Resolution |
|---|---|---|
| Weatherproof connector could not be installed | RJ45 connector had already been terminated before installing the weatherproof components | Cut the RJ45 connector, installed the weatherproof components first, and re-terminated the cable |
| microSD card requested formatting | New/uninitialized microSD card | Formatted through Storage Management |
| Difficulty finding PC recording download | Initially searching through the wrong VIGI interfaces/functions | Installed and used VIGI PC Client |
| FTP appeared potentially useful for copying recordings | FTP functionality was initially misunderstood | Determined that FTP was for camera uploads rather than normal microSD browsing |
| VIGI PC Client was difficult to find | Regional VIGI download page did not list the application | Used another official VIGI download page without the regional redirect |
| C340 appeared Offline in VIGI PC Client | PC Client connection/account mode | Switched to **Use Without Login** |
| Re-adding the C340 did not resolve Offline status | Device registration was not the underlying issue | Changed the PC Client access mode instead |
| Needed to copy recordings without removing the microSD card | Physical removal would be inconvenient after mounting | Used VIGI PC Client Playback and Download over the LAN |

# Skills Practiced
This lab provided practical experience with:

- Power over Ethernet
- Ethernet cable termination
- T568B wiring
- RJ45 installation
- Outdoor Ethernet weatherproofing
- IP camera deployment
- Device discovery
- IPv4 addressing
- DHCP
- DHCP reservations
- MAC addresses
- Subnet masks
- Default gateways
- DNS
- Local Area Network communication
- Firmware upgrades
- H.265 video compression
- Variable Bit Rate
- Frame-rate optimization
- Network Time Protocol
- microSD storage management
- Circular recording
- Continuous recording
- Motion detection
- Local versus cloud access
- TP-Link ID device binding
- CCTV playback
- Network-based recording export
- Application-layer troubleshooting

# Key Lessons Learned
## 1. Prepare Weatherproof Components Before Terminating the Cable
Outdoor camera connectors may require weatherproof components to be installed on the cable before the RJ45 connector is crimped.

Always inspect the complete connector assembly before terminating a custom cable.

## 2. DHCP Reservation Provides Predictable Addressing
A DHCP reservation provides the convenience of DHCP while allowing a device to consistently receive the same IP address.

This is useful for infrastructure devices such as:

- Security cameras
- Printers
- Access points
- Servers
- Network appliances

## 3. Similar Management Tools Can Have Different Purposes
VIGI Config Tool, VIGI Security Manager, and VIGI PC Client share some features but are optimized for different tasks.

The correct tool should be selected based on the task rather than assuming every management application provides the same functionality.

## 4. "Offline" Does Not Always Mean a Network Failure
The VIGI PC Client reported the camera as offline even though:

- The camera was powered.
- The camera had an IP address.
- Web access worked.
- Mobile access worked.
- Playback worked.

This demonstrated the importance of identifying **which layer is actually failing** before changing network settings.

## 5. microSD Recordings Can Be Backed Up Over the Network
The 128 GB microSD card does not need to be physically removed to copy recordings.

Footage can be transferred through:

```text
Camera → Ethernet → LAN → PC
```

using VIGI PC Client.

This provides a much more practical backup method after permanent installation.

# Final Result
The TP-Link VIGI C340 was successfully:

- Connected through Power over Ethernet.
- Connected to the existing home network.
- Discovered using VIGI software.
- Initialized.
- Configured with a 128 GB microSD card.
- Configured for 24/7 continuous recording.
- Configured with circular recording.
- Configured with audio recording.
- Configured for 2560 × 1440 video.
- Configured with H.265.
- Configured with Smart Coding.
- Configured for NTP time synchronization.
- Updated to the latest available firmware.
- Configured with DHCP addressing.
- Used to practice DHCP address reservation on the ER605.
- Bound to a TP-Link ID.
- Accessed through the VIGI mobile application.
- Accessed through its local web interface.
- Accessed locally through VIGI PC Client.
- Tested for Live View.
- Tested for recorded playback.
- Tested for motion-event playback.
- Successfully tested for downloading recordings to a PC without removing the microSD card.

# Current Network Path
```text
Internet
   |
   |
TP-Link ER605
192.168.0.1
   |
   |
TL-SG108PE PoE Switch
   |
   | PoE + Ethernet
   |
VIGI C340
192.168.0.107
   |
   |
128 GB microSD
```

# Next Steps
The camera configuration and recording-download workflow have been successfully tested.

The next phase is the **permanent physical installation of the C340**.

After mounting, the following should be configured and tested based on the camera's actual field of view:

- Final camera orientation
- Image rotation
- Motion detection area
- Person detection
- Detection sensitivity
- Smart Event configuration
- Active Defense
- Privacy Mask if required
- Night vision
- Outdoor microphone level
- Daytime recording quality
- Nighttime recording quality
- Final playback test
- Final recording download test

The detection area should be configured **after permanent mounting**, because the camera's field of view will change once it is installed in its final position.

## Lab Status
| Component | Status |
|---|---|
| Camera Configuration | Complete |
| PoE Connectivity | Verified |
| Network Connectivity | Verified |
| 128 GB microSD | Verified |
| Continuous Recording | Verified |
| Motion Detection | Verified |
| Mobile Access | Verified |
| Local Web Access | Verified |
| PC Playback | Verified |
| PC Recording Download | Verified |
| DHCP Reservation Practice | Complete |
| Firmware Upgrade | Complete |
| Permanent Mounting | **Pending** |
| Final Detection Zones | **Pending** |
| Day/Night Testing | **Pending** |