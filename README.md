# ios17_firebase

This is a template to set up the toolchain and integrate Firebase into Flutter project with iOS 17. __NOTE: None of the instructions was created by myself, I just collected them in one place, so it's convinient for you. All links are in the description__

## Getting Started

### 1. Update Xcode

To do that, either do it in Settings -> Software update or open the Terminal and type:

    $ sudo rm -rf /Library/Developer/CommandLineTools
    $ xcode-select --install

### 2. Add a new Simulator

Refer to this instruction:
https://developer.apple.com/documentation/safari-developer-tools/adding-additional-simulators

Open Xcode -> Settings -> Platforms -> Plus in the lower left corner -> Choose iOS 17 -> Download and install -> wait.

### 3. Create Simulator

Open the Simulator app.

File -> New Simulator -> Give it a name, choose an OS and device type -> Create.

### 4. Clone this Repository 

    $ git clone https://github.com/karchevskii/ios17_firebase.git

### 5. Configure Firebase

    $ firebase login
    $ flutterfire configure     <- create or choose your existing project

Refer: https://firebase.google.com/docs/flutter/setup?platform=ios

### 6. Edited Podfile

I also added this code to Podfile:

    post_install do |installer|
    installer.pods_project.targets.each do |target|
        flutter_additional_ios_build_settings(target)
        target.build_configurations.each do |config|
            xcconfig_path = config.base_configuration_reference.real_path
            xcconfig = File.read(xcconfig_path)
            xcconfig_mod = xcconfig.gsub(/DT_TOOLCHAIN_DIR/, "TOOLCHAIN_DIR")
            File.open(xcconfig_path, "w") { |file| file << xcconfig_mod }
        end
    end
    end


#### You just need to run:
    $ brew upgrade cocoapods
    $ pod update

Refer: https://stackoverflow.com/a/77142190/16379096

__That's it. Start your Flutter app as usual.__
