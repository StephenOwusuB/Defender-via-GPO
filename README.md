
## Onboarding Devices with Group Policy

1. Go to [security.microsoft.com](https://security.microsoft.com).
2. Navigate to **Settings** and select **Endpoints**.
![Select Endpoint](https://github.com/StephenOwusuB/Implementing-Microsoft-Defender-for-Enterprise-Security/blob/main/images/DGPO%20images/MDE%20onboard%202.png)
3. Scroll down to **Device management** and select **Onboarding**.
[GPO](https://github.com/StephenOwusuB/Implementing-Microsoft-Defender-for-Enterprise-Security/blob/main/images/DGPO%20images/MDE%20onboard%204.png)
4. Choose the onboarding options with the deployment method set to **Group Policy**. Ensure to download the package for Group Policy as the scripts vary based on the deployment method.
5. On your Domain Controller (DC), extract the downloaded package. You will see `WindowsDefenderATPOnboardscript` and `OptionalParamsPolicy` folders. The `OptionalParamsPolicy` folder includes two files used for enabling sample collection for deep analysis. The `WindowsDefenderATPOnboardscript` is used to onboard devices.
6. ![GPO](https://github.com/StephenOwusuB/Implementing-Microsoft-Defender-for-Enterprise-Security/blob/main/images/DGPO%20images/MDE%20onboard%206.png)
7. Go to **Group Policy Management**:
    - Expand your domain.
    - Select **Group Policy**.
    - Right-click and select **New**.
    - Name your GPO (e.g., Onboarding MDE Device).
![New GPO](https://github.com/StephenOwusuB/Implementing-Microsoft-Defender-for-Enterprise-Security/blob/main/images/DGPO%20images/MDE%20onboard%208.png)

8. To ensure the file is accessible to the client from the shared location:
    - Right-click the Group Policy and select **Edit**.
    - Go to **Computer Configuration** > **Preferences** > **Control Panel Settings**.
    - Click **Scheduled Tasks**.
    - Right-click the space and select **New** > **Immediate Task (at least Windows 7)**.
    - Specify a name (e.g., deviceonboard).
    - Specify security options by typing **SYSTEM** to select `NT AUTHORITY\SYSTEM` and ensure it runs with the highest privileges.
    - Define an action by selecting the **Action** tab at the top and clicking **New**. Define the location where the file exists.

![New GPO](https://github.com/StephenOwusuB/Implementing-Microsoft-Defender-for-Enterprise-Security/blob/main/images/DGPO%20images/MDE%20onboard%209.png)
![Schedule task](https://github.com/StephenOwusuB/Implementing-Microsoft-Defender-for-Enterprise-Security/blob/main/images/DGPO%20images/MDE%20onboard%2010.png)
![Schedule task](https://github.com/StephenOwusuB/Implementing-Microsoft-Defender-for-Enterprise-Security/blob/main/images/DGPO%20images/MDE%20onboard%2011.png)
![Schedule task](https://github.com/StephenOwusuB/Implementing-Microsoft-Defender-for-Enterprise-Security/blob/main/images/DGPO%20images/MDE%20onboard%2012.png)
![Schedule task](https://github.com/StephenOwusuB/Implementing-Microsoft-Defender-for-Enterprise-Security/blob/main/images/DGPO%20images/MDE%20onboard%2013.png)
![Schedule task](https://github.com/StephenOwusuB/Implementing-Microsoft-Defender-for-Enterprise-Security/blob/main/images/DGPO%20images/MDE%20onboard%2026.png)
## Creating a Share Folder

1. Go to **Server Manager** and click on **File and Shares**.
2. Select **Tasks** and click on **New Share**.
3. Select **SMB Quick Profile** and click **Next**.
4. Specify the volume for the share and select a custom path.
5. Select the share folder you created on the root drive or create a new one.
6. Click **Next** and proceed through the wizard, adding descriptions and configuring share settings as needed.
7. Disable inheritance and convert inherited permissions into explicit permissions. Remove all default users and add specific users or groups with the required permissions.
8. Click **OK**, **Apply**, and **Create**.

## Completing the Task

1. Add domain computers permission to access the share.
2. Copy the share path, package path, and configuration path.
3. Paste these paths in the configuration settings in the scheduled task.
4. Click **Apply** and **OK**.

This means the Group Policy Object (GPO) has been created with the respective task.

## Setting Up Sample Collection

1. Use the same GPO for setting up sample collection or create a new GPO if you intend to exclude some devices.
2. Go to the file location, expand the `OptionalParamsPolicy` folder, and copy the ADMX file.
3. Navigate to `C:\Windows\PolicyDefinitions` and paste the ADMX file.
4. Copy the `en-US` file and paste it in `C:\Windows\PolicyDefinitions\en-US`.
   Sample Collection](https://github.com/StephenOwusuB/Implementing-Microsoft-Defender-for-Enterprise-Security/blob/main/images/DGPO%20images/MDE%20onboard%2027.png)
5. Restart the Group Policy Management Console. If changes are not showing, restart the server.
7. Link the GPO to the Organizational Unit (OU) by right-clicking the OU and selecting **Link Existing GPO**.

Select the GPO to link it.
![Link GPO](https://github.com/StephenOwusuB/Implementing-Microsoft-Defender-for-Enterprise-Security/blob/main/images/DGPO%20images/MDE%20onboard%2028.png)
---


