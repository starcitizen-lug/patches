# patches
Patches created by the community for wine and other Linux packages

The Wine patches listed here are sourced and applied to our [LUG-Wine Runners](https://github.com/starcitizen-lug/lug-wine)

# Required Compatibility Patches

**EAC Compatibility**
- 10.2+_eac_fix
  - EAC expects separate 32bit and 64bit wine loaders
- eac_locale
  - For certain locales, the EAC launcher requires specific fonts that are unavailable in Wine, resulting in an error. Force en-us for only EAC specifically
- disable_syscall_dispatch
  - EAC fails with syscall_dispatch enabled on 11.5 and newer
- eac_60101_timeout
  - Avoids EAC error 60101 due to a timeout waiting for the eac_wine_pid file

# Quality of Life Patches
- cache-committed-size
  - Star Citizen checks committed size thousands of times per second and it is a problematic lookup in wine
- silence-sc-unsupported-os
  - Automatically acknowledge popup that prevents the game from continuing loading without user input
- unopenable-device-is-bad
  - Fixes RSI Launcher failing when trying to patch a a game install outside C:
- append_cmd
  - Automatically apply CEF electron args --in-process-gpu --disable-gpu --no-deprecation in winewayland mode 
- sc_gpumem
  - Satisfy the way SC monitors GPU memory. The game uses NtGdiDdDDIQueryStatistics instead of querying Vulkan
- 0001-wineopenxr_add
  - Apply wineopenxr from Proton
- 0002-wineopenxr_enable
  - Enable wineopenxr from Proton

 <br/>

 **Enable DLSS**
- dummy_dlls
  - ngx checks for the existence of several DLLS, create dummy DLLs of 'cryptbase.dll', 'devobj.dll', 'drvstore.dll' to satisfy checks
- enables_dxvk-nvapi
  - Enable dxvk-nvapi environment variable by default
- nvngx_dlls
  - Automate nvngx dlls setup
 
**Wayland**
- systray-title
  - Give a useful title to the systray icon window in winewayland mode so that users know what it is
- winewayland-prefer-relative-pointer
  - Improve interaction mode cursor behavior on wayland
- winewayland-guess-primary-output
  - Present the game on the primary monitor
- winewayland-fullscreen-idle-inhibit
  - Prevent idle when using game controllers and sticks
 
# Vulkan

Vulkan fails to initialize for some Nvidia users on the r.LinuxWINEOverride = 1 override. This necessitates using DX11 instead, or using VKD3D-Proton for the DX12 presentation mode

**VKD3D-Proton**
- hidewineexports
  - Wine's HideWineExports does not work properly and needs to be fixed
- reg_hide_wine
  - Enable HideWineExports to trigger the DX12 present mode through VKD3D-Proton
- reg_show_wine
  - Disable HideWineExports when switching back to normal lug-wine from lug-wine-experimental
