
enum AppStoryboard : String {
    // Please use same storyboard name as the name of cases in enum, Case-sensitive.
    // You can skip raw values as for string type enums, case name is the implicit raw value.
    
    case Main, Profile, Login , Popup , Dashboard, TabBar, VideoPlayer
    
    var instance : UIStoryboard {
      return UIStoryboard(name: self.rawValue, bundle: Bundle.main)
    }
    
    func viewController<T : UIViewController>(viewControllerClass : T.Type, function : String = #function, line : Int = #line, file : String = #file) -> T {
        
        let storyboardID = (viewControllerClass as UIViewController.Type).storyboardID
         
        guard let scene = instance.instantiateViewController(withIdentifier: storyboardID) as? T else {
            fatalError("ViewController with identifier \(storyboardID), not found in \(self.rawValue) Storyboard.\nFile : \(file) \nLine Number : \(line) \nFunction : \(function)")
        }
        
        return scene
    }
    
    func initialViewController() -> UIViewController? {
        return instance.instantiateInitialViewController()
    }
    
}
// https://xd.adobe.com/view/808b4414-9055-4801-bff9-9c477dd8e5b6-d5d8/screen/38243573-bb76-4c7e-b8eb-59286e10621c
//https://gist.github.com/cscouto/fb49c0e8dc48c266ec76ee198c247a07
//https://medium.com/swift-productions/swift-tableview-github-jobs-json-7e35f7b4c13f
//https://www.kodeco.com/10787749-creating-a-custom-calendar-control-for-ios
