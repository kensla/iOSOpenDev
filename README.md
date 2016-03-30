#How to install iOSOpenDev manually?

OS X 10.10+ & Xcode 7+

-----

1. **Dependency**

 `brew install ldid dpkg`

2. **Theos**

 [Wiki](https://github.com/theos/theos/wiki)
    
 [Setup](http://iphonedevwiki.net/index.php/Theos/Setup)

3. **iOSOpenDev**

 [Wiki](https://github.com/kokoabim/iOSOpenDev/wiki)

 3.1. update **.zshrc**
 
 `export iOSOpenDevPath=path/to/iOSOpenDev`
 
 `export iOSOpenDevDevice=`
 
 `export PATH=$iOSOpenDevPath:$PATH`

 3.2. get **iOSOpenDev**
 
 * `git clone --recursive https://github.com/kokoabim/iOSOpenDev.git $iOSOpenDevPath`

 * copy the **templates** dir into *$iOSOpenDevPath*
 
   this version of **templates** is refined by the official one: the *ShellScript* of *BuildPhases* in **TemplateInfo.plist** is changed to `$iOSOpenDevPath/bin/iosod --xcbp`. the *[$iOSOpenDevPath]* here is not that of *.zshrc*, it is a user defined key in **Base.xctemplate**.

 3.3. setup **Xcode**

 * copy the **.xcspec** files into */Applications/Xcode/Content/Developer/Platforms/[PLATFORM_PATH]/Developer/Library/Xcode/Specifications* (mkdir if not existed)
    
 * `mkdir -p /Applications/Xcode/Content/Developer/Platforms/[PLATFORM_PATH]/Developer/usr/bin`
	
 * `ln -fhs $iOSOpenDevPath/bin/iosod /Applications/Xcode/Content/Developer/Platforms/[PLATFORM_PATH]/Developer/usr/bin`
	
 * `ln -fhs $iOSOpenDevPath/bin/ldid /Applications/Xcode/Content/Developer/Platforms/[PLATFORM_PATH]/Developer/usr/bin`
	
 3.4. setup **SDK**
 
 * add the following key/value into **[SDK_PATH]/SDKSettings.plist**:

            DefaultProperties.CODE_SIGNING_REQUIRED => NO
            DefaultProperties.ENTITLEMENTS_REQUIRED => NO
            DefaultProperties.AD_HOC_CODE_SIGNING_ALLOWED => YES
            
 * in Xcode 7.3, the private framework has been removed from iOS 9.3 SDK, so maybe you want to use iOS 9.2 SDK. once you copy iOS 9.2 SDK into *[PLATFORM_PATH]/Developer/SDKs*, you should update the **[PLATFORM_PATH]/Info.plist** as following, or else Xcode 7.3 can not recognize iOS 9.2 SDK in build settings:

             MinimumSDKVersion => 9.2

 3.5. setup **templates**
 
 * `ln -fhs $iOSOpenDevPath/templates ~/Library/Developer/Xcode/Templates/iOSOpenDev`
 * open **TemplateInfo.plist** of **Base.xctemplate** and **Empty Project.xctemplate** with Xcode, then set the value of user defined key *[iOSOpenDevPath]* to *$HOME/Tools/iOS/iOSOpenDev*.
