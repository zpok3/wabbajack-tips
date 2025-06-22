# wabbajack-tips
Just some tips and useful info about compiling Wabbajack lists I've learned (for Fallout 3 and New Vegas mainly).

## Meta Files
### Quick overview
For Wabbajack to install modlists "*without bundling any assets or re-distributing any mods*" it must be able to match everything in the portable MO2 instance you've created for the modlist to a source. Sources include:
- The internet (e.g. NexusMods, ModDB, GitHub, etc).
- The files for the game the modlist is for.

### Obtaining metadata for Nexus files without a mod manager download button
So you might have noticed certain files on the Nexus do not have an option to download with mod manager, and only a manual download button. Fortunately MO2 can obtain metadata for these files.
1. Place the file into the downloads folder for the MO2 instance.
2. In MO2, right click the file in the downloads list and select `Query Info`.

![query info](https://raw.githubusercontent.com/zpok3/wabbajack-tips/main/imgs/query-info-example.webp)
> [!tip]
> FNV/TTW MO2 instances can automatically query info for Fallout 3 Nexus files, same goes for FO3 MO2 instances and New Vegas Nexus files.

### Obtaining metadata for files from a Nexus that isn't the game that MO2 is managing
You may have noticed the `Query Info` option is unable to automatically obtain metadata for files hosted on the Modding Tools Nexus or the Skyrim SE Nexus (e.g. [MO2 ModdingLinked Edition](https://www.nexusmods.com/site/mods/874) or [Root Builder](https://www.nexusmods.com/skyrimspecialedition/mods/31720)). It's pretty easy to configure it manually.
1. In MO2 right click the file in the downloads list and select `Open Meta File` and replace the contents with the following template:
```
[General]
installed=true
gameName=
modID=
fileID=
```
2. Set`gameName` to `site` if it's from the Modding Tools Nexus or `skyrimse` if it's from the Skyrim SE Nexus.

3. You can find the `modID` by looking at the number at the end of the mod page's URL.

![modid](https://raw.githubusercontent.com/zpok3/wabbajack-tips/main/imgs/wj_tips_modID.webp)

5. You can find `fileID` by right clicking the `Manual download` button and selecting `Open in new tab`. Switch to that tab, and the file ID will be located at the end of the URL.

![fileid](https://raw.githubusercontent.com/zpok3/wabbajack-tips/main/imgs/wj_tips_fileID.webp)

## Compilation Settings
Just a quick overview of compilation settings and examples of where they'd be useful.

### Always Enabled
- Wabbajack normally will ignore mods that are disabled in the selected MO2 profile during compilation. Useful for optional mods that you want to be disabled by default (e.g. platform specific files for Steam/GOG, [DXVK](https://www.nexusmods.com/newvegas/mods/79299)).

### Ignore
- Makes Wabbajack ignore a specified file/folder. Useful if you have mods you use for development you don't want included in the final installation.

### Include
- Inlines files into the `.wabbajack` file, do NOT use this on downloaded mods. Useful for files like xEdit modgroups, custom patches, and custom mods made for the list. Note that you will be missing out on Nexus donation points if the mods/patches are usable outside of the modlist (read [here](https://wiki.wabbajack.org/policies_and_license/Wabbajack%20Monetization%20Policy.html#you-must) for more details).

### No Match include
- Inlines files that cannot be matched to a source into the `.wabbajack` file. Not really useful in Fallout 3/New Vegas as there aren't any tools I am aware of that generate outputs that cannot be uploaded to the Nexus or the Wabbajack CDN. It's mainly used on tool outputs (e.g. ParallaxGen) that are a mix of new assets and assets that can be matched to stock game files/downloaded mods.

## Creating a GitHub personal access token to access the Wabbajack CDN
- Instead of a classic token you can generate a fine-grained token with just read/write access to the `Contents` of the repository that contains your `modlists.json`. This is a bit better for security because it limits the personal access token to just what Wabbajack needs access to.
