## 1、创建私有Repo（Specs）
    在Git上创建一个Respository，并命名为XHProjectMain
    添加Private Pod并验证 
##### 终端依次执行：
    添加私有Repo
    pod repo add XHProjectMain https://github.com/GSmallSea/XHProjectMain.git
    验证是否成功
    pod repo lint .
## 2、创建主工程
    在Git上创建一个Respository，并命名为XHMainProject
    将Respository拉取下来并且通过XCodec创建工程，终端执行
    git clone https://github.com/GSmallSea/XHMainProject.git
##### 终端切到PAToapAPP工程根目录下，初始化你的Podfile，此时不需要在Podfile添加任何依赖
    直接复制一个Podfile文件即可、
    pod install
##### 现在主工程已创建完毕。
## 3、创建组件Pod（创建多个Pod，创建方式相同）
##### 在Git上创建Repository，并拉取到本地
    git clone https://github.com/GSmallSea/XHMainProject-User.git
##### 在XHMainProject-User工程目录下，创建XHMainProject-User工程
##### 并且创建Pod/Classes目录，将XHMainProject-User的Classes/{h,m}拷贝到Pod/Classes目录下面、创建.podspec
    pod spec create XHMainProject-User.podspec  (.podspec 跟项目名一样即可)
## 文件目录变成
    LICENSE
    Pod/Classes/{h,m}
    README.md
    XHMainProject-User
    XHMainProject-User.podspec
## 修改.podspec文件
    spec.name         = "XHMainProject-User"
    spec.version      = "0.0.7"
    spec.summary      = "XHMainProject"
    spec.description  = "XHMainProject第一个" 
    spec.homepage     = "https://github.com/GSmallSea/XHMainProject-User.git"
    spec.license      = { :type => "MIT", :file => "FILE_LICENSE" }
    spec.author             = { "GSmallSea" => "gxiao_hai@163.com" }
    spec.source       = { :git => "https://github.com/GSmallSea/XHMainProject-User.git", :tag => "#{spec.version}" }
    spec.source_files  =  "Pod/Classes", "Pod/Classes/**/*.{h,m}"#(文件目录下面)
    spec.exclude_files = "Classes/Exclude"
    spec.dependency 'MJExtension','~> 3.0'#(spec.dependency 'MJExtension','~> 3.0) 设置要与pod中的设置一样比如版本号
    spec.platform     = :ios, "8.0" #项目中添加其他pod的时候要设置 spec.platform
    spec.dependency 'CTMediator'
    spec.frameworks = 'UIKit'
## 本地验证.podspec是否正确
    pod lib lint
## 提交到Github，并远程验证，按照下列步骤需要首先提交Git，然后添加Tag
     git add .
     git commit -m "添加Pod"
     #添加Tag
     git tag 0.0.1 #这里需要与你的.podspec中s.version值相同
     git push --tags
     #验证
     pod spec lint
###### 下面表示成功
     Analyzed 1 podspec
     PAToapAPP-User.podspec passed validation.
## 添加Pod到你的私有的Repo中(这个别忘记)
     pod repo push XHProjectMain XHMainProject-User.podspec
## 试试搜索你的Pod
    pod search XHMainProject-User
#### 表示成功
    XHMainProject
    pod 'XHMainProject-User', '~> 0.0.7'
    - Homepage: https://github.com/GSmallSea/XHMainProject-User.git
    - Source:   https://github.com/GSmallSea/XHMainProject-User.git
##  现在你可以使用了，请记住在你的Podfile中添加你Private Pod 源
    source 'https://github.com/GSmallSea/XHProjectMain.git'
    source 'https://github.com/CocoaPods/Specs.git'
    platform :ios, '8.0'
    target 'XHMainProject' do
    pod 'XHMainProject-User', '~>0.0.7'
    end
## 当组件化项目完成以后，后续开发中主要的操作(反复一下操作)
    1、工程变更、进入podspec文件修改version版本号及其他pod的导入(dependency)
    2、git add .
    3、git commit -m "添加Pod"
    4、git push
    5、git tag 0.0.1 #这里需要与你的.podspec中s.version值相同
    6、git push --tags
    7、pod spec lint
    8、pod repo push XHProjectMain XHMainProject-User.podspec
    9、查看主项(XHMainProject)目中的.cocoapods目录下去查看工程是否有对应版本信息
    



    
    
