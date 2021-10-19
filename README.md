## HOW_TO_PLAT_OLD_VERSION_STEAM_GAME_WITHOUT_AUTOUPDATE
## 如何跳过 steam 更新玩老版本游戏

**注意本文仅是一种思路，并未经过充分验证，如果您失败了，请多次尝试或直接放弃，本作者不承担任何无法使用的风险。**

**仅供研究测试和爱好使用，请小心您的账号！**

## 游戏还未更新或游戏更新未完成

0.  steam 提示游戏更新时，不要更新！点击取消更新，彻底关闭 steam 。

1.  得到 `APPID`，查询 https://steamdb.info/ 得到这个游戏的 `APPID`。例如帝国时代3决定版ID [933110](https://steamdb.info/app/933110/) 。

2.  找到这个游戏的 `Depot ID` ，还以刚才帝国时代 3 为例，刚才页面信息点击 Depot 显示主体游戏 `933111`，中文语音包 `933113`

3.  打开 steam 游戏安装目录如 `D:\steam\steamapps`，找到形如 `appmanifest_933110.acf` 这样的配置文件，备份一份，然后找出来关键信息。

	比如需要玩的版本的 `manifest`，这里我以2021 年 9 月 14 日版本 [8640815080218763479](https://steamdb.info/depot/933111/history/?changeid=M:8640815080218763479) 为例

4.  伪造 `appmanifest_933110.acf` 骗过更新器 , 去 steamdb 找到最新版本的 `manifest` 和 `buildid` 

![image](https://user-images.githubusercontent.com/21209416/137933796-2af13fab-8c75-4c9c-a9e5-64ed5bca1617.png)

- 把老版本的 `8640815080218763479` 改成最新版本 `4771437915371768058`

- 同时 `StateFlags`	 改成 	`4`

- `"LastUpdated"` 最好改成游戏更新后的 UNIX 时间比如：	"1634099906" （2021-10-19 22:49:15）

- "buildid"	 改成最新版本 "7500522"

- size 类大小理论上应该不用改 **【未充分测试】**

- 这些改成如下

```
"BytesToDownload"		"0"
"BytesDownloaded"		"0"
"BytesToStage"		"0"
"BytesStaged"		"0"
"AutoUpdateBehavior"		"0"
"AllowOtherDownloadsWhileRunning"		"0"
"ScheduledAutoUpdate"		"0"
```

给一个我改好的例子（**不可直接用，参考着改!!**）：

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

	然后检查 steam 更新目录`D:\steam\steamapps\downloading`有无下载文件，有的干掉, 直接进入游戏目录打开游戏即可。


## 或者下载老版本

借助 [DepotDownloader](https://github.com/SteamRE/DepotDownloader) ，下载之后在 depotdownloader 目录新建一个批处理。

形如


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
使用命令行登录下载，如果觉得慢或许可以试试 [proxychains-windows](https://github.com/shunf4/proxychains-windows) ，方法自行研究。

等待下载完毕后，拷到游戏安装目录，并且如上面伪装一个 `appmanifest` 即可。

或者等自己下载完新版本，备份新游戏路径，然后把老版本拷入进去打开即可。

理论上只要伪装好 `appmanifest`就行，此外猜测每次游戏更新都要伪装最新版【还未测试】。


## TODO

- 本文有效性需充分验证

- 翻译成其他语言



### PS

等我写完了我才发现有 https://github.com/Jack-Myth/SteamDepotDownloader-GUI 这种东西 2333333

