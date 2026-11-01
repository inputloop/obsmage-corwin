# STAGES

<!-- omg:pin 5d207251e90f1ca62aa3aede8b8ca1cf3989a5f4720ffc619a54e3404a737a69 -->
The single-file roll-up of every obsmage atom. Edit a block below and run
`omg_atoms.py unroll STAGES.md atoms/` to send the change back. Secret values never
appear here (`@secret(len=N)`). Generated; the pin above is the atoms it came from.

## GSUS_Tech/basic.ini

```kv set=GSUS_Tech/basic.ini/set-AdvOut.kv
Encoder=jim_nvenc
ApplyServiceSettings=true
UseRescale=false
TrackIndex=1
VodTrackIndex=2
RecType=Standard
RecFilePath=C:\\Users\\corwi\\Videos
RecFormat2=hybrid_mp4
RecUseRescale=false
RecTracks=1
RecEncoder=none
FLVTrack=1
StreamMultiTrackAudioMixes=1
FFOutputToFile=true
FFFilePath=C:\\Users\\corwi\\Videos
FFExtension=mp4
FFVBitrate=6000
FFVGOPSize=250
FFUseRescale=false
FFIgnoreCompat=false
FFABitrate=160
FFAudioMixes=1
Track1Bitrate=160
Track2Bitrate=160
Track3Bitrate=160
Track4Bitrate=160
Track5Bitrate=160
Track6Bitrate=160
RecSplitFileTime=15
RecSplitFileSize=2048
RecRB=false
RecRBTime=20
RecRBSize=512
AudioEncoder=ffmpeg_aac
RecAudioEncoder=ffmpeg_aac
```

```kv set=GSUS_Tech/basic.ini/set-Audio.kv
MonitoringDeviceId=default
MonitoringDeviceName=Default
SampleRate=48000
ChannelSetup=Stereo
MeterDecayRate=23.53
PeakMeterType=0
```

```kv set=GSUS_Tech/basic.ini/set-Auth.kv
Type=Twitch
```

```kv set=GSUS_Tech/basic.ini/set-General.kv
Name=GSUS Tech
```

```kv set=GSUS_Tech/basic.ini/set-Hotkeys.kv
OBSBasic.SaveReplayBuffer={"bindings":[]}
```

```kv set=GSUS_Tech/basic.ini/set-Output.kv
Mode=Simple
BindIP=default
FilenameFormatting=%CCYY-%MM-%DD %hh-%mm-%ss
DelayEnable=false
DelaySec=20
DelayPreserve=true
Reconnect=true
RetryDelay=2
MaxRetries=25
IPFamily=IPv4+IPv6
NewSocketLoopEnable=false
LowLatencyEnable=false
```

```kv set=GSUS_Tech/basic.ini/set-Panels.kv
CookieId=3FA955918D7DFE63
```

```kv set=GSUS_Tech/basic.ini/set-SimpleOutput.kv
VBitrate=6000
StreamEncoder=nvenc
RecEncoder=nvenc
RecQuality=Small
FilePath=C:\\Users\\corwi\\Videos
RecFormat2=hybrid_mp4
ABitrate=160
UseAdvanced=false
Preset=veryfast
NVENCPreset2=p5
RecRB=false
RecRBTime=20
RecRBSize=512
RecRBPrefix=Replay
StreamAudioEncoder=aac
RecAudioEncoder=aac
RecTracks=1
```

```kv set=GSUS_Tech/basic.ini/set-Stream1.kv
IgnoreRecommended=false
EnableMultitrackVideo=false
MultitrackVideoMaximumAggregateBitrateAuto=true
MultitrackVideoMaximumVideoTracksAuto=true
```

```kv set=GSUS_Tech/basic.ini/set-Twitch.kv
Name=mplscorwin
DockState=AAAA/wAAAAD9AAAABAAAAAAAAALaAAAECPwCAAAAA/wAAABvAAAB2gAAARsBAAAZ+gAAAAMBAAAABPsAAABcAG0AcABsAHMAQwBvAHIAdwBpAG4AIAAtACAAVAB3AGkAdABjAGgAIABBAGMAdABpAHYAaQB0AHkAIABGAGUAZQBkAF8AZQB4AHQAcgBhAEIAcgBvAHcAcwBlAHIBAAAAAP////8AAABQAP////sAAABYAG0AcABsAHMAQwBvAHIAdwBpAG4AIAAtACAAVAB3AGkAdABjAGgAIABTAHQAcgBlAGEAbQAgAEkAbgBmAG8AXwBlAHgAdAByAGEAQgByAG8AdwBzAGUAcgEAAAAA/////wAAAFAA////+wAAABIAbQBpAHgAZQByAEQAbwBjAGsBAAAAAP////8AAAEBAP////sAAAAYAGMAbwBuAHQAcgBvAGwAcwBEAG8AYwBrAQAAAOIAAAH4AAAAzAD////8AAABvgAAAJwAAAAAAP////oAAAAAAQAAAAH7AAAAFAB0AHcAaQB0AGMAaABJAG4AZgBvAQAAAAD/////AAAAAAAAAAD8AAACTQAAAioAAAChAQAAGfoAAAABAQAAAAP7AAAAHgB0AHIAYQBuAHMAaQB0AGkAbwBuAHMARABvAGMAawEAAAAA/////wAAAIIA////+wAAABQAcwBjAGUAbgBlAHMARABvAGMAawEAAAAA/////wAAAJgA////+wAAABYAcwBvAHUAcgBjAGUAcwBEAG8AYwBrAQAAAAAAAAF5AAAAmAD///8AAAABAAAAyAAAA2T8AgAAAAP7AAAAFgB0AHcAaQB0AGMAaABTAHQAYQB0AHMCAAADWwAAAYQAAADIAAAA+vsAAAAUAHQAdwBpAHQAYwBoAEYAZQBlAGQCAAACAAAAAOUAAAEsAAACivsAAAAUAHQAdwBpAHQAYwBoAEMAaABhAHQAAAAAbwAAA2QAAAEsAP///wAAAAIAAAeAAAAAUPwBAAAAAvsAAABKAG0AcABsAHMAQwBvAHIAdwBpAG4AIAAtACAAVAB3AGkAdABjAGgAIABDAGgAYQB0AF8AZQB4AHQAcgBhAEIAcgBvAHcAcwBlAHIBAAAAAAAABqkAAABQAP////sAAABQAEAAQwBvAHIAdwBpAG4AQgByAHUAcwB0ACAALQAgAFkAbwB1AFQAdQBiAGUAIABDAGgAYQB0AF8AZQB4AHQAcgBhAEIAcgBvAHcAcwBlAHIBAAAGrQAAANMAAABQAP///wAAAAMAAAeAAAAAjvwBAAAAAfsAAAASAHMAdABhAHQAcwBEAG8AYwBrAgAAAloAAAHXAAACcQAAAO0AAASiAAAECAAAAAQAAAAEAAAACAAAAAj8AAAAAA==
RefreshToken=@secret(len=50)
Token=@secret(len=30)
ExpireTime=1793494769
ScopeVer=1
AddonChoice=3
UUID=ccb0594d101e4e6885a3c41bc39844bc
```

```kv set=GSUS_Tech/basic.ini/set-Video.kv
BaseCX=1920
BaseCY=1080
OutputCX=1920
OutputCY=1080
FPSType=0
FPSCommon=60
FPSInt=30
FPSNum=30
FPSDen=1
ScaleType=bicubic
ColorFormat=NV12
ColorSpace=709
ColorRange=Partial
SdrWhiteLevel=300
HdrNominalPeakLevel=1000
```

```kv set=GSUS_Tech/basic.ini/set-WebsocketAPI.kv
ServerEnabled=true
ServerPort=4444
DebugEnabled=false
AlertsEnabled=false
AuthRequired=true
AuthSecret=@secret(len=44)
AuthSalt=@secret(len=44)
```

## GSUS_Tech/service.json

```kv set=GSUS_Tech/service.json/_all.kv
/settings/key:="@secret(len=44)"
/settings/server:="auto"
/settings/service:="Twitch"
/type:="rtmp_common"
```

## GSUS_Tech/streamEncoder.json

```kv set=GSUS_Tech/streamEncoder.json/_all.kv
:=[]
```

