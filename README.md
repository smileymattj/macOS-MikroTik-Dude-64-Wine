# macOS-MikroTik-Dude-64-Wine
Run 32-bit MikroTik Dude Client on macOS Catalina (64-bit only) or later


## Resource Links ##

https://www.xquartz.org<br>
https://github.com/Gcenx/WineskinServer/releases<br>
https://mikrotik.com/download<br>
https://www.nirsoft.net/utils/resources_extract.html<br>


## Create Temp Working Directory ##
mkdir WineBuilds<br>
cd WineBuilds<br>


## Download Assets ##
curl -O -L https://github.com/XQuartz/XQuartz/releases/download/XQuartz-2.8.5/XQuartz-2.8.5.pkg<br>
curl -O -L https://github.com/Gcenx/WineskinServer/releases/download/V1.8.4.2/WS11WineCX21.2.0.tar.7z<br>
curl -O -L https://download.mikrotik.com/routeros/7.8/dude-install-7.8.exe<br>
curl -O -L https://www.nirsoft.net/utils/resourcesextract.zip<br>

curl -O -L https://raw.githubusercontent.com/smileymattj/macOS-MikroTik-Dude-64-Wine/main/Dude.app/Contents/Info.plist<br>
curl -O -L https://raw.githubusercontent.com/smileymattj/macOS-MikroTik-Dude-64-Wine/main/Dude.app/Contents/MacOS/Dude<br>


## Install XQuartz
open XQuartz-2.8.5.pkg<br>


## Install Wine ##
open WS11WineCX21.2.0.tar.7z<br>

cd wswine.bundle<br>
sudo rm -r share/wine/gecko<br>
sudo mkdir /usr/local/wine<br>
sudo mv * /usr/local/wine/<br>


## Install Dude ##
/usr/local/wine/bin/wine32on64 dude-install-7.8.exe<br>

/usr/local/wine/bin/wine32on64 ~/.wine/drive_c/Program\ Files/Dude/dude.exe<br>


## Create Application Shortcut ##
mkdir -p Dude.app/Contents/MacOS<br>
mkdir -p Dude.app/Contents/Resources<br>

mv Info.plist Dude.app/Contents/<br>
mv Dude Dude.app/Contents/MacOS/<br>
chmod +x Dude.app/Contents/MacOS/Dude<br>


## Extract & Set Icon ##
cp ~/.wine/drive_c/Program\ Files/Dude/dude.exe dude.exe<br>

open resourcesextract.zip<br>

/usr/local/wine/bin/wine32on64 resourcesextract/ResourcesExtract.exe<br>

open Dude_200.ico<br>

mkdir Icon.iconset<br>
mv icon_128x128.png Icon.iconset/icon_128x128.png<br>

iconutil -c icns Icon.iconset<br>

mv Icon.icns Dude.app/Contents/Resources/<br>


## Install Dude Application ## 
mv Dude.app /Applications/<br>

## Cleanup ##
cd ..<br>
rm -r WineBuilds<br>
