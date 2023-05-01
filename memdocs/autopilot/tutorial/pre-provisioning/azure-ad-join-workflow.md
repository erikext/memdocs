---
title: Overview for Windows Autopilot for pre-provisioned deployment Azure AD joins in Intune
description: Overview for Windows Autopilot for pre-provisioned deployment Azure AD join in Intune.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/24/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Step by step tutorial for Windows Autopilot for pre-provisioned deployment Azure AD join in Intune

This step by step tutorial guides you through using Intune to perform a Windows Autopilot for pre-provisioned deployment scenario when the devices are strictly Azure AD joined.

The purpose of this tutorial is a step by step guide for all the configuration steps required for a successful Autopilot for pre-provisioned deployment Azure AD join deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [How to: Plan your Azure AD join implementation](/azure/active-directory/devices/azureadjoin-plan) to make sure all prerequisites are met for joining devices to Azure AD.

> [!NOTE]
>
> Since Windows Autopilot for pre-provisioned deployment Azure AD join builds on top of [Windows Autopilot user-driven Azure AD join](../user-driven/azure-ad-join-workflow.md), it's strongly recommended that the Windows Autopilot user-driven Azure AD join scenario is set up, tested, and working first before attempting to use the Windows Autopilot for pre-provisioned deployment Azure AD join scenario. If the Windows Autopilot user-driven Azure AD join doesn't work, then most likely the Windows Autopilot pre-provisioned deployment Azure AD join scenario won't work either.

## Windows Autopilot for pre-provisioned deployment Azure AD join overview

Windows Autopilot for pre-provisioned deployment Azure AD join is an Autopilot solution that automates the configuration of Windows on a new device delivered directly from an IT department, OEM, or reseller. Windows Autopilot for pre-provisioned deployment uses the existing Windows installation installed by the OEM at the factory. The end-user only needs to perform a minimal number of actions during the deployment process such as:

- Powering on the device.
- In certain scenarios, selecting the language, locale, and keyboard layout.
- Connecting to a wireless network if the device isn't connected to a wired network.
- Signing into Azure AD with the end-user's Azure AD credentials.

Windows Autopilot for pre-provisioned deployment can perform the following tasks during the deployment:

- Joins the device to Azure AD.
- Enrolls the device in Intune.
- Installs applications.
- Applies device configuration policies such as BitLocker and Windows Hello for Business.
- Checks for compliance.
- Enrollment Status Page (ESP) can be used to prevent an end-user from using the device until it's fully configured.

Windows Autopilot for pre-provisioned deployment consists of two phases:

- Device ESP phase: Windows is configured and applications and policies assigned to the device are applied.
- User ESP phase: Applications and policies assigned to the user are applied.

Once the Windows Autopilot for pre-provisioned deployment is complete, the device is ready for the end-user to use and they're immediately sent to the Desktop.

## Differences between Windows Autopilot user-driven deployment and Windows Autopilot for pre-provisioned deployment

The main difference between Windows Autopilot user-driven deployment and Windows Autopilot for pre-provisioned deployment is:

- Windows Autopilot user-driven deployment: Both the Device ESP phase and the User ESP phase occur when the end-user goes through the Autopilot deployment after turning on the device for the first time.

- Windows Autopilot for pre-provisioned deployment: Device ESP phase and user ESP phase are split and occur at two different points in time.

  - The IT department, OEM, or reseller handles the device ESP phase. This phase is known as the **Technician flow**. Once the Technician flow is complete, the device is powered down and delivered to the end-user.

  - When the end-user receives the device, they turn it on for the first time, and the device undergoes the user ESP phase. A portion of device ESP also reruns to ensure there are no new applications or policies assigned to the device since the Technician flow ran. This phase is known as the **User flow**.

The deployment is split up between the Technician flow and User flow phases so that the deployment is faster when the end-user receives the device. The deployment is faster when the end-user receives the device because the IT department, OEM, or reseller has completed the first portion of the deployment during the Technician flow.

One possible disadvantage of Windows Autopilot for pre-provisioned deployment over Windows Autopilot user-driven deployment is that if the OEM or reseller is unable to perform the Technician flow, then the device may need to first go to the organization's IT department. The organization's IT department then needs to run the Technician flow once they receive the device followed by delivering the device to the end-user. This extra step prevents the device from being shipped and delivered to the end-user directly from the OEM or reseller. This extra step can lengthen the amount of time before the end-user receives the device.

## Workflow

The following steps are needed to configure and then perform a Windows Autopilot for pre-provisioned deployment Azure AD join in Intune:

> [!div class="checklist"]
> - Step 1: [Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)
> - Step 2: [Allow users to join devices to Azure AD](azure-ad-join-allow-users-to-join.md)
> - Step 3: [Register devices as Autopilot devices](azure-ad-join-register-device.md)
> - Step 4: [Create a device group](azure-ad-join-device-group.md)
> - Step 5: [Configure and assign Autopilot Enrollment Status Page (ESP)](azure-ad-join-esp.md)
> - Step 6: [Create and assign Autopilot profile](azure-ad-join-autopilot-profile.md)
> - Step 7: [Assign Autopilot device to a user (optional)](azure-ad-join-assign-device-to-user.md)
> - Step 8: [Technician flow](azure-ad-join-technician-flow.md)
> - Step 9: [User flow](azure-ad-join-user-flow.md)

> [!NOTE]
>
> Although the workflow is designed for lab or testing scenarios, it can also be used in a production environment. Some of the steps in the workflow are interchangeable and interchanging some of the steps may make more sense in a production environment. For example, the **Create a device group** step followed by the **Register devices as Autopilot devices** step may make more sense in a production environment.

## Walkthrough

> [!div class="nextstepaction"]
> [Step 1: Set up Windows automatic Intune enrollment](azure-ad-join-automatic-enrollment.md)

## More information

For more information on Windows Autopilot for pre-provisioned deployment Azure AD join, see the following article(s):

- [Windows Autopilot for pre-provisioned deployment](/mem/autopilot/pre-provision)
- [User-driven mode for Azure AD join](/mem/autopilot/user-driven#user-driven-mode-for-azure-ad-join)