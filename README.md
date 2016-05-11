# Android-OCR-and-BluetoothSPP
Optical character recognition and send control command to Arduino via Bluetooth using BluetoothSPP Library 1) Download and install the ndk from here https://developer.android.com/tools/sdk/ndk/index.html. I had some trouble with its path in following steps so i put it in “C:\”.

2) Add that path to environment variables of the system (eg: “C:\android_ndk_r10d”) and then reboot so your machine can find it.

3) Download “tess-two-master” from here https://github.com/rmtheis/tess-two, extract it (for example in “C:\”) and rename it in “tess”.

4) Open “tess” folder and then open “tess-two” folder. Click on a blank space while pressing the shift button and select “Open command window here”.

5) Write “ndk-build” and wait until it completes (about 20min).

6) Go back in the parent folder, select “eyes-two” folder and again click on a blank space while pressing the shift button in order to open the command window.

7) Write “ndk-build” and wait.

8) Write “android update project –target 1 –path C:\tess\tess-two”. Of course I assume your “tess” folder is located in “C:\”

9) Write “ant release”. IF IT COMPLAINS go where you change your system environment variables as you did in step 2 and ADD a new variable with name “JAVA_HOME” and value the path to your jdk (eg: “C:\Program Files\Java\jdk1.8.0_40″)

10) Open a completely new Android Studio project and follow these instructions https://coderwall.com/p/eurvaq/tesseract-with-andoird-and-gradle from section “Configure tess-two with gradle” but for safety don’t delete any folder or file even if he suggests to do so. I had some trouble with “build.gradle” file in “libraries\tess-two” directory, but it is sufficient to change some value on it. In my case I have:

“classpath ‘com.android.tools.build:gradle:0.14.0′” instead of “classpath ‘com.android.tools.build:gradle:0.9.+’ ”

and

”compileSdkVersion 21 buildToolsVersion “21.0.2” defaultConfig { minSdkVersion 15 targetSdkVersion 21 } ”

instead of

”compileSdkVersion 19 buildToolsVersion “19.0.3”
defaultConfig { minSdkVersion 8 targetSdkVersion 19} ”.

Note that the last step means you have to go in “File -> Project Structure -> Select a module from the left subwindow -> Dependencies (last tab) ->Press the green “+” on your right -> Module Dependency -> OK”

11) Download this project https://github.com/GautamGupta/Simple-Android-OCR and copy&paste in your new project the code in these files: “SimpleAndroidOCRActivity.java”, “main.xml”, “strings.xml”. Of course your files may have different names (in my case “MainActivity.java”, “activity_main.xml”, “strings.xml”) so some renaming in the code may be necessary. Also open your “AndroidManifest.xml” and add at the end (but before “/manifest”) what you find between “/application” and “/manifest” in the just downloaded “AndroidManifest.xml” (it means that you have to add “uses-permissions” and “uses-feature” tag).

12) Download from here https://code.google.com/p/tesseract-ocr/downloads/list the file in the language you prefer (eg: tesseract-ocr-3.02.eng.tar.gz ), extract it and locate the file “yourLanguage.traineddata” (eg: “eng.traineddata”). Forget for a moment your Android Studio IDE, open the folder of your project and go in “app–>src–>main”. Create here a new folder and name it “assets”. Open it and create another folder named “tessdata”. Put there your .traineddata file.
