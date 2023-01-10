# VideoStation-FFMPEG-Patcher

<p align="center">
  <img src="https://github.com/AlexPresso/VideoStation-FFMPEG-Patcher/blob/main/banner.png?raw=true" height=200px alt="Banner">
</p>

This patcher is designed to continue the work of [Benjamin Poncet](https://github.com/BenjaminPoncet), to enable **DTS**, **EAC3** and **TrueHD** support to Synology VideoStation, by replacing the original ffmpeg and gstreamer files by a wrapper using SynoCommunity packages.

Huge thanks to [Benjamin Poncet](https://github.com/BenjaminPoncet), [Vincent Fortier](https://github.com/th0ma7), [SynoCommunity](https://github.com/SynoCommunity) and all contributors.

### Also want to patch MediaServer ? [there you go](https://github.com/AlexPresso/mediaserver-ffmpeg-patcher)

## Dependencies
- DSM 6.2.2-24922 Update 4 (and above)
- Video Station 2.4.6-1594 (and above)
- SynoCommunity ffmpeg 4.2.1-23 (and above) ([help](https://synocommunity.com/#easy-install))

## Supported / Unsupported scenarios
- **[DTS or EAC3 or TrueHD] + [Any non HEVC standard video format]**: ✅
- **[no DTS, no EAC3, no TrueHD] + [HEVC]**: ✅
- **[DTS or EAC3 or TrueHD] + [HEVC]**: ⚠️ Not working on architectures where Advanced Media Extensions uses GStreamer for audio decoding (Please don't submit any more issue related to this scenario, I'm working on it, see [#33](https://github.com/AlexPresso/VideoStation-FFMPEG-Patcher/pull/33))

## Instructions
- Check that you meet the required [dependencies](https://github.com/AlexPresso/VideoStation-FFMPEG-Patcher#dependencies)
- Install SynoCommunity ffmpeg ([help](https://synocommunity.com/#easy-install))
- If you plan to play HEVC / AAC videos, install Advanced Media Extensions
- Connect to your NAS using SSH (admin user required) ([help](https://www.synology.com/en-global/knowledgebase/DSM/tutorial/General_Setup/How_to_login_to_DSM_with_root_permission_via_SSH_Telnet))
- Use the command `sudo -i` to switch to root user
- Use the [following](https://github.com/AlexPresso/VideoStation-FFMPEG-Patcher#usage) command (Basic command) to execute the patch
- You'll have to re-run the patcher everytime you update VideoStation, Advanced Media Extensions and DSM

## Usage
Basic command:  
`curl https://raw.githubusercontent.com/AlexPresso/VideoStation-FFMPEG-Patcher/main/patcher.sh | bash`   
With options:  
`curl https://raw.githubusercontent.com/AlexPresso/VideoStation-FFMPEG-Patcher/main/patcher.sh | bash -s -- <flags>`

| Flags | Required | Description                                                                     | Default |
|-------|----------|---------------------------------------------------------------------------------|---------|
| -a    | No       | Action flag: choose between `patch` or `unpatch` ; example: `-a patch`          | patch   |
| -b    | No       | Branch flag: allows you to choose the wrapper branch to use ; example `-b main` | main    |                                                  



# 2023.01.10. 적용

1. SSH 접속 & sudo -i
2. 이 repo의 "patcher.sh" get 받아오기
```bash
curl https://raw.githubusercontent.com/AlexPresso/VideoStation-FFMPEG-Patcher/main/patcher.sh | bash
```
그러며 자동 videoStation 재시작까지 shell script에서 재시작해줌

```bash
 % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  4396  100  4396    0     0  10247      0 --:--:-- --:--:-- --:--:-- 10223
[2023-01-10 13:04:22] [INFO] ffmpeg-patcher v2.0
[2023-01-10 13:04:23] [Message of the day]

The patcher was redesigned to include an unpatch procedure.

I'm aware of an issue with HEVC and I'm working on it.

As always, please let me know of any issue you could have.

[2023-01-10 13:04:23] [INFO] You're running DSM 7.0.1
[2023-01-10 13:04:23] [INFO] ====== Patching procedure (branch: main) ======
[2023-01-10 13:04:23] [INFO] Saving current ffmpeg as ffmpeg.orig
[2023-01-10 13:04:23] [INFO] Downloading and installing ffmpeg's wrapper...
[2023-01-10 13:04:24] [INFO] Patching CodecPack's ffmpeg41
[2023-01-10 13:04:24] [INFO] Patching CodecPack's ffmpeg27
[2023-01-10 13:04:24] [INFO] Saving current libsynovte.so as libsynovte.so.orig
[2023-01-10 13:04:24] [INFO] Enabling eac3, dts and truehd
[2023-01-10 13:04:24] [INFO] Restarting CodecPack...
restart package [CodecPack] successfully
[2023-01-10 13:06:37] [INFO] Restarting VideoStation...
restart package [VideoStation] successfully

[2023-01-10 13:08:02] [INFO] Done patching, you can now enjoy your movies ;) (please add a star to the repo if it worked for you)
```

3. videoStation이나 ffmpeg 버전 업데이트시마다 patch .sh 재실행해줘야 함!!
