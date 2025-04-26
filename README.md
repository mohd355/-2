# -2
تبي تلعب ؟ تعال ملعبي
QemZone-iOS/
├── QemZone/
│   ├── Models/
│   │   ├── Stadium.swift
│   │   ├── Match.swift
│   │   └── User.swift
│   ├── Services/
│   │   ├── AuthService.swift
│   │   ├── MatchService.swift
│   │   └── FirebaseManager.swift
│   ├── Views/
│   │   ├── Auth/
│   │   │   ├── LoginView.swift
│   │   │   └── RegisterView.swift
│   │   ├── Main/
│   │   │   ├── HomeView.swift
│   │   │   ├── MatchesView.swift
│   │   │   └── ProfileView.swift
│   │   ├── Stadiums/
│   │   │   ├── StadiumListView.swift
│   │   │   ├── StadiumDetailView.swift
│   │   │   └── CreateStadiumView.swift
│   │   └── Components/
│   │       ├── StadiumCard.swift
│   │       └── RatingView.swift
│   ├── ViewModels/
│   │   ├── AuthViewModel.swift
│   │   ├── StadiumViewModel.swift
│   │   └── MatchViewModel.swift
│   └── Utilities/
│       ├── Extensions/
│       │   ├── View+Ext.swift
│       │   └── String+Ext.swift
│       └── Theme/
│           ├── Colors.swift
│           └── Fonts.swift
├── QemZone.xcodeproj
└── README.md
import Firebase

class FirebaseManager {
    static let shared = FirebaseManager()
    
    let auth: Auth
    let firestore: Firestore
    
    private init() {
        FirebaseApp.configure()
        auth = Auth.auth()
        firestore = Firestore.firestore()
    }
}
import SwiftUI
import FirebaseCore

@main
struct QemZoneApp: App {
    @UIApplicationDelegateAdaptor(AppDelegate.self) var delegate
    
    var body: some Scene {
        WindowGroup {
            RootView()
                .environmentObject(AuthViewModel())
        }
    }
}

class AppDelegate: NSObject, UIApplicationDelegate {
    func application(_ application: UIApplication,
                   didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey : Any]? = nil) -> Bool {
        FirebaseManager.shared
        return true
    }
}
# QemZone - iOS App

![QemZone Logo](assets/logo.png)

تطبيق حجز الملاعب الرياضية بلغة SwiftUI مع Firebase

## المميزات
- نظام حجز الملاعب
- إنشاء مباريات ودية
- تقييم اللاعبين
- دفع إلكتروني

## المتطلبات
- iOS 15+
- Xcode 14+
- Swift 5.7+

## التنصيب
1. استنسخ المشروع:
```bash
git clone https://github.com/yourusername/QemZone-iOS.git
cd QemZone-iOS
open QemZone.xcodeproj
// ضع هيكل المجلدات هنا كما بالأعلى
FIREBASE_API_KEY=your_key_here
### 🛠 ملفات الإعداد الإضافية

1. `.gitignore` (للمشاريع iOS)
2. `Project.swift` (للحزم)
```swift
import PackageDescription

let package = Package(
    name: "QemZone",
    platforms: [.iOS(.v15)],
    dependencies: [
        .package(url: "https://github.com/firebase/firebase-ios-sdk.git", from: "10.0.0")
    ],
    targets: [
        .target(
            name: "QemZone",
            dependencies: [
                .product(name: "FirebaseAuth", package: "firebase-ios-sdk"),
                .product(name: "FirebaseFirestore", package: "firebase-ios-sdk")
            ]
        )
    ]
)
