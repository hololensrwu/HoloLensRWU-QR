---
page_type: sample
name: QR code tracking in Unity
description: This sample shows you how to use QR Codes in Unity projects using a HoloLens or Windows Mixed Reality immersive headset.
languages:
- csharp
products:
- windows-mixed-reality
- hololens
---

# QR code tracking in Unity 

![License](https://img.shields.io/badge/license-MIT-green.svg)

Supported Unity versions | Built with XR configuration
:-----------------: | :----------------: |
Unity 2020 or higher | Windows XR Plugin |

This sample shows you how to use QR Codes in Unity projects using a HoloLens or Windows Mixed Reality immersive headset. Covered features include displaying a holographic square over QR codes and associated data such as:
* GUID
* Physical size
* Timestamp
* Decoded data

## Contents

| File/folder | Description |
|-------------|-------------|
| `Sample/Assets` | Unity assets, scenes, prefabs, and scripts. |
| `Sample/Packages` | Project manifest and packages list. |
| `Sample/ProjectSettings` | Unity asset setting files. |
| `Sample/UserSettings` | Generated user settings from Unity. |
| `.gitignore` | Define what to ignore at commit time. |
| `README.md` | This README file. |
| `LICENSE`   | The license for the sample. |

## Prerequisites

* Install the [latest Mixed Reality tools](https://docs.microsoft.com/windows/mixed-reality/develop/install-the-tools?tabs=unity)
* Install the [recommended Unity version](https://docs.microsoft.com/windows/mixed-reality/develop/install-the-tools?tabs=unity#install-your-engine-of-choice) 
* Download the [QR code NuGet package](https://www.nuget.org/Packages/Microsoft.MixedReality.QR)
* **For Windows Mixed Reality headsets**: QR code tracking on desktop PCs is only supported on Windows 10 Version 2004 and higher.

## Setup

1. Clone or download this sample repository.
2. Open the **Sample** folder in Unity Hub and launch the project

## Running the sample

1. Hit **Play** in the Unity editor
2. In the HoloLens connected to Unity or with Remoting, a QR pops up in the scene in front of the user
3. When the QR code is read, a rectangle object is placed at the QR code coordinates 

## Key concepts

https://docs.microsoft.com/windows/mixed-reality/develop/platform-capabilities-and-apis/qr-code-tracking

`QRCode.cs` - This script is attached to the QR code object and populates the text displayed in the scene with the QR code properties on `Start`.
`QRCodesManager.cs` - This is the main class that handles the QR SDK, including: 
* Loading the plugin
* Checking if tracking is supported
* Requesting access to the webcame
* Adding event listeners for new, updated, and removed QR codes
* Handling events through callback functions
* Starting and stopping QR code tracking
* Maintaining a local list of QR codes

`QRCodesSetup.cs` - Kicks off the QR code manager tracking functionality in `QRCodesManager`.

`QRCodesVisualizer.cs` - Handles all QR code visualizing in the scene and instantiates all QR codes in the local list kept in `QRCodesManager`.

`SpatialGraphNodeTracker.cs` - This script is attached to the QR code object and transforms real-world QR code coordinates into the Unity coordinate system. The script also places the virtual QR code in the scene at the same location as the real-world QR code.

`SpatialGraphNode.cs` - This script is abstracting the tracking of a spatial graph static node, which represents the tracking information of QR code in a GUID id.

## OpenXR sample
To view the OpenXR version of the QRCode tracking on HoloLens 2, please checkout the "openxr" branch of this sample repro,  https://github.com/microsoft/MixedReality-QRCode-Sample/tree/OpenXR.  
You can also inspect how to make modifications to existing QRCode Unity project to support OpenXR from this pull request: https://github.com/microsoft/MixedReality-QRCode-Sample/pull/18


## API Reference

https://docs.microsoft.com/windows/mixed-reality/develop/platform-capabilities-and-apis/qr-code-tracking#qr-api-reference

## Best practices 

* **Quiet zones**: To be read correctly, QR codes require a margin around all sides of the code. This margin must not contain any printed content and should be four modules (a single black square in the code) wide. 
    * The [QR spec](https://www.qrcode.com/howto/code.html) contains more information about quiet zones.

* **Lighting and backdrop**: If the backdrop to the code is dark, try a black on gray code if your detection rate is low. If the backdrop is relatively light, a regular code should work fine.

* **Size**: Windows Mixed Reality devices don't work with QR codes with sides smaller than 5 cm each. For QR codes between 5 cm and 10-cm length sides, you must be fairly close to detect the code. It will also take longer to detect codes at this size. 
    * The exact time to detect codes depends not only on the size of the QR codes, but how far you're away from the code. Moving closer to the code will help offset issues with size.

* **Distance and angular position**: The tracking cameras can only detect a certain level of detail. For small codes - < 10 cm along the sides - you must be fairly close. For a version 1 QR code varying from 10 cm to 25 cm wide, the minimum detection distance ranges from 0.15 meters to 0.5 meters.
    * The detection distance for size increases linearly, but also depends on QR version or module size. The higher the version, the smaller the modules, which can only be detected from a closer position. You can also try micro QR codes if you want the distance of detection to be longer. QR detection works with a range of angles += 45 deg to ensure we have proper resolution to detect the code.

## Next steps

* [QR code tracking](https://docs.microsoft.com/windows/mixed-reality/develop/platform-capabilities-and-apis/qr-code-tracking#quiet-zones-around-qr-codes)
* [World locking and spatial anchors](https://docs.microsoft.com/windows/mixed-reality/design/spatial-anchors-in-unity)
* [HoloLens environment considerations](https://docs.microsoft.com/hololens/hololens-environment-considerations)
