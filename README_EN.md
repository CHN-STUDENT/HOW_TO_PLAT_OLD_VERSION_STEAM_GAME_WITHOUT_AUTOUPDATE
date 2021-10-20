## HOW_TO_PLAT_OLD_VERSION_STEAM_GAME_WITHOUT_AUTOUPDATE

This is a readme to introduce how to play old version steam game without auto update. 

But It has not been fully validated, so you may not get successfull easily. If you failed, please try again or give up.　

**Warnning: Playing old version game may have issue or not, be care of!**

## If your game have not update complete or download update patch.


0. Do not download any patch and exist steam entirely.

1. Get your game app id from https://steamdb.info/ , eg: Age of Empires III: Definitive Edition 's ID [933110](https://steamdb.info/app/933110/)

2. Get your game depot id, eg: Age of Empires III: Definitive Edition Main file is `933111`, Chinese voice package 's ID `933113`

3. Open your steam game path, eg:  `D:\steam\steamapps`，Find appmanifest file likes  `appmanifest_933110.acf`, then backup. And found your game info in here.

    - I want to play [8640815080218763479](https://steamdb.info/depot/933111/history/?changeid=M:8640815080218763479) version which published in 2021.09.24, my Owner id is `76561198354349477`


4. Forge appmanifest file to cheat updateer, you need find the lastest version `manifest` and `buildid` 

![image](https://user-images.githubusercontent.com/21209416/137933796-2af13fab-8c75-4c9c-a9e5-64ed5bca1617.png)

- Set old mainifest id `8640815080218763479` to lastest `4771437915371768058`

- Set  `StateFlags`	 to 	`4`

- Set `"LastUpdated"` to 	"1634099906" （2021-10-19 22:49:15）or later, It is a Unix time, make sure it will be late on update publish time.

- Set `"buildid"`	 to lastest `"7500522"`

- Set `"UpdateResult"`  to `"0"`

- **I have not try if need to change size info, may be not** 

- Set something settings to `"0"`,like this:

```
"BytesToDownload"		"0"
"BytesDownloaded"		"0"
"BytesToStage"		"0"
"BytesStaged"		"0"
"AutoUpdateBehavior"		"0"
"AllowOtherDownloadsWhileRunning"		"0"
"ScheduledAutoUpdate"		"0"
```

This is my appmanifest, **you could not be use in yourself without any edit**：

```
"AppState"
{
	"appid"		"933110"
	"Universe"		"1"
	"LauncherPath"		"D:\\steam\\steam.exe"
	"name"		"Age of Empires III: Definitive Edition"
	"StateFlags"		"4"
	"installdir"		"AoE3DE"
	"LastUpdated"		"1634099906"
	"UpdateResult"		"0"
	"SizeOnDisk"		"46451641103"
	"buildid"		"7500522"
	"LastOwner"		"76561198354349477"
	"BytesToDownload"		"0"
	"BytesDownloaded"		"0"
	"BytesToStage"		"0"
	"BytesStaged"		"0"
	"AutoUpdateBehavior"		"0"
	"AllowOtherDownloadsWhileRunning"		"0"
	"ScheduledAutoUpdate"		"0"
	"InstalledDepots"
	{
		"933111"
		{
			"manifest"		"4771437915371768058"
			"size"		"45975794377"
		}
		"933113"
		{
			"manifest"		"8217306787633308756"
			"size"		"475846726"
		}
	}
	"InstallScripts"
	{
		"933111"		"install.vdf"
	}
	"UserConfig"
	{
		"language"		"schinese"
	}
}
```

At last, you need to check steam downloading path like `D:\steam\steamapps\downloading` if has download patch, if has something please delete.

Then you can play games.


## Or Download old version by using depotdownloader

you need to use tools [DepotDownloader](https://github.com/SteamRE/DepotDownloader) ，create a batch in depotdownloader root path。


```
@echo off
title download 7330660
dotnet %~dp0DepotDownloader.dll %* ^
 -username xxxxx^
 -app 933110 ^
 -depot 933111 ^
 -manifest 8640815080218763479 ^
 -dir %~dp0\7330660 ^
 -validate ^
 -remember-password
```

use console (cmd) to open this batch

After download complete，copy to your steam installing path, Forge an appmanifest file.

Or you can download all new version, rename new installing path, copy download file to there.

**I think to cheat updater, we only need to do fake `appmanifest` file, and if have any update, we need to cheat again. But i have not fully validated, hope you can help me test.**
