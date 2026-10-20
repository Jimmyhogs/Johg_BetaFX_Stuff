# Johg_BetaFX_Stuff
This repository is where I am gonna post my BetaFX Kernel stuff since pastebin's advertisement state is just like malware.

For any of these scripts, make sure you click on the copy icon, then go to Vegas and ctrl+v on "Script Input" inside of BetaFX Custom OpenCL Kernel.

The OFX plugin can be downloaded here: https://github.com/boundless-beta/openfx-betafx/releases

-------------------------------------------------------------------

These actions below will cause Vegas Pro to crash

1. Making LUT's with this plugin inside of the effect chain

2. Changing the project resolution after adding the plugin
(if you do change the resolution, click away from the frame
that has the plugin in there, then save and reopen Vegas Pro)

3. Changing the project "Preview" settings after adding the plugin
(make sure "Adjust Size and Quality for Optimal Playback" is off)
(if you do change the preview settings, click away from the frame
that has the plugin in there, then save and reopen Vegas Pro)

4. When you open up Vegas Pro and select the plugin, it's best
to drag the (Default) preset as it is less prone to crashing
as opposed to dragging one of the presets you made. You can
select your preset on the dropdown menu after you drag it in.
