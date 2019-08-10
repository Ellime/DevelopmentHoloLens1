![Banner](https://dl.dropboxusercontent.com/s/o6og0jpfvy47awl/IMG_20190722_113507%20-%20Copy.jpg?dl=0)

Last updated: 8/2/2019

# Intro
This document aims to lessen the challenge of developing for the Microsoft HoloLens by suggesting resources and clarifying areas of confusion. Official guides by Microsoft and unofficial resources are linked and additional notes are included. This document covers the HoloLens 1 and is not entirely applicable to the HoloLens 2.

Currently, with Microsoft halting development on the HoloLens 1 and HoloLens 2 not yet ready, this document serves as an up-to-date resource for mixed reality developers.

Currently this document only covers mixed reality development with Unity, primarily on a Long-Term Support (LTS) stream, and a physical HoloLens 1 device.

Changes and contributors are viewable on [GitHub](https://github.com/Ellime/DevelopmentHoloLens1).

This document is not sponsored by or affiliated with Microsoft, Unity Technologies, or any of their affiliates.


# Environment Setup
Hardware and other specs are listed at [https://docs.microsoft.com/en-us/windows/mixed-reality/install-the-tools](https://docs.microsoft.com/en-us/windows/mixed-reality/install-the-tools).

## Windows
Windows 10 is required to develop for the HoloLens. It is possible to use a virtual machine with a different OS as the host.

Have Developer Mode enabled on your computer under _Settings -> Update and security -> For developers_. Enabling Device Portal and Device Discovery is unnecessary to use the HoloLens with Unity and Visual Studio.


## Unity
Microsoft recommends a Long-Term Support (LTS) version of Unity such as 2018.4.x.

Install any and all versions of Unity you plan on using for HoloLens development with all Windows and Universal Windows Platform (UWP) Build Support modules. Using the Unity Hub application to install Unity allows you to pick modules to add.

## Visual Studio
The “Workloads” for Visual Studio refer to packages to select while installing the app. Workloads can also be added after installing Visual Studio by relaunching its installer and clicking “Modify”.

Visual Studio 2017 can be an optional installation with some Unity versions. If this option was taken, the stand-alone Visual Studio installer needs to be installed to add Workloads.

## Mixed Reality Toolkit
The Mixed Reality Toolkit (MRTK) is just a set of packages to add to a mixed reality project, useful for helping one get started. It is not an installation nor a requirement.

## HoloLens 1 Device
In _Settings -> Update & Security -> For developers_, turn on Developer mode and Device Portal to allow the HoloLens to pair with your computer.

Go to the Windows Store and install the Holographic Remoting Player app. This is needed to pair the HoloLens with your computer over a network. 

Both your computer and the HoloLens must be on the same network to interact with and deploy your project.

## HoloLens 1 Emulator
HyperV needs to be enabled in _Control Panel -> Programs and Features -> Turn Windows features on or off_.

If using a virtual machine for Windows on a different host, see [https://blog.gleitzman.com/post/146912278931/the-almost-perfect-hololens-development](https://blog.gleitzman.com/post/146912278931/the-almost-perfect-hololens-development) for guidance on running the emulator.

# Project Setup and Tutorials

## Project Setup
Quick-start guide for a new project and scenes: [https://docs.microsoft.com/en-us/windows/mixed-reality/configure-unity-project](https://docs.microsoft.com/en-us/windows/mixed-reality/configure-unity-project). Check the recommended Build Settings for your version of Unity.

Recommended Unity project settings for performance: [https://docs.microsoft.com/en-us/windows/mixed-reality/recommended-settings-for-unity](https://docs.microsoft.com/en-us/windows/mixed-reality/recommended-settings-for-unity). These settings are not specifically referred to in most other guides.

Some Microsoft guides use .NET instead of IL2CPP or select “Unity C# Projects” under _Build Settings_, which is disabled if using IL2CPP – this won’t interfere with deploying from Visual Studio. IL2CPP comments out all the C# code and replaces it with C++.
Use IL2CPP when possible as it is more CPU-efficient and the .NET backend is being depreciated. If using .NET, checking “Unity C# Projects” is recommended for debugging.

## Build Settings
Different Unity versions display different options in the Build Settings window. The ones that remain consistent are:
- Select “Universal Windows Platform”.
- Set Build Type to “D3D” unless you rely on XAML (not likely).
- Set Architecture to x86 to match with the HoloLens.

Below are windows from a few different versions with the recommended settings.

![Figure 1: Unity ver. 2018.4.2f1](https://dl.dropboxusercontent.com/s/zu65dw5hdjlv0xj/1.png?dl=0)

_Figure 1: Unity ver. 2018.4.2f1_

![Figure 2: Unity ver. 2017.2.5f1](https://dl.dropboxusercontent.com/s/qdg5h5ah0m4rq6o/2.png?dl=0)

_Figure 2: Unity ver. 2017.2.5f1_

## Testing and Deployment Guides
Microsoft guide for connecting a HoloLens to Unity and demo a project (Unity Remoting): [https://docs.microsoft.com/en-us/windows/mixed-reality/unity-play-mode](https://docs.microsoft.com/en-us/windows/mixed-reality/unity-play-mode)

Microsoft guide on deploying and debugging your project with Visual Studio to the HoloLens device: [https://docs.microsoft.com/en-us/windows/mixed-reality/using-visual-studio](https://docs.microsoft.com/en-us/windows/mixed-reality/using-visual-studio). There is a typo; always select “Start Without Debugging” to build and deploy.

## Development Tutorials
Microsoft tutorial to make and deploy a project with the HoloLens device: [https://docs.microsoft.com/en-us/windows/mixed-reality/holograms-100](https://docs.microsoft.com/en-us/windows/mixed-reality/holograms-100). This guide is outdated and uses Unity 5.6.0b11 and .NET. If deploying a C++ app from Visual Studio over a network there are additional steps to enter the IP address of the HoloLens device as described in a Testing and Deployment Tutorial.

Microsoft tutorial to make and deploy a project with the HoloLens emulator: [https://docs.microsoft.com/en-us/windows/mixed-reality/holograms-101e](https://docs.microsoft.com/en-us/windows/mixed-reality/holograms-101e)

Microsoft tutorial to start with the MRTK: [https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html)

Thorough step-by-step guide starting with unboxing a HoloLens 1: [https://medium.com/@mkryaz/step-by-step-hololens-1-with-unity-and-visual-studio-tutorial-4601d5dfcc8f](https://medium.com/@mkryaz/step-by-step-hololens-1-with-unity-and-visual-studio-tutorial-4601d5dfcc8f)

# Debugging

## Unity
You can build to the same directory as a preexisting one but not build with .NET to an IL2CPP build folder or vice versa. A good practice is to delete your previous build of an app before rebuilding.

When using Unity Remoting your project may not appear as expected or at all in the HoloLens. Unity Remoting runs Mono instead of .NET for the backend so what’s deployed may behave differently than the actual project.

## Visual Studio
If Visual Studio fails to run your project, check that you selected the same target settings (x64 vs. x86 or Debug vs. Release) as you used in Unity’s Build Settings.

If Visual Studio shows the build succeeded but the deployment failed due to a connection error, make sure the HoloLens is on and not in standby (sleep) mode. The HoloLens will go into standby if left inactive for three minutes or by briefly pushing the power button once.

# Appendix
Long-Term Support (LTS) stream: A family of Unity version, such as 2018.4.x, which are intended to receive no changes aside from bug fixes. More info at https://blogs.unity3d.com/2018/04/09/new-plans-for-unity-releases-introducing-the-tech-and-long-term-support-lts-streams/

Unity Remoting: Method of demoing a Unity project in-app and linked to a HoloLens device.
