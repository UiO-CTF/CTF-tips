# mobile hacking tips

## Tools
* jdgui
* [jadx](https://github.com/skylot/jadx)
* dex2jar (dex-tools)
* hopper disassembler
* [Frida](https://www.frida.re/docs/home/)
* apk-tool
* drozer
* [JDO](https://github.com/fileoffset/JDO) - Java DeObfuscator
* [kwetza](https://github.com/sensepost/kwetza)

## jd-gui

### Having problems running jd-gui
`jd-gui` does not always work too well with Java 9 or 10. 
Try running the following command in the the jd-gui folder:
```
java --add-opens java.base/jdk.internal.loader=ALL-UNNAMED --add-opens jdk.zipfs/jdk.nio.zipfs=ALL-UNNAMED -jar jd-gui-1.4.0.jar
```

## How to contribute
1. Find a folder associated to your contribution
    * It doesn't exist. Then make a new folder!
2. Make your changes, and send a pull request ;) 
