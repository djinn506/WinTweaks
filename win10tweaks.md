
# W10

# Blaine the monkey

May 21, 2021(check back for updates!)
Dec 02, 2022(switch to markdown and github)

-START-
Windows Bloat
Art Apps Tweaks(to be updated..)
NVIDIA
MSI
Internet
OneDrive and Services
Power Settings
Research Links
Downloads
Addendum

Todo: expand on some options and aero tweaker options. Fix Markdown styles.

Disclaimer: Use at your own risk, this is just a tweaking blueprint and you need to know your way around windows. This isn’t a step to step guide, the point is just to send you on your way to squeeze the most out of your system, just cutting down on unneeded junk. Only thing that may differ between people using this on their pc is just programming tools that might need some dependencies and people using specific server protocols, etc (That being said most of these changes aren’t destructive) First make a system restore point for each of the big changes here just in case it breaks something or you don’t like the change for some reason so you can always roll back to a previous state of your system. This is a personal list, what works for me on my system so you may have to tweak some things further. I’m also skipping some things that are common like don’t run a bunch of extensions in your browser.
Only reason I made this was to keep track of my own edits for sanity sake.. Luckily this can live on the internet free to be browsed and easy to check back, edit and save as a pdf. There’s lots to do as soon as you format the PC and this is a healthy reminder of what to do right after, so I’m not scrounging the internet to get my sweet performance back. Most of the edits here are ripped from FR33THY so check him out if you’re interested in more.(Ross from Freeman’s Mind pointed me in the right direction)
Enjoy this humble bundle of computer magic, and feel free to share it around! (Oh, and let me know if there’s other edits I missed.)

If you read this and still need more assistance, here’s FR33THY’s playlist on tweaking windows 10
<https://www.youtube.com/watch?v=PYNlVUyaW0U&list=PLykpkrQ1xVu1jTFCju1cmY9UAHw99aGWW>
There are a lot more tweaks listed here but that’ll give you a clue of where and how to approach these edits.

-START-

- Disable fast boot on BIOS.
- Disable Network Throttling(disregard for notebooks) “HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile”=dword:NetworkThrottlingIndex hex:ffffffff
- Install ShupUp10 <https://www.oo-software.com/en/shutup10>, enable all edits, but let apps use microphone and or camera.
- Remove Unwanted Programs using CCleaner/RevoUninstaller/etc
- Disable unneeded autostart programs.(using CCleaner or any similar program)
- Disable unneeded schedules.(using CCleaner or any similar program)
- Defrag HDD harddrives(**Optional**) - Don’t defrag SSD //you can use defraggler or smartdefrag or windows default defragger.
- **Optional** Disable Compression and Indexing on harddrives (not a big impact and it’ll slog you down when enabled) You’re better off compressing/optimizing the files themselves instead, and not relying on an automatic windows function. I use Riot for images,  Handbrake for videos and Everything for quick searches.
- Open Device Manager and Disable unused devices to cut down on latency {On restart W10 will reinstall basic drivers.}
- Disable visual effects on windows / only thumbnails and smooth system fonts(**Optional**)
- Disable unneeded services manually // using msconfig > services.(ie: windows biometrics)
- **Optional** Use MalwareBytes
- **Optional** Image Visualizer set to JPGview // also install on c:/programs for convenience. <https://sourceforge.net/projects/jpegview/>
- **Optional** Ublock origins (adblock browser extension) settings: add regional filters(on my filters), set to automatically disable javascript, block remote fonts(huge perf boost).
- **Optional** Browser Performance Disable Hardware Acceleration when Available.(makes browsers take up less resources and be more stable) This will also disable rendering 3D graphics on the browser.
- Deletes old drivers from Windows “DriverStore” Folder  <https://github.com/lostindark/DriverStoreExplorer#driverstore-explorer-rapr> - Select “Old Drivers” then click on delete. This folder can get pretty big if not managed.

Windows Bloat

- Disable Automatic Windows Updates <https://christitus.com/windows-update-security-only/>
Computer - Administrative Templates - Windows Components - Windows Update - Windows Update for Business
Set the Feature Updates to Enabled. “Semi-Annual Channel” “365” days
regedit alternative method: “Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings”
dword32bit:”BranchReadinessLevel”: 20
dword32bit:”DeferFeatureUpdatesPeriodInDays”: 365
dword32bit:”DeferQualityUpdatesPeriodInDays”: 4
- Uninstall OneDrive: cmd: “%SystemRoot%\SysWOW64\OneDriveSetup.exe /uninstall”
- Remove OneNote: cmd: “Get-AppxPackage *OneNote* | Remove-AppxPackage”
- Disable Cortana gpedit.msc - All Users: Allow Cortana: Disabled
- Turn OFF cloud search on Windows Start Menu.(search for something on the menu and click on cog for settings)
- **Optional** Uninstall Windows Edge “.\setup.exe –uninstall –system-level –verbose-logging –force-uninstall” (shell cmd in install folder)
- Disable Windows *Optional* Features: Disable SMB 1.0 sharing service (huge write-read drive boost!)
 Search for “Features” / You should get a window that reads “Turn windows features on or off” with a list of features
- Disable Windows *Optional* Features: Disable TCP Port and NTS Framework // only things ON are .NET Framework 3.5 and 4.8 => WCF Services -> Print and Document Services enabled.(in case you use printers) (you can also leave the hyper-v if you use the native pc virtualization)
- WindowsAeroTweaker <https://winaero.com/winaero-tweaker/> unzip/portable mode // Lots of things here, most are up to preference but I’ll expand on this later.
- Windows10Debloater <https://github.com/Sycnex/Windows10Debloater> (git) // run all, they are all useful scripts, run in admin mode. It mostly removes Windows Apps and some OneNote registries. It’s easier to run with PowerShell. (if it asks for permission run “Set-ExecutionPolicy Unrestricted”)
- (manual alternative) Remove Windows Bloat Apps(W10Debloater runs this too) cmd/powershell:

```Remove-AppxPackage -package Microsoft.BingFinance_10004.3.193.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.BingNews_10004.3.193.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.BingSports_10004.3.193.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.BingWeather_10004.3.193.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.Getstarted_2015.622.1108.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.MicrosoftOfficeHub_2015.4218.23751.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.MicrosoftSolitaireCollection_3.1.6103.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.Office.OneNote_2015.4201.10091.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.People_2015.627.626.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.SkypeApp_3.2.1.0_neutral_~_kzf8qxf38zg5c
Remove-AppxPackage -package Microsoft.Windows.Photos_2015.618.1921.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.WindowsAlarms_2015.619.10.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.WindowsCalculator_2015.619.10.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.WindowsCamera_2015.612.1501.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package microsoft.windowscommunicationsapps_2015.6002.42251.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.WindowsMaps_2015.619.213.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.WindowsPhone_2015.620.10.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.WindowsSoundRecorder_2015.615.1606.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.XboxApp_2015.617.130.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.ZuneMusic_2019.6.10841.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.ZuneVideo_2019.6.10811.0_neutral_~_8wekyb3d8bbwe
Remove-AppxPackage -package Microsoft.3DBuilder_10.0.0.0_x64__8wekyb3d8bbwe
```

- Disable Fullscreen Optimizations on all programs manually
right click exe, Properties, Compatibility, Disable Fullscreen Optimizations Checked
-**Optional** ISLC <https://www.wagnardsoft.com/forums/viewtopic.php?t=1256> (clears memory when a program closes and sets system clock to reduce latency)- set wanted timer resolution to unchecked(**Optional**:set to 0.5 for max perf) so the program just clears memory. Set to autostart and launch on log-on.
- **Optional** Set Full System Responsiveness “HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile” dword:SytemResponsiveness hex:00000000
- **Optional** Set High Priority Games “HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games” Gpu Priority: 8 Priority:6
- **Optional** <https://github.com/lostindark/DriverStoreExplorer#driverstore-explorer-rapr> Deletes Old(unused) Drivers from DriverStore Folder (check folder size first)

Art Apps Tweaks(to be updated..)

- Disable/Uninstall unused plugins on Max and Maya Photoshop etc whatever software you use the most should be as light as possible while keeping functionality. Ie:
 3ds max uninstall MAXtoA(material switcher) Revit and Material Libraries(all resolutions).
 Maya uninstall Bifrost(particle simulation)
- Photoshop Wacom Tweaks
 C:\Users\j\AppData\Roaming\Adobe\Adobe Photoshop CC\Adobe Photoshop CC Settings
 New txt file “PSUserConfig.txt”:

# Use WinTab

UseSystemStylus 0

# Use Legacy Healing Brush

LegacyHealingBrush 1

# Disable Scratch Compression for fast HDD

VMCompressionPages 0

# Use Overscrolling

OverscrollingAlways 2

- Disable Touch Input Lag // regedit
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\TouchPrediction]
"Latency"=dword:00000002
"SampleTime"=dword:00000002
"UseHWTimeStamp"=dword:00000001

NVIDIA

- Disable Automatic Driver Updates regedit
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\DriverSearching] "SearchOrderConfig"=dword:00000000
- Restart in safe mode and run DDU(Display Driver Uninstaller) to remove automatic Nvidia drivers.(you just need the driver itself so uninstall for now)
- Extract Nvidia Drivers .exe (using 7-zip or similar)
- Remove all folders but NVII, Driver and GFExperience, leave the loose files alone.(setup, etc.)
- Run Setup and opt out of experience. (no need since we’re already over 9000)
- Depending on what you play, some good stable versions are: 442.74 - 451.48 - 475.30(latest) if you’re using older games maybe try benchmarking with fraps using the older versions first.
- Update Nvidia Driver to version v460.84 or latest for security reasons. <https://www.bleepingcomputer.com/news/security/nvidia-fixes-high-severity-flaws-affecting-windows-linux-devices/>
- Set Nvidia control panel settings to performance // use my settings unless you know better.
- Disable Ansel on Nvidia using <https://github.com/Orbmu2k/nvidiaProfileInspector> Run NPI look under “Other” Set “NVIDIA Predefined Ansel Usage” to 0x0000000
- Set cuda force p2 state to OFF. (also using Nvidia Profile Inspector) Under “Common” Set “CUDA- Force P2 State” to “Off”
- Install and run Interrupt-Affinity Policy Tool. X64 version.
<http://download.microsoft.com/download/9/2/0/9200a84d-6c21-4226-9922-57ef1dae939e/Interrupt_Affinity_Policy_Tool.msi>
 Set nvidia on cpu 8 and 9. Restart device.

- Uninstall all Visual C programs (Preferably using CCleaner or similar uninstaller)
- Install Visual C++ by major geeks(burf) <https://www.majorgeeks.com/files/details/visual_c_runtime_installer.html>
- Install Microsoft Visual Basic/C++ by major geeks <https://www.majorgeeks.com/files/details/multipack_visual_c_installer.html>
- Install Microsoft Visual Cpp <https://www.majorgeeks.com/files/details/visual_c_runtime_installer.html>
- Install DXwebsetup <https://www.microsoft.com/en-us/Download/confirmation.aspx?id=35>
- Open Device Manager: Menu / View Devices by Connection:
Look for “PCI-to-PCI Bridge”- Disable Nvidia HighDefinition Sound Driver(**Optional** this will disable sound from HDMI connections). Disable USB 3.e Driver (unneeded)
- Run msi_util <https://forums.guru3d.com/threads/windows-line-based-vs-message-signaled-based-interrupts-msi-tool.378044/> set video card to msi to “Enabled”. Interrupt to “high”. Accept to Restart.
- Run msi_util again and double check.
Nvidia Control panel Settings (set to performance first):
Gamma correction off
Low latency mode on
Open gl set to {installed gpu card}
Power management maximum performance
Shafer cache on
Texture filtering high performance
Trilinear optimizations on
Threaded optimizations auto/on
Triple buffering off
Vertical sync off
Virtual reality prerendered frames 1

Need more help? Most of these edits are here <https://www.youtube.com/watch?v=o5KiZIXfhko>

MSI

- Install and Configure Msi Afterburner (my settings in geforce 1050ti):

Power Limit Full, Temp Limit full, +100 MemoryClock(not pictured). Fan Ramp 30C at 50% and 90C at 100%.

Internet

- Install Intel Ethernet Driver for Ethernet connections (in case you’re using ethernet) (skip this if you’re using wifi)  <https://downloadcenter.intel.com/download/25016/Ethernet-Intel-Network-Adapter-Driver-for-Windows-10>
- Run “TCP optimizer” <https://www.speedguide.net/downloads.php>  with 50mib speed // test either my config here for wifi connections or set optimized, alternately just read the instructions to see what each option does.
- Set Google DNS ipv4 “8.8.8.8″ - “8.8.4.4″ and ipv6 “2001:4860:4860::6464 - 2001:4860:4860::64″// Preferably use openVPN or any vpn service.
 Control Panel\Network and Internet\Network Connections (right click on the connections you’re using, properties, I only enable Internet Protocol Version 4 and 6) Double click on Internet Protocol, set “Use the following DNS server” and input the DNS listed before on both IPv4 and IPv6
- Disable Auto Tuning  - cmd: “netsh int tcp set global autotuninglevel=disabled”
- Disable Reserved Bandwidth gpedit.msc: Computer Config / Admin Templates / Network /  Qos Packet / Limit Reserved Bandwidth / enabled 0%
- **Optional** Disable Nagle’s Algorithm “HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces\{NIC-id}”NIC-id is your ip TcpAckFrequency:1 to disable “nagling” for gaming.  TCPNoDelay:1 to disable “nagling” TcpDelAckTicks:0
- **Optional** Install Simplewall <https://www.henrypp.org/product/simplewall> and enable shields and autostartup // unlock file // (set UAC to low) // extract to c//programs so it doesn’t trigger antivirus or anything. (disable any windows connections that're automatic, you just need to re-enable those whenever you want to update) btw don’t ever update *Optional* features on windows.
Wishlist: to perpetually disable OneNote and Sync from windows services. Disable cache from services.
Results from 6mib to 55mib wifi speed. From slow system boot to fast booting and fast programs(didn’t benchmark anything) Reducing device latency and disabling SMB 1.0 windows feature was the biggest detractor but there’s lots to do. Programs open pretty instantly. Windows processes down to 33, background processes 40.

OneDrive and Services
Remove OneDrive:

- cmd:“taskkill/f /im onedrive.exe”
- cmd:”%SystemRoot%\SysWOW64\OneDriveSetup.exe/ uninstall”
- Run gpedit Computer Configuration\Administrative Templates\Windows Components\OneDrive
- Double Click "Prevent the usage of OneDrive for file storage" - Set to Enable, Enable the policy and click ok.
- Disable on Windows Explorer
gpedit [HKEY_CLASSES_ROOT\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}] @="OneDrive"
"System.IsPinnedToNameSpaceTree"=dword:00000000
"SortOrderIndex"=dword:00000042
<https://community.spiceworks.com/how_to/139987-remove-onedrive-from-windows-10-completely>
- Disable Unistoresvc:(**Optional**)
 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\UnistoreSvc set "Start" to "4" (disabled)
<https://appuals.com/how-to-fix-unistack-service-group-unistacksvcgroup-high-cpu-or-memory-usage/>
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\
Set all to start "4"(means disabled)(**Optional**)
avctp service
captureservice
bcastdvr service
bluetooth service(unless you use it)
bcastservice
onesyncsvc
onesyncsvc_32131
SENS
Sense
SensorService
UdkUserSvc (**Optional**)
UserDataSvc (**Optional**)
SensorDataService
TabletInputService
UserDataService  
WpnUserService

Power Settings
This part is based on “Power Tweaks” - Fr33thy <https://www.youtube.com/watch?v=PbP--el7FbA>

- Install ParkControl <https://bitsum.com/parkcontrol/> (you only need this to set a custom power plan, you can uninstall the program right after)
- Install Power Settings Explorer <https://forums.guru3d.com/threads/windows-power-plan-settings-explorer-utility.416058/>
“boottweaks.reg”:
Windows Registry Editor Version 5.00
; Disable driver updates
; Disable driver searching
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\DriverSearching]
"SearchOrderConfig"=dword:00000000
; Disable UAC
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System]
"EnableLUA"=dword:00000000
; Use my sign in info after restart - disable
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System]
"DisableAutomaticRestartSignOn"=dword:00000001
; Turn off microsoft consumer experiences (GPEDIT)
; Disables app suggestions on start  
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\CloudContent]
"DisableWindowsConsumerFeatures"=dword:00000001
; Windows photo viewer default
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Photo Viewer\Capabilities\FileAssociations]
".tif"="PhotoViewer.FileAssoc.Tiff"
".tiff"="PhotoViewer.FileAssoc.Tiff"
".bmp"="PhotoViewer.FileAssoc.Tiff"
".dib"="PhotoViewer.FileAssoc.Tiff"
".gif"="PhotoViewer.FileAssoc.Tiff"
".jfif"="PhotoViewer.FileAssoc.Tiff"
".jpe"="PhotoViewer.FileAssoc.Tiff"
".jpeg"="PhotoViewer.FileAssoc.Tiff"
".jpg"="PhotoViewer.FileAssoc.Tiff"
".jxr"="PhotoViewer.FileAssoc.Tiff"
".png"="PhotoViewer.FileAssoc.Tiff"
; Network throttling
; System responsiveness
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile]
"NetworkThrottlingIndex"=dword:ffffffff
"SystemResponsiveness"=dword:00000000
; Disable automatic maintenance
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Schedule\Maintenance]
"MaintenanceDisabled"=dword:00000001
; Disable fast startup
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Power]
"HiberbootEnabled"=dword:00000000
; Disable power throttling
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\PowerThrottling]
"PowerThrottlingOff"=dword:00000001
; Optional: Disable spectre and meltdown (Do NOT disable cpu mitigations if you're connected to the internet)
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management]
"FeatureSettingsOverride"=dword:00000003
"FeatureSettingsOverrideMask"=dword:00000003
; Processor scheduling
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\PriorityControl]
"Win32PrioritySeparation"=dword:00000026
; Network throttling
; System responsiveness
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile]
"NetworkThrottlingIndex"=dword:ffffffff
"SystemResponsiveness"=dword:00000000
; Games scheduling
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games]
"Affinity"=dword:00000000
"Background Only"="False"
"Clock Rate"=dword:00002710
"GPU Priority"=dword:00000008
"Priority"=dword:00000006
"Scheduling Category"="High"
"SFIO Priority"="High"
; System properties - performance options - custom
[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\VisualEffects]
"VisualFXSetting"=dword:00000002
; Disable FSO globally
[HKEY_CURRENT_USER\System\GameConfigStore]
"GameDVR_Enabled"=dword:00000000
"GameDVR_FSEBehaviorMode"=dword:00000002
"GameDVR_HonorUserFSEBehaviorMode"=dword:00000000
"GameDVR_DXGIHonorFSEWindowsCompatible"=dword:00000000
"GameDVR_EFSEFeatureFlags"=dword:00000000
; Disable game bar
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\default\ApplicationManagement\AllowGameDVR]
"value"=dword:00000000
; Disable hibernate
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power]
"HibernateEnabled"=dword:00000000

; Menu show delay
[HKEY_CURRENT_USER\Control Panel\Desktop]
"MenuShowDelay"="0"

-----------------------------------------------------------------;
; Disable updates
Gpedit.msc

Computer Configuration/Administrative Templates/Windows Components/Windows Update
Configure automatic updates - disabled

- Disable Updates **Optional**

Specify intranet microsoft update service location - enabled
Enter these links below in boxes to the left
    http:\\neverupdatewindows10.com
    http:\\neverupdatewindows10.com
    http:\\neverupdatewindows10.com
-----------------------------------------------------------------;

Remove access to use all windows update features - enabled

-----------------------------------------------------------------;

Do not connect to any windows update internet locations - enabled

Do not include drivers with windows updates - enabled

-----------------------------------------------------------------;

Annoyances:
Remove Speech Service:
C:\WINDOWS\SysWOW64\Speech_OneCore\Common\SpeechRuntime.exe -ToastNotifier
temp solution: rename "Speech_OneCore" folder to "bk_Speech_OneCore"

Disable Windows Explorer Ribbon: delete/rename folder (incomplete)

Remove w10 lock screen
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI\SessionData "AllowLockScreen" set to "0" //windows resets it
C:\Windows\SystemApps rename "Microsoft.LockApp_cw5n1h2txyewy"(actual fix)
take ownership reg
Windows Registry Editor Version 5.00
;Created by Vishal Gupta for AskVG.com
[HKEY_CLASSES_ROOT\*\shell\runas]
@="Take ownership"
"HasLUAShield"=""
"NoWorkingDirectory"=""

[HKEY_CLASSES_ROOT\*\shell\runas\command]
@="cmd.exe /c takeown /f \"%1\" && icacls \"%1\" /grant administrators:F"
"IsolatedCommand"="cmd.exe /c takeown /f \"%1\" && icacls \"%1\" /grant administrators:F"

[HKEY_CLASSES_ROOT\Directory\shell\runas]
@="Take ownership"
"HasLUAShield"=""
"NoWorkingDirectory"=""

[HKEY_CLASSES_ROOT\Directory\shell\runas\command]
@="cmd.exe /c takeown /f \"%1\" /r /d y && icacls \"%1\" /grant administrators:F /t"
"IsolatedCommand"="cmd.exe /c takeown /f \"%1\" /r /d y && icacls \"%1\" /grant administrators:F /t"

Disable Windows Store(nuke)

Computer Configuration -> Administrative Templates -> Windows Components -> Store
Turn Off Store Application - Enabled  

Get-AppxPackage *windowsstore* | Remove-AppxPackage

Get-AppxPackage -name "*windowsstore*" -user "username" | Remove-AppxPackage

Firefox tweaks

about:config

animations disable animations

browser.tabs.remote.autostart false

content.notify.interval 500000

content.switch.threshold 250000

How to disable Picture-In-Picture
 options ; browsing; enable picture controls (unchecked)

add ui.prefersReducedMotion 1 (number)

Booting settings
**Optional** Copy into a new “BCDEdit.txt” file, set to “.cmd” and run file.
@echo off
@echo
@echo Disable HPET
bcdedit /deletevalue useplatformclock
@echo
@echo Disable dynamic tick (laptop power savings)
bcdedit /set disabledynamictick yes
@echo
@echo Disable synthetic timers
bcdedit /set useplatformtick yes
@echo
@echo Boot timeout 0
bcdedit /timeout 0
@echo
@echo Disable nx
bcdedit /set nx optout
@echo
@echo Disable boot screen animation
bcdedit /set bootux disabled
@echo
@echo Speed up boot times
bcdedit /set bootmenupolicy standard
@echo
@echo Disable hyper virtualization
bcdedit /set hypervisorlaunchtype off
@echo
@echo Disable trusted platform module (TPM)
bcdedit /set tpmbootentropy ForceDisable
@echo
@echo Remove windows login logo
bcdedit /set quietboot yes
@echo
@echo
@echo Disable boot logo
bcdedit /set {globalsettings} custom:16000067 true
@echo
@echo Disable spinning animation
bcdedit /set {globalsettings} custom:16000069 true
@echo
@echo Disable boot messages
bcdedit /set {globalsettings} custom:16000068 true
@echo
pause

Research Links

- FR33THY Entire youtube Channel <https://www.youtube.com/watch?v=gajy_5oFbIc>
- FR33THY Windows A Z Performance Latency <https://www.youtube.com/watch?v=PYNlVUyaW0U&list=PLykpkrQ1xVu1jTFCju1cmY9UAHw99aGWW>
- FR33THY Driver Lag Bloatware Nvidia Performance Telemetry Kboost Msi Mode <https://www.youtube.com/watch?v=o5KiZIXfhko>
- FR33THY BIOS Update - Win A-Z Pt1 <https://www.youtube.com/watch?v=jSFjyLmX_0Y>
- FR33THY Nvidia Graphics Tweaks and Overclock <https://www.youtube.com/watch?v=gajy_5oFbIc>
- The Fastest Windows 10 Setup - Chris Titus Tech <https://www.youtube.com/watch?v=Tfd7BXCo9Xk>
- Disable Spectre Mitigation for Performance Gain - Chris Titus Tech <https://www.youtube.com/watch?v=mAYxMC1Vzkw>
- Improving graphics quality with NVIDIA DSR - forthenext <https://www.youtube.com/watch?v=vmzGrHw6hyI>
- 17 Reasons Why I Do Not Use Windows 10  - Chris Titus Tech  <https://www.youtube.com/watch?v=TMeeryVlGAY>
- Windows Update Security Only  <https://christitus.com/windows-update-security-only/>
- Windows 10Gamer Tweaks <https://www.back2gaming.com/guides/how-to-tweak-windows-10-for-gaming/>

Downloads

<https://winaero.com/winaero-tweaker/>
<https://github.com/Sycnex/Windows10Debloater>
<https://www.henrypp.org/product/simplewall>
<https://www.speedguide.net/downloads.php>
<https://downloadcenter.intel.com/download/25016/Ethernet-Intel-Network-Adapter-Driver-for-Windows-10>
<https://www.guru3d.com/files-details/display-driver-uninstaller-download.html>
<https://github.com/Orbmu2k/nvidiaProfileInspector>
<https://sourceforge.net/projects/jpegview/>
<https://www.bitdefender.com/>
<https://bitsum.com/parkcontrol/>

Addendum
Some Useful tools that didn’t fit anywhere else.

Images:
<https://www.majorgeeks.com/files/details/jpegview.html> JpegView - Fast Image Visualizer
<https://www.irfanview.com/64bit.htm> IrfanView - Fast Image Visualizer(mainly use it for thumbnails)
<https://riot-optimizer.com/download/> Riot Radical Image Optimization tool, Fast Realtime Image Compressor (mostly for web) - Also does batch
<https://github.com/amadvance/advancecomp/releases> needed for compressing PNGs with Riot (“advpng.exe”)
<http://optipng.sourceforge.net/> Another Riot Plugin for PNGs compression
<http://advsys.net/ken/util/pngout.exe> Another Riot Plugin for PNGs compression (extreme)

Usability
<https://www.strokesplus.net/Downloads> Allows mouse gestures depending the application you’re using
<https://www.autohotkey.com/> AutoHotkey - allows you to remap your keyboard or set keys/ key combinations to perform certain actions.
