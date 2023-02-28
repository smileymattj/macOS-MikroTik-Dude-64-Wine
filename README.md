# macOS-MikroTik-Dude-64-Wine
Run 32-bit MikroTik Dude Client on macOS Catalina (64-bit only) or later


## Resource Links ##

https://www.xquartz.org<br>
https://github.com/Gcenx/WineskinServer/releases<br>
https://mikrotik.com/download<br>
https://www.nirsoft.net/utils/resources_extract.html<br>


## Create Temp Working Directory ##
mkdir WineBuilds


## Download Assets ##
curl -O -L https://github.com/XQuartz/XQuartz/releases/download/XQuartz-2.8.5/XQuartz-2.8.5.pkg<br>
curl -O -L https://github.com/Gcenx/WineskinServer/releases/download/V1.8.4.2/WS11WineCX21.2.0.tar.7z<br>
curl -O -L https://download.mikrotik.com/routeros/7.8/dude-install-7.8.exe<br>
curl -O -L https://www.nirsoft.net/utils/resourcesextract.zip<br>

curl -O -L https://raw.githubusercontent.com/smileymattj/macOS-MikroTik-Dude-64-Wine/main/Dude.app/Contents/Info.plist<br>
curl -O -L https://raw.githubusercontent.com/smileymattj/macOS-MikroTik-Dude-64-Wine/main/Dude.app/Contents/MacOS/Dude<br>


## Install XQuartz
open XQuartz-2.8.5.pkg


## Install Wine ##
open WS11WineCX21.2.0.tar.7z

cd wswine.bundle
sudo rm -r share/wine/gecko
sudo mkdir /usr/local/wine
sudo mv * /usr/local/wine/


## Install Dude ##
/usr/local/wine/bin/wine32on64 dude-install-7.8.exe

/usr/local/wine/bin/wine32on64 ~/.wine/drive_c/Program\ Files/Dude/dude.exe


## Create Application Shortcut ##
mkdir -p Dude.app/Contents/MacOS
mkdir -p Dude.app/Contents/Resources

mv Info.plist Dude.app/Contents/
mv Dude Dude.app/Contents/MacOS/
chmod +x Dude.app/Contents/MacOS/Dude


## Extract & Set Icon ##
cp ~/.wine/drive_c/Program\ Files/Dude/dude.exe dude.exe

open resourcesextract.zip

/usr/local/wine/bin/wine32on64 resourcesextract/ResourcesExtract.exe

open Dude_200.ico 

mkdir Icon.iconset
mv icon_128x128.png Icon.iconset/icon_128x128.png

iconutil -c icns Icon.iconset

mv Icon.icns Dude.app/Contents/Resources/


## Install Dude Application ## 
mv Dude.app /Applications/

## Cleanup ##
cd ..
rm -r WineBuilds
