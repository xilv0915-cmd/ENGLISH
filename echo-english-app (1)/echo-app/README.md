# Echo 英语陪练 APP(安卓 v0.2)

## 免费生成 APK(无需安装任何开发环境)
1. 注册 GitHub 账号,新建一个仓库(Public 或 Private 均可)。
2. 把本文件夹内的所有文件(含隐藏文件夹 .github)上传到仓库。
3. 打开仓库的 Actions 页面,运行 "Build Android APK"(上传后会自动运行,约 5–8 分钟)。
4. 运行完成后,在页面底部 Artifacts 下载 Echo-English-APK,解压得到 app-debug.apk。
5. 传到安卓手机安装(需允许"安装未知来源应用"),首次使用时允许麦克风权限。

## 手机端语音设置(决定能否免翻墙)
- 语音识别:使用手机系统自带的识别服务。国产手机(华为/小米/OPPO/vivo)自带的语音引擎可直接使用;若提示不可用,请在系统设置中启用语音输入服务,并下载英语离线语音包。
- 朗读:使用系统 TTS。请在 设置 > 辅助功能/语言 > 文字转语音 中确认已安装英语(en-US)语音。
- 无法识别时,APP 内仍可文字输入回答。

## 本地调试
npm install && npx cap add android && npx cap sync android && npx cap open android


## v0.3:离线 AI 自由对话(小米 14)
APP 的"🤖 自由"标签会连接手机本地的 llama-server(OpenAI 兼容接口),全程不联网。
1. 安装 Termux(从 GitHub Releases 或 F-Droid 下载 APK)。
2. 在 Termux 中依次执行:
   pkg update && pkg install -y llama-cpp curl
   curl -L -o qwen.gguf "https://modelscope.cn/models/Qwen/Qwen2.5-1.5B-Instruct-GGUF/resolve/master/qwen2.5-1.5b-instruct-q4_k_m.gguf"
   (链接失效时,在 modelscope.cn 搜索 Qwen2.5-1.5B-Instruct-GGUF,下载 q4_k_m 文件)
   termux-wake-lock
   llama-server -m qwen.gguf -c 2048 --host 127.0.0.1 --port 8080 -t 6
3. 保持 Termux 在后台运行(系统设置里把 Termux 和本 APP 的电池策略设为"无限制")。
4. 打开 Echo APP > 🤖 自由 > 选择水平开始聊。
想要更聪明可换 Qwen2.5-3B(小米 14 内存充足,速度会慢一些)。

## v0.4:📷 扫读
拍照或选图,离线识别英文(Tesseract,识别引擎和英文数据已打包在 www/tess,无需联网),点单词听发音,或朗读全文/慢速朗读。首次识别需加载约 2–3 秒。印刷体效果好,手写体较差。
