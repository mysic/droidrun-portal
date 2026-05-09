# If you use a proxy (e.g. 127.0.0.1:7890), add this to gradle.properties (create if not exists):
#
# systemProp.http.proxyHost=127.0.0.1
# systemProp.http.proxyPort=7890
# systemProp.https.proxyHost=127.0.0.1
# systemProp.https.proxyPort=7890
#
# Or set environment variables before building:
# export http_proxy=http://127.0.0.1:7890
# export https_proxy=http://127.0.0.1:7890

WebRTC 功能我想预览一下，怎么操作？
credits 是干什么用的？


# compile and package APK
cd /home/mysic/workspaces/android-automatic/droidrun-portal

# 1) compile and package debug APK (run from project root)
chmod +x gradlew
./gradlew --no-daemon assembleDebug

# debug APK path
ls -lh app/build/outputs/apk/debug/app-debug.apk

# 2) compile and package release APK (unsigned)
./gradlew --no-daemon assembleRelease

# release APK path
ls -lh app/build/outputs/apk/release/app-release-unsigned.apk
