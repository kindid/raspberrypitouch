=================================================================================================

monitor - does not work pefectly on RPi3

https://raspberrypi.stackexchange.com/questions/62403/touchscreen-lcd-usb-hannsg-and-elo-behaving-unexpected-on-raspi-3
https://raspberrypi.stackexchange.com/questions/60383/rpi3-and-larger-touch-screen-monitors
https://www.hannspree.eu/support/faq/touch-monitors/#1528373570561-44b67852-4510
win8
        https://www.hannspree.eu/wp-content/uploads/2019/04/WIN8.rar

Use a windows box - i got a question about config files and ignored it
        It's mostly chinglish so be very careful when reading the instructions

=================================================================================================

Also... you need to install...

sudo apt-get install xinput-calibrator

===========================================================================================================

https://www.tal.org/tutorials/building-qt-512-raspberry-pi

Minor bug *src-5.12.3 should be *src-5.12.5

# i've hacked this about and added a TON of skips
-skip qtactiveqt

PKG_CONFIG_LIBDIR=/usr/lib/arm-linux-gnueabihf/pkgconfig:/usr/share/pkgconfig \
../qt-everywhere-src-5.12.5/configure -platform linux-rpi3-g++ \
-v \
-opengl es2 -eglfs \
-no-gtk \
-opensource -confirm-license -release \
-reduce-exports \
-force-pkg-config \
-nomake examples -no-compile-examples \
-skip qtwayland \
-skip qtwebengine \
-skip qt3d \
-skip qtscript \
-skip qtcharts \
-skip qtandroidextras \
-skip qtmultimedia \
-skip qtactiveqt \
-skip qtmacextras \
-skip qtdatavis3d \
-skip qtcanvas3d \
-skip qtvirtualkeyboard \
-skip qtwebview \
-skip qtwinextras \
-no-feature-geoservices_mapboxgl \
-qt-pcre \
-no-pch \
-ssl \
-evdev \
-system-freetype \
-fontconfig \
-glib \
-prefix /opt/Qt5.12 \
-qpa eglfs


this has some beeped up dependency... lets GO...

-skip qtlocation \

# TODO;

===========================================================================================================


/home/pi/qt/build
make



===========================================================================================================


QSG_ATLAS_WIDTH
QSG_ATLAS_HEIGHT
QSG_ATLAS_SIZE_LIMIT
QT_QPA_EGLFS_PHYSICAL_HEIGHT
QT_QPA_EGLFS_PHYSICAL_WIDTH

===========================================================================================================

EGLFS will drive you insane. You can't quite applications very easily at all (or at all)

Solution - add an escape key handler very high up the stack (top level widget for example)

        Alternatively press the "big bomb" icon (which really shouldn't be in production builds)


===========================================================================================================



root@raspberryyocto:~# mkdir /mnt/fat
root@raspberryyocto:~# mount /dev/mmcblk0p1 /mnt/fat
root@raspberryyocto:~# vi /mnt/fat/config.txt


except not vi

add gpu_mem=256

===========================================================================================================


Configure summary:

Build type: linux-rpi3-g++ (arm, CPU features: neon)
Compiler: gcc 6.3.0
Configuration: use_gold_linker enable_new_dtags largefile neon shared rpath release c++11 c++14 concurrent dbus reduce_exports stl
Build options:
  Mode ................................... release
  Optimize release build for size ........ no
  Building shared libraries .............. yes
  Using C standard ....................... C11
  Using C++ standard ..................... C++14
  Using ccache ........................... no
  Using gold linker ...................... yes
  Using new DTAGS ........................ yes
  Using precompiled headers .............. no
  Using LTCG ............................. no
  Target compiler supports:
    NEON ................................. yes
  Build parts ............................ libs tools
Qt modules and options:
  Qt Concurrent .......................... yes
  Qt D-Bus ............................... yes
  Qt D-Bus directly linked to libdbus .... yes
  Qt Gui ................................. yes
  Qt Network ............................. yes
  Qt Sql ................................. yes
  Qt Testlib ............................. yes
  Qt Widgets ............................. yes
  Qt Xml ................................. yes
Support enabled for:
  Using pkg-config ....................... yes
  udev ................................... yes
  Using system zlib ...................... yes
Qt Core:
  DoubleConversion ....................... yes
    Using system DoubleConversion ........ no
  GLib ................................... yes
  iconv .................................. no
  ICU .................................... yes
  Tracing backend ........................ <none>
  Logging backends:
    journald ............................. no
    syslog ............................... no
    slog2 ................................ no
  Using system PCRE2 ..................... no
Qt Network:
  getifaddrs() ........................... yes
  IPv6 ifname ............................ yes
  libproxy ............................... no
  Linux AF_NETLINK ....................... yes
  OpenSSL ................................ yes
    Qt directly linked to OpenSSL ........ no
  OpenSSL 1.1 ............................ yes
  DTLS ................................... yes
  SCTP ................................... no
  Use system proxies ..................... yes
Qt Gui:
  Accessibility .......................... yes
  FreeType ............................... yes
    Using system FreeType ................ yes
  HarfBuzz ............................... yes
    Using system HarfBuzz ................ no
  Fontconfig ............................. yes
  Image formats:
    GIF .................................. yes
    ICO .................................. yes
    JPEG ................................. yes
      Using system libjpeg ............... yes
    PNG .................................. yes
      Using system libpng ................ yes
  EGL .................................... yes
  OpenVG ................................. yes
  OpenGL:
    Desktop OpenGL ....................... no
    OpenGL ES 2.0 ........................ yes
    OpenGL ES 3.0 ........................ no
    OpenGL ES 3.1 ........................ no
    OpenGL ES 3.2 ........................ no
  Vulkan ................................. no
  Session Management ..................... yes
Features used by QPA backends:
  evdev .................................. yes
  libinput ............................... yes
  INTEGRITY HID .......................... no
  mtdev .................................. no
  tslib .................................. no
  xkbcommon .............................. yes
  X11 specific:
    XLib ................................. no
    XCB Xlib ............................. no
    EGL on X11 ........................... no
QPA backends:
  DirectFB ............................... no
  EGLFS .................................. yes
  EGLFS details:
    EGLFS OpenWFD ........................ no
    EGLFS i.Mx6 .......................... no
    EGLFS i.Mx6 Wayland .................. no
    EGLFS RCAR ........................... no
    EGLFS EGLDevice ...................... no
    EGLFS GBM ............................ no
    EGLFS VSP2 ........................... no
    EGLFS Mali ........................... no
    EGLFS Raspberry Pi ................... yes
    EGLFS X11 ............................ no
  LinuxFB ................................ yes
  VNC .................................... yes
  Mir client ............................. no
Qt Sql:
  SQL item models ........................ yes
Qt Widgets:
  GTK+ ................................... no
  Styles ................................. Fusion Windows
Qt PrintSupport:
  CUPS ................................... no
Qt Sql Drivers:
  DB2 (IBM) .............................. no
  InterBase .............................. no
  MySql .................................. no
  OCI (Oracle) ........................... no
  ODBC ................................... no
  PostgreSQL ............................. no
  SQLite2 ................................ no
  SQLite ................................. yes
    Using system provided SQLite ......... no
  TDS (Sybase) ........................... no
Qt Testlib:
  Tester for item models ................. yes
Qt SerialBus:
  Socket CAN ............................. yes
  Socket CAN FD .......................... yes
Further Image Formats:
  JasPer ................................. no
  MNG .................................... no
  TIFF ................................... yes
    Using system libtiff ................. no
  WEBP ................................... yes
    Using system libwebp ................. no
Qt QML:
  QML network support .................... yes
  QML debugging and profiling support .... yes
  QML sequence object .................... yes
  QML list model ......................... yes
  QML XML http request ................... yes
  QML Locale ............................. yes
  QML delegate model ..................... yes
Qt Quick:
  Direct3D 12 ............................ no
  AnimatedImage item ..................... yes
  Canvas item ............................ yes
  Support for Qt Quick Designer .......... yes
  Flipable item .......................... yes
  GridView item .......................... yes
  ListView item .......................... yes
  TableView item ......................... yes
  Path support ........................... yes
  PathView item .......................... yes
  Positioner items ....................... yes
  Repeater item .......................... yes
  ShaderEffect item ...................... yes
  Sprite item ............................ yes
Qt Scxml:
  ECMAScript data model for QtScxml ...... yes
Qt Gamepad:
  SDL2 ................................... no
Qt 3D:
  Assimp ................................. yes
  System Assimp .......................... no
  Output Qt3D Job traces ................. no
  Output Qt3D GL traces .................. no
  Use SSE2 instructions .................. no
  Use AVX2 instructions .................. no
  Aspects:
    Render aspect ........................ yes
    Input aspect ......................... yes
    Logic aspect ......................... yes
    Animation aspect ..................... yes
    Extras aspect ........................ yes
Qt 3D Renderers:
  OpenGL Renderer ........................ yes
Qt 3D GeometryLoaders:
  Autodesk FBX ........................... no
Qt Bluetooth:
  BlueZ .................................. no
  BlueZ Low Energy ....................... no
  Linux Crypto API ....................... no
  WinRT Bluetooth API (desktop & UWP) .... no
Qt Sensors:
  sensorfw ............................... no
Qt Quick Controls 2:
  Styles ................................. Default Fusion Imagine Material Universal
Qt Quick Templates 2:
  Hover support .......................... yes
  Multi-touch support .................... yes
Qt Positioning:
  Gypsy GPS Daemon ....................... no
  WinRT Geolocation API .................. no
Qt Location:
  Qt.labs.location experimental QML plugin . yes
  Geoservice plugins:
    OpenStreetMap ........................ yes
    HERE ................................. yes
    Esri ................................. yes
    Mapbox ............................... yes
    MapboxGL ............................. no
    Itemsoverlay ......................... yes
QtXmlPatterns:
  XML schema support ..................... yes
Qt Multimedia:
  ALSA ................................... no
  GStreamer 1.0 .......................... no
  GStreamer 0.10 ......................... no
  Video for Linux ........................ yes
  OpenAL ................................. no
  PulseAudio ............................. no
  Resource Policy (libresourceqt5) ....... no
  Windows Audio Services ................. no
  DirectShow ............................. no
  Windows Media Foundation ............... no
Qt Tools:
  QDoc ................................... no
