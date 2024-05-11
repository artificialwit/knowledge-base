# Kotlin update and installtion
Open terminal run below command one by one
curl -s "https://get.sdkman.io" | bash
sdk install kotlin
kotlin -version

# Command
- flutter doctor
- flutter pub outdated
- flutter pub upgrade --major-versions
- 
# Launch JSON file
```json
{
    "version": "0.2.0",
    "configurations": [
      {
        "name": "aw-web-app",
        "request": "launch",
        "type": "dart",
        "program": "lib/main.dart",
        "args": ["-d", "chrome"]
      },
      {
        "name": "aw-android-app",
        "request": "launch",
        "type": "dart",
        "deviceId": "3fad3f56"
      }
    ]
  }
```
  
