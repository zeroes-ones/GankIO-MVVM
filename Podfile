platform :ios, '10.0'
use_frameworks!

target 'GankIO-MVVM' do
 
  # Networking
  pod 'Moya/RxSwift', '~> 13.0'
  pod 'ReachabilitySwift'
  
  # Rx Extensions
  pod 'RxCocoa'
  pod 'RxSwift'
  pod 'RxSwiftExt'
  pod 'RxDataSources'
  #pod 'RxGesture'
  #pod 'RxOptional'
  #pod 'RxTheme'
  pod 'RxViewController'
  pod 'NSObject+Rx' #NSObject has rx operator
  pod 'Result'
  #pod 'RxAnimated'
  
  # create uiview use then for sugar
  # has bug in xcode 10.2 -- no code prompt
  pod 'Then'

  # JSON Mapping support moya13
  pod 'Moya-ObjectMapper/RxSwift', :git => 'https://github.com/leasual/Moya-ObjectMapper.git'
  #pod 'ObjectMapper'
  # Image
  # it will use large memory to cache image
  #pod 'Kingfisher'
  pod 'SDWebImage'
  # Date
  #pod 'DateToolsSwift'
  pod 'SwiftDate'
  
  # Keyboard
  pod 'IQKeyboardManagerSwift'

  # Auto Layout
  pod 'SnapKit'

  # Code Quality
  #pod 'FLEX'
 
  # Logging
  pod 'CocoaLumberjack/Swift'

  # Tool
  pod 'SwiftLint'
  pod 'R.swift'
  
  # DI
  pod 'Swinject'

  # Color
  #pod 'ChameleonFramework/Swift'

  # Database
  #pod 'RxRealm'
  #pod 'RealmSwift'
  
  # UI
  pod 'CBFlashyTabBarController'
  #pod 'QMUIKit'
  pod 'CHTCollectionViewWaterfallLayout'
  pod 'MJRefresh'
  pod 'ATGMediaBrowser'

  # Pods for GankIO-MVVM
  target 'GankIO-MVVMTests' do
    inherit! :search_paths
    pod 'RxTest'
  end

  target 'GankIO-MVVMUITests' do
    inherit! :search_paths
    pod 'RxTest'
  end

end

post_install do |installer|
  # Cocoapods optimization, always clean project after pod updating
  Dir.glob(installer.sandbox.target_support_files_root + "Pods-*/*.sh").each do |script|
    flag_name = File.basename(script, ".sh") + "-Installation-Flag"
    folder = "${TARGET_BUILD_DIR}/${UNLOCALIZED_RESOURCES_FOLDER_PATH}"
    file = File.join(folder, flag_name)
    content = File.read(script)
    content.gsub!(/set -e/, "set -e\nKG_FILE=\"#{file}\"\nif [ -f \"$KG_FILE\" ]; then exit 0; fi\nmkdir -p \"#{folder}\"\ntouch \"$KG_FILE\"")
    File.write(script, content)
  end
  
  # Enable tracing resources
  installer.pods_project.targets.each do |target|
    if target.name == 'RxSwift'
      target.build_configurations.each do |config|
        if config.name == 'Debug'
          config.build_settings['OTHER_SWIFT_FLAGS'] ||= ['-D', 'TRACE_RESOURCES']
        end
      end
    end
  end
end

