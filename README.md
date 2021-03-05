# windows-terminal-settings
A setup readme for how I like my Windows Terminal configured.

---

## Getting Started

### Pre-requisites
Make sure you have git and the windows terminal installed.
- install `git` [here](https://git-scm.com/downloads)
- install `Windows Terminal` via the `Microsoft Store`, or alternatively via `github` [here](https://github.com/microsoft/terminal/releases)

### Make It Pretty
After installing git and Windows Terminal, open Windows Terminal and run the following commands. We will be following
the instructions found [here](https://www.hanselman.com/blog/how-to-make-a-pretty-prompt-in-windows-terminal-with-powerline-nerd-fonts-cascadia-code-wsl-and-ohmyposh)

Run these lines in the Powershell shell, which is the Windows Terminal default shell:
```
Install-Module posh-git -Scope CurrentUser
Install-Module oh-my-posh -Scope CurrentUser
```
You may also attempt to run this:
```
Install-Module -Name PSReadLine -AllowPrerelease -Scope CurrentUser -Force -SkipPublisherCheck
```
After running the above commands, type the below into the prompt to open the profile. If it does not exist, it will ask you if you want to create one.
```
notepad $PROFILE
```
Add the below lines to the profile then `save`
```
Import-Module posh-git
Import-Module oh-my-posh
Set-Theme Paradox
```
After saving, close Windows Terminal and reopen. You may find that on opening, you are greeted with an error related to the Set-Theme command. If this is the case, replace that line with the following:
```
Set-PoshPrompt Paradox
```
`Paradox` is the theme name. There are additional themes to choose from, which can be found [here](https://github.com/JanDeDobbeleer/oh-my-posh?WT.mc_id=-blog-scottha#themes)

### Settings File
See the included settings.json file in this repo for the settings that I prefer. Copy and paste into the settings.json file on the machine.

### Background Picture
The background picture is included in the repo, however it must be copied to a location that Windows Terminal can read from in order to use it.
This is the location it should be copied to, which is the AppData folder that Windows Terminal creates:
```
%LOCALAPPDATA%\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\RoamingState
```
The picture file must be either a .jpg or a .gif to work. Adjust the settings.json file accordingly for how you'd like it formatted.

### A Better Font
The font I prefer is **Cascadia Code PL**, which includes the glyph's that are necessary for some of the git related command prompts. Find it [here](https://github.com/microsoft/cascadia-code/releases?WT.mc_id=-blog-scottha)
Additional fonts can be found at [NerdFonts](https://www.nerdfonts.com/) but make sure that they have support for PowerLine glyphs.

### Basic Powershell Functions - The Bread and Butter
I use some very basic powershell functions as alias's in my profile to faciliate not having to use the mouse as much as possible. Here is an example function and alias definition, which I would put in the profile (`notepad $PROFILE`) below the above lines. 
```
function Open-VS17 {
  Param($FileName)
  start "C:\Program Files (x86)\Microsoft Visual Studio\2017\Professional\Common7\IDE\devenv.exe" $FileName
}
Set-Alias vs17 Open-VS17
```
This allows me to navigate to the local repo for my project, make sure I've done a `fetch` and `pull` on my branch, and then run the following to open the project solution in Visual Studio 2017, directly from the prompt:
```
vs17 -FileName ProjectName.sln
```
**Additional Function Call - Definitions***
Depending on the dependencies of the projects I'm working on, I may want to add a function similar to the below, which would let me know which version of Visual Studio or other IDE to use with that particular project. This is especially important regarding Business Intelligence type projects in the Microsoft Stack (SSIS, SSRS, etc).
```
function VisualStudioDefine {
  "ProjectName - Use 2015"
  "ProjectName - Use 2017"
  "ProjectName - Use 2010"
}
Set-Alias vsdefine VisualStudioDefine
```
