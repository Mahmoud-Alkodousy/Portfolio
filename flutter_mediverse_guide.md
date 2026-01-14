# 🚀 MediVerse Advanced Flutter App - Technical Specification

## 📋 وصف المشروع

تطبيق متقدم لمتابعة دور المرضى في المستشفى مع واجهة مستخدم حديثة وتحديثات فورية.

---

## 🎯 متطلبات المشروع

### المميزات الأساسية:
- ✅ تسجيل دخول بالرقم القومي + Biometric (بصمة/وجه)
- ✅ عرض بيانات المريض بشكل جذاب
- ✅ متابعة الدور **لحظياً** مع WebSocket
- ✅ إشعارات ذكية عند اقتراب الدور
- ✅ Dark Mode
- ✅ Glassmorphism UI Design
- ✅ Smooth Animations

### المميزات المتقدمة:
- ✨ Skeleton Loading (مش CircularProgressIndicator عادي)
- ✨ Hero Animations بين الصفحات
- ✨ Pull-to-Refresh مع تأثيرات
- ✨ Haptic Feedback
- ✨ Custom Fonts (Cairo + Poppins)
- ✨ Gradient Buttons مع Scale Animation
- ✨ Wave Progress Indicator
- ✨ Animated Counter للدور

---

## 📂 Project Structure (هيكل المشروع)

```
mediverse_advanced/
├── lib/
│   ├── main.dart
│   │
│   ├── core/
│   │   ├── constants/
│   │   │   ├── app_colors.dart          # كل الألوان + Gradients
│   │   │   ├── app_strings.dart         # كل النصوص
│   │   │   ├── app_dimensions.dart      # Spacing & Sizes
│   │   │   └── api_config.dart          # URLs & Settings
│   │   │
│   │   ├── theme/
│   │   │   └── app_theme.dart           # Light + Dark Theme
│   │   │
│   │   ├── utils/
│   │   │   ├── validators.dart          # التحقق من البيانات
│   │   │   └── helpers.dart             # دوال مساعدة
│   │   │
│   │   └── widgets/                     # Shared Widgets
│   │       ├── gradient_button.dart     # زرار مع Gradient + Animation
│   │       ├── glass_card.dart          # Glassmorphism Card
│   │       ├── skeleton_loader.dart     # Loading Placeholder
│   │       └── animated_counter.dart    # عداد متحرك
│   │
│   ├── models/
│   │   ├── patient.dart                 # بيانات المريض
│   │   └── queue_status.dart            # حالة الدور
│   │
│   ├── services/
│   │   ├── api_service.dart             # REST API Calls
│   │   ├── websocket_service.dart       # Real-time Updates
│   │   ├── notification_service.dart    # Local Notifications
│   │   ├── biometric_service.dart       # Face ID / Fingerprint
│   │   └── storage_service.dart         # SharedPreferences
│   │
│   ├── providers/                       # Riverpod State Management
│   │   ├── auth_provider.dart           # Authentication State
│   │   ├── queue_provider.dart          # Queue State
│   │   └── theme_provider.dart          # Dark Mode State
│   │
│   └── screens/
│       ├── splash_screen.dart           # Splash مع Animation
│       ├── login_screen.dart            # تسجيل الدخول
│       └── home_screen.dart             # الشاشة الرئيسية
│
├── assets/
│   ├── fonts/
│   │   ├── Cairo/                       # خط عربي
│   │   └── Poppins/                     # خط إنجليزي
│   └── images/
│       └── logo.png
│
└── pubspec.yaml
```

---

## 📦 Dependencies (pubspec.yaml)

```yaml
dependencies:
  flutter:
    sdk: flutter

  # State Management
  flutter_riverpod: ^2.4.9

  # Networking
  dio: ^5.4.0
  web_socket_channel: ^2.4.0

  # Local Storage
  shared_preferences: ^2.2.2

  # UI
  flutter_screenutil: ^5.9.0
  shimmer: ^3.0.0
  flutter_animate: ^4.5.0
  
  # Notifications
  flutter_local_notifications: ^16.3.0

  # Biometric
  local_auth: ^2.1.8

  # Utils
  intl: ^0.19.0
  logger: ^2.0.2
```

---

## 🎨 Design System - مهم جداً!

### **قواعد التصميم الإجبارية:**

#### 1. **الألوان (Colors)**
```dart
// Primary Colors
primaryBlue = #2563EB
primaryBlueDark = #1E40AF
accentGreen = #10B981

// Gradients (استخدمها في كل الأزرار)
primaryGradient = [#2563EB → #1E40AF]
successGradient = [#10B981 → #059669]

// Glassmorphism
glassBackground = white.withOpacity(0.15)
glassBorder = white.withOpacity(0.3)
glassBlur = 10px
```

#### 2. **Typography (الخطوط)**
```dart
// استخدم Cairo للعربي
headingLarge = Cairo, 28sp, Bold
headingMedium = Cairo, 20sp, SemiBold
bodyLarge = Cairo, 16sp, Regular
bodySmall = Cairo, 14sp, Regular

// Numbers استخدم Poppins
numbers = Poppins, Bold
```

#### 3. **Spacing (المسافات)**
```dart
// استخدم مضاعفات 8
spacing8 = 8.w
spacing16 = 16.w
spacing24 = 24.w
spacing32 = 32.w

// Border Radius
radiusSmall = 12.r
radiusMedium = 16.r
radiusLarge = 20.r
```

#### 4. **Shadows (الظلال)**
```dart
// استخدم shadows ناعمة
elevation1 = BoxShadow(
  color: black.withOpacity(0.05),
  blurRadius: 8,
  offset: Offset(0, 2),
)

// للأزرار الرئيسية
elevationPrimary = BoxShadow(
  color: primaryBlue.withOpacity(0.3),
  blurRadius: 20,
  offset: Offset(0, 8),
)
```

#### 5. **Animations (الحركات)**
```dart
// Duration
micro = 100ms      // للـ Tap
short = 200ms      // للـ Fade
medium = 300ms     // للـ Slide
long = 600ms       // للـ Complex

// Curves
easeInOut          // للحركات العادية
elasticOut         // للـ Scale
bounceOut          // للأزرار
```

---

## 📱 الشاشات بالتفصيل

### **1. Splash Screen**

**المطلوب:**
- Logo يظهر مع Scale + Fade Animation
- Gradient Background
- مدة 2 ثانية ثم ينتقل للـ Login

**التصميم:**
```
┌─────────────────────────┐
│                         │
│                         │
│       [LOGO 🏥]         │ <- Scale من 0.5 إلى 1.0
│                         │    Fade من 0 إلى 1
│      MediVerse          │ <- Fade بعد Logo
│   نظام متابعة الدور    │
│                         │
│    ●●● Loading          │ <- Animated Dots
│                         │
└─────────────────────────┘
     Gradient BG
```

**الكود:**
```dart
// استخدم AnimatedScale + AnimatedOpacity
// Gradient Background
// Timer(2 seconds) -> Navigator.push(LoginScreen)
```

---

### **2. Login Screen**

**المطلوب:**
- Glass Card للـ Login Form
- Gradient Button
- Biometric Button (بصمة/وجه)
- TextField مع Focus Animation
- Error Handling مع Shake Animation

**التصميم:**
```
┌─────────────────────────────────┐
│                                 │
│     [LOGO]                      │
│     MediVerse                   │
│     نظام متابعة الدور الذكي   │
│                                 │
│  ┌─────────────────────────┐   │
│  │  Glass Card             │   │
│  │                         │   │
│  │  📱 الرقم القومي       │   │
│  │  [______________]       │   │ <- Focus: Border gradient animation
│  │                         │   │
│  │  [تسجيل الدخول 🔐]     │   │ <- Gradient Button + Scale on tap
│  │                         │   │
│  │      ────── أو ──────   │   │
│  │                         │   │
│  │  [👆 البصمة]            │   │ <- Ripple effect on tap
│  │                         │   │
│  └─────────────────────────┘   │
│                                 │
└─────────────────────────────────┘
    Animated Background
    (Gradient + Moving shapes)
```

**المميزات الإجبارية:**
1. **Glass Card**: 
   - Background: white.withOpacity(0.15)
   - Border: white.withOpacity(0.3)
   - Blur: 10
   
2. **TextField**:
   - عند Focus: Border يتحول لـ Gradient
   - Prefix Icon: 📱
   - Validation مع رسالة خطأ تحت الحقل
   
3. **Gradient Button**:
   - عند الضغط: Scale Animation (1.0 → 0.95)
   - Shadow ملونة (primaryBlue.withOpacity(0.3))
   - Loading: CircularProgressIndicator أبيض
   
4. **Biometric Button**:
   - Circle Button
   - Ripple Animation عند الضغط
   - Icon: 👆 أو Face ID icon

**Error Handling:**
```dart
// إذا الرقم القومي خطأ:
// - Shake animation للـ TextField
// - Error message أحمر تحت الحقل
// - Haptic Feedback (vibration)

// إذا المريض مش موجود:
// - Dialog مع animation
// - Icon ❌
```

---

### **3. Home Screen**

**المطلوب:**
- AppBar مع Gradient
- Patient Info Card (Glassmorphism)
- Queue Status Card (متحرك)
- Animated Counter للدور
- Wave Progress Indicator
- Pull to Refresh
- Real-time Updates (WebSocket)

**التصميم:**
```
┌─────────────────────────────────────┐
│ [←]  MediVerse         [🔄] [🌙]   │ <- Gradient AppBar
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │
│  │ Glass Card - Patient Info     │  │
│  │                               │  │
│  │  [👤]  أحمد محمد علي         │  │
│  │        📋 30310031700357      │  │
│  │  ─────────────────────────    │  │
│  │  🩸 فصيلة الدم: O+           │  │
│  │  📅 العمر: 35 سنة            │  │
│  │  📞 الموبايل: 01012345678    │  │
│  │                               │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ Gradient Card - Queue Status  │  │
│  │                               │  │
│  │  حجزك اليوم                  │  │
│  │                               │ │
│  │  د. أحمد السيد               │ │
│  │  🩺 باطنة عامة               │ │
│  │  📍 الدور 2 - أوضة 205       │ │
│  │                               │ │
│  │  ╔═══════════════════════╗    │ │
│  │  ║                       ║    │ │
│  │  ║         3️⃣            ║    │ <- Animated Counter
│  │  ║                       ║    │    (Flip Animation)
│  │  ║      مرضى             ║    │
│  │  ╚═══════════════════════╝    │ │
│  │                               │ │
│  │  ▓▓▓▓▓▓▓░░░ 70%               │ │ <- Wave Progress
│  │  ↑ أنت هنا                   │  │    (Animated)
│  │                               │ │
│  │  ⏱️ الوقت المتوقع: ~15 دقيقة│ │
│  │                               │ │
│  │  آخر تحديث: منذ 5 ثواني     │  │ <- Live Update
│  │                               │ │
│  └───────────────────────────────┘ │
│                                     │
└─────────────────────────────────────┘
```

**المميزات الإجبارية:**

#### **Patient Info Card:**
```dart
// Glass Card مع:
// - Avatar Circle مع Gradient Border
// - Divider بعد الاسم
// - Info Rows مع Icons ملونة
// - Fade In Animation عند الدخول
```

#### **Queue Status Card:**
```dart
// Gradient Card (primaryGradient) مع:
// - White text
// - Doctor Info في Glass Container داخلي
// - Animated Counter (FlipAnimation)
// - Wave Progress (Custom Painter)
// - Pulse animation للـ "آخر تحديث"
```

#### **Animated Counter:**
```dart
// العداد لما يتغير:
// - Flip Animation (زي الساعات الرقمية)
// - Scale pulse
// - Color change إذا قرب الدور (< 3)
```

#### **Wave Progress:**
```dart
// Progress Bar مع:
// - Wave animation (Sine wave)
// - Gradient fill
// - Dots تتحرك مع الموجة
// - "أنت هنا" pointer متحرك
```

#### **Real-time Updates:**
```dart
// WebSocket Connection:
// - عند تغيير الدور: Animated transition
// - عند دورك: Confetti animation
// - Notification + Haptic Feedback
```

**AppBar Actions:**
```dart
// [🔄] Refresh Button:
// - Rotation animation عند الضغط
// - Fetch new data

// [🌙] Dark Mode Toggle:
// - Smooth theme transition
// - Icon يتغير (🌙 / ☀️)
```

**Pull to Refresh:**
```dart
// Custom Refresh Indicator:
// - Logo يدور
// - Gradient spinner
// - Haptic feedback
```

---

## 🔧 Services بالتفصيل

### **1. api_service.dart**

**المطلوب:**
```dart
class ApiService {
  final Dio _dio;
  
  // Constructor مع Interceptors
  ApiService() {
    _dio = Dio(BaseOptions(
      baseUrl: ApiConfig.baseUrl,
      connectTimeout: 30 seconds,
      receiveTimeout: 30 seconds,
    ));
    
    // Add Interceptors:
    // 1. Logging (في Debug mode)
    // 2. Error Handler
    // 3. Retry (3 مرات)
  }
  
  // Methods
  Future<Patient?> login(String nationalId);
  Future<QueueStatus?> getQueueStatus(int patientId);
}
```

**Error Handling:**
```dart
// يجب معالجة:
// - Network Error (لا يوجد إنترنت)
// - Timeout Error
// - Server Error (500)
// - Not Found (404)
// - Unauthorized (401)

// كل error له رسالة مخصصة بالعربي
```

---

### **2. websocket_service.dart**

**المطلوب:**
```dart
class WebSocketService {
  WebSocketChannel? _channel;
  final _controller = StreamController<QueueStatus>.broadcast();
  
  Stream<QueueStatus> get queueStream => _controller.stream;
  
  void connect(int patientId) {
    // Connect to: ws://IP:8004/ws/patient/{patientId}
    // Auto-reconnect عند قطع الاتصال
  }
  
  void disconnect() {
    // Clean up
  }
}
```

**Auto-reconnect:**
```dart
// إذا انقطع الاتصال:
// - انتظر 3 ثواني
// - حاول الاتصال مرة أخرى
// - كرر 5 مرات
// - إذا فشل: اعرض رسالة للمستخدم
```

---

### **3. notification_service.dart**

**المطلوب:**
```dart
class NotificationService {
  Future<void> initialize();
  
  Future<void> showQueueUpdate({
    required int patientsAhead,
    required String doctorName,
    required String location,
  });
  
  Future<void> showYourTurn({
    required String doctorName,
    required String location,
  });
}
```

**Notification Triggers:**
```dart
// إشعار 1: عند 3 مرضى قبلك
// إشعار 2: عند 1 مريض قبلك
// إشعار 3: عند دورك (patientsAhead = 0)
```

---

### **4. biometric_service.dart**

**المطلوب:**
```dart
class BiometricService {
  Future<bool> isBiometricAvailable();
  Future<bool> authenticate();
  Future<void> saveCredentials(String nationalId);
  Future<String?> getSavedCredentials();
}
```

**Flow:**
```dart
// 1. عند Login أول مرة:
//    - اسأل المستخدم: "حفظ البصمة؟"
//    - إذا نعم: احفظ الرقم القومي في SecureStorage
//
// 2. عند فتح التطبيق:
//    - إذا يوجد رقم محفوظ: اعرض زر البصمة
//    - عند الضغط: Biometric Authentication
//    - إذا نجح: Login تلقائي
```

---

### **5. storage_service.dart**

**المطلوب:**
```dart
class StorageService {
  Future<void> saveLastLogin(String nationalId);
  Future<String?> getLastLogin();
  
  Future<void> saveDarkMode(bool isDark);
  Future<bool> getDarkMode();
  
  Future<void> clear();
}
```

---

## 🎭 Providers (Riverpod)

### **auth_provider.dart**

```dart
@riverpod
class AuthNotifier extends _$AuthNotifier {
  @override
  AsyncValue<Patient?> build() {
    // Check saved credentials
    return const AsyncValue.loading();
  }
  
  Future<void> login(String nationalId) async {
    state = const AsyncValue.loading();
    
    try {
      final patient = await ApiService().login(nationalId);
      if (patient != null) {
        state = AsyncValue.data(patient);
        await StorageService().saveLastLogin(nationalId);
      } else {
        state = AsyncValue.error('المريض غير موجود');
      }
    } catch (e) {
      state = AsyncValue.error(e.toString());
    }
  }
  
  Future<void> biometricLogin() async {
    // ... Biometric flow
  }
  
  void logout() {
    state = const AsyncValue.data(null);
    StorageService().clear();
  }
}
```

---

### **queue_provider.dart**

```dart
@riverpod
class QueueNotifier extends _$QueueNotifier {
  Timer? _refreshTimer;
  WebSocketService? _wsService;
  
  @override
  AsyncValue<QueueStatus?> build(int patientId) {
    _initWebSocket(patientId);
    return const AsyncValue.loading();
  }
  
  void _initWebSocket(int patientId) {
    _wsService = WebSocketService();
    _wsService!.connect(patientId);
    
    _wsService!.queueStream.listen((status) {
      state = AsyncValue.data(status);
      _checkNotifications(status);
    });
  }
  
  Future<void> refresh() async {
    try {
      final status = await ApiService().getQueueStatus(patientId);
      state = AsyncValue.data(status);
    } catch (e) {
      // Keep old data, show error toast
    }
  }
  
  void _checkNotifications(QueueStatus status) {
    if (status.patientsAhead == 1) {
      NotificationService().showQueueUpdate(...);
    } else if (status.patientsAhead == 0) {
      NotificationService().showYourTurn(...);
      // Confetti animation
    }
  }
  
  @override
  void dispose() {
    _refreshTimer?.cancel();
    _wsService?.disconnect();
    super.dispose();
  }
}
```

---

## 🎨 Core Widgets بالتفصيل

### **gradient_button.dart**

```dart
class GradientButton extends StatefulWidget {
  final String text;
  final VoidCallback? onPressed;
  final bool isLoading;
  final IconData? icon;
  final Gradient? gradient;
  
  // المطلوب:
  // 1. Container مع Gradient Background
  // 2. Scale Animation عند الضغط (1.0 → 0.95)
  // 3. Shadow ملونة
  // 4. Loading: CircularProgressIndicator أبيض
  // 5. Haptic Feedback عند الضغط
}
```

---

### **glass_card.dart**

```dart
class GlassCard extends StatelessWidget {
  final Widget child;
  final double blur;
  final double opacity;
  
  @override
  Widget build(BuildContext context) {
    return ClipRRect(
      borderRadius: BorderRadius.circular(20),
      child: BackdropFilter(
        filter: ImageFilter.blur(sigmaX: blur, sigmaY: blur),
        child: Container(
          decoration: BoxDecoration(
            color: Colors.white.withOpacity(opacity),
            borderRadius: BorderRadius.circular(20),
            border: Border.all(
              color: Colors.white.withOpacity(0.3),
              width: 1.5,
            ),
          ),
          child: child,
        ),
      ),
    );
  }
}
```

---

### **skeleton_loader.dart**

```dart
class SkeletonLoader extends StatefulWidget {
  final double width;
  final double height;
  final BorderRadius? borderRadius;
  
  // المطلوب:
  // 1. Container مع shimmer animation
  // 2. Opacity يتغير (0.3 ↔ 0.7)
  // 3. Duration: 1 second
  // 4. Repeat: infinite
}

// استخدمه بدل CircularProgressIndicator
// مثال:
// - Patient Card Skeleton
// - Queue Card Skeleton
```

---

### **animated_counter.dart**

```dart
class AnimatedCounter extends StatefulWidget {
  final int value;
  final TextStyle? textStyle;
  
  // المطلوب:
  // 1. عند تغيير القيمة: Flip Animation
  // 2. Scale pulse
  // 3. Color change إذا value < 3 (أحمر)
  
  // Animation:
  // - Old value يطلع لفوق (slide + fade)
  // - New value يدخل من تحت (slide + fade)
  // - Duration: 400ms
}
```

---

### **wave_progress.dart**

```dart
class WaveProgress extends StatefulWidget {
  final double progress; // 0.0 to 1.0
  final double height;
  
  // المطلوب:
  // 1. CustomPainter لرسم الموجة
  // 2. Sine wave animation
  // 3. Gradient fill
  // 4. "أنت هنا" pointer
  
  // Math:
  // y = sin(x + offset) * amplitude
  // offset يزيد مع الوقت (animation)
}
```

---

## 📋 Testing Checklist

قبل التسليم، تأكد من:

### **Functionality:**
- [ ] Login بالرقم القومي يعمل
- [ ] Login بالبصمة يعمل (إذا متوفر)
- [ ] عرض بيانات المريض صحيح
- [ ] WebSocket يتصل ويستقبل Updates
- [ ] الإشعارات تظهر عند اقتراب الدور
- [ ] Dark Mode يعمل
- [ ] Pull to Refresh يعمل

### **UI/UX:**
- [ ] كل الـ Animations smooth (60 FPS)
- [ ] Glassmorphism واضح وجميل
- [ ] الألوان متناسقة
- [ ] Spacing منتظم (مضاعفات 8)
- [ ] Shadows ناعمة
- [ ] الخط واضح وسهل القراءة
- [ ] Loading States موجودة (Skeleton)
- [ ] Error Messages واضحة

### **Performance:**
- [ ] لا يوجد Memory Leaks
- [ ] dispose() للـ Controllers
- [ ] WebSocket ينفصل عند الخروج
- [ ] Images محسّنة

### **Code Quality:**
- [ ] الكود منظم ونظيف
- [ ] Comments واضحة
- [ ] No hardcoded values
- [ ] Error Handling موجود

---

## 🔌 API Documentation

### **Base URL**
```
Development: http://192.168.1.100:8004
Production: https://api.mediverse.com
```

---

### **1. Login API**

**Endpoint:**
```
GET /check-national-id/{national_id}
```

**Example Request:**
```
GET /check-national-id/30310031700357
```

**Success Response (200):**
```json
{
  "exists": true,
  "patient": {
    "id": 1,
    "full_name": "أحمد محمد علي السيد",
    "national_id": "30310031700357",
    "gender": "Male",
    "age": 35,
    "blood_type": "O+",
    "phone_number": "01012345678",
    "chronic_diseases": "السكري|ضغط الدم",
    "allergies": "البنسلين",
    "current_medications": "الأنسولين|أملوديبين",
    "created_at": "2024-01-15T10:30:00Z",
    "updated_at": "2024-01-15T10:30:00Z"
  }
}
```

**Error Response (404):**
```json
{
  "exists": false,
  "message": "المريض غير موجود في النظام"
}
```

**Error Handling:**
- 404: "المريض غير موجود"
- 500: "خطأ في السيرفر، حاول مرة أخرى"
- Timeout: "انتهت مهلة الاتصال"
- Network: "تحقق من اتصال الإنترنت"

---

### **2. Get Queue Status API**

**Endpoint:**
```
GET /queue/status/{patient_id}
```

**Example Request:**
```
GET /queue/status/1
```

**Success Response (200):**
```json
{
  "queue_id": 15,
  "doctor_id": 3,
  "doctor_name": "د. أحمد السيد",
  "specialty": "Internal Medicine",
  "specialty_ar": "باطنة عامة",
  "position": 4,
  "status": "waiting",
  "estimated_wait_minutes": 15,
  "patients_ahead": 3,
  "join_time": "2024-01-15T09:00:00Z",
  "floor_number": "2",
  "room_number": "205"
}
```

**No Queue Response (404):**
```json
{
  "message": "لا يوجد حجز حالياً"
}
```

**Status Values:**
- `waiting`: في الانتظار
- `called`: تم استدعاؤك
- `in_consultation`: في الكشف
- `completed`: انتهى الكشف
- `cancelled`: ملغي

---

### **3. WebSocket Real-time Updates**

**Endpoint:**
```
WS /ws/patient/{patient_id}
```

**Example Connection:**
```dart
final channel = WebSocketChannel.connect(
  Uri.parse('ws://192.168.1.100:8004/ws/patient/1'),
);

channel.stream.listen((message) {
  final data = jsonDecode(message);
  // Handle queue update
  final queueStatus = QueueStatus.fromJson(data);
  // Update UI
});
```

**Message Format:**
```json
{
  "type": "queue_update",
  "queue_id": 15,
  "doctor_id": 3,
  "doctor_name": "د. أحمد السيد",
  "specialty": "Internal Medicine",
  "specialty_ar": "باطنة عامة",
  "position": 3,
  "status": "waiting",
  "estimated_wait_minutes": 10,
  "patients_ahead": 2,
  "join_time": "2024-01-15T09:00:00Z",
  "floor_number": "2",
  "room_number": "205"
}
```

**WebSocket Events:**
- `queue_update`: تحديث حالة الدور
- `your_turn`: دورك الآن
- `cancelled`: تم إلغاء الموعد
- `doctor_delayed`: تأخير من الطبيب

**Auto-Reconnect Logic:**
```dart
// عند قطع الاتصال:
// 1. Wait 3 seconds
// 2. Attempt reconnect
// 3. Retry max 5 times
// 4. Show error if all attempts fail
```

---

## 🎨 Animation Specifications

### **1. Splash Screen Animation**

```dart
Timeline:
0ms   → Logo Scale: 0.5, Opacity: 0
200ms → Logo Scale: 1.0, Opacity: 1.0 (Curve: elasticOut)
600ms → Text Fade In (Curve: easeIn)
1000ms→ Loading Dots Start
2000ms→ Navigate to Login
```

---

### **2. Login Screen Animations**

**TextField Focus Animation:**
```dart
// عند Focus:
// 1. Border color: grey → gradient (300ms)
// 2. Border width: 1 → 2 (300ms)
// 3. Scale: 1.0 → 1.02 (200ms, subtle)
```

**Button Press Animation:**
```dart
// عند الضغط:
// 1. Scale: 1.0 → 0.95 (100ms)
// 2. Haptic feedback (medium)
// عند الإفلات:
// 1. Scale: 0.95 → 1.0 (100ms)
```

**Error Shake Animation:**
```dart
// عند خطأ:
// 1. Shake TextField: -5, 5, -5, 5, 0 (400ms)
// 2. Error text fade in (200ms)
// 3. Haptic feedback (error)
```

**Biometric Button:**
```dart
// عند الضغط:
// 1. Ripple effect (400ms)
// 2. Scale pulse: 1.0 → 1.1 → 1.0 (600ms)
// 3. Rotate icon: 0 → 360 (800ms)
```

---

### **3. Home Screen Animations**

**Page Enter Animation:**
```dart
// عند الدخول:
// 1. AppBar slide from top (300ms, delay: 0ms)
// 2. Patient Card fade + slide up (400ms, delay: 100ms)
// 3. Queue Card fade + slide up (400ms, delay: 200ms)
```

**Counter Flip Animation:**
```dart
// عند تغيير الرقم:
// Old Number:
// - Slide up + fade out (300ms)
// New Number:
// - Slide from bottom + fade in (300ms)
// - Scale pulse: 1.0 → 1.2 → 1.0 (400ms)

// Color Change:
// - If value < 3: Color gradient to red (500ms)
```

**Wave Progress Animation:**
```dart
// Continuous:
// - Sine wave offset increases
// - Speed: complete cycle every 2 seconds
// - Amplitude: 5px
// - Frequency: 2 waves

// Formula:
// y = sin((x + offset) * frequency) * amplitude
// offset += 0.05 (per frame)
```

**Pull to Refresh:**
```dart
// Pull:
// - Logo rotates (0 → 360)
// - Progress circle grows
// Release:
// - Spinner animation (gradient)
// - Haptic feedback
```

**Real-time Update Animation:**
```dart
// عند استقبال update من WebSocket:
// 1. Pulse effect على الـ Card (200ms)
// 2. Counter flip animation
// 3. Progress bar animate to new value (500ms)
// 4. "آخر تحديث" fade + color change (300ms)
```

**Your Turn Celebration:**
```dart
// عند دورك (patients_ahead = 0):
// 1. Confetti animation (2 seconds)
// 2. Success gradient على Card (500ms)
// 3. Vibration pattern (long)
// 4. Notification sound
```

---

## 📱 Responsive Design Rules

### **Phone (< 600dp):**
```dart
- Single column layout
- Card padding: 16
- Font sizes: as specified
- Bottom sheet for details
```

### **Tablet (≥ 600dp):**
```dart
- Two column layout (Patient Info | Queue Status)
- Card padding: 24
- Font sizes: +2sp
- Dialogs instead of bottom sheets
- Max width: 1200
```

---

## 🌙 Dark Mode Specifications

### **Colors in Dark Mode:**
```dart
Background: #0F172A (darkBackground)
Surface: #1E293B (darkSurface)
Card: #1E293B with slight elevation
Text Primary: #F8FAFC
Text Secondary: #CBD5E1

// Glassmorphism in Dark Mode:
glassBackground = white.withOpacity(0.05)
glassBorder = white.withOpacity(0.1)

// Keep gradients the same
primaryGradient = same
successGradient = same
```

### **Theme Toggle Animation:**
```dart
// عند تغيير Theme:
// 1. Circular reveal animation (600ms)
// 2. Colors crossfade (400ms)
// 3. Icons flip (300ms)
// 4. Save preference to storage
```

---

## 🔔 Notification System

### **Local Notifications:**

**Notification 1: "دورك قريب"**
```dart
Trigger: patientsAhead == 3
Title: 🔔 دورك قريب!
Body: باقي 3 مرضى قبلك
      استعد للذهاب إلى د. [اسم الطبيب]
      📍 [المكان]
Sound: default
Vibration: medium
```

**Notification 2: "مريض واحد قبلك"**
```dart
Trigger: patientsAhead == 1
Title: ⚠️ مريض واحد قبلك!
Body: استعد فوراً
      د. [اسم الطبيب]
      📍 [المكان]
Sound: default
Vibration: long
Priority: HIGH
```

**Notification 3: "حان دورك"**
```dart
Trigger: patientsAhead == 0
Title: 🎉 حان دورك!
Body: توجه فوراً إلى:
      د. [اسم الطبيب]
      📍 الدور [X] - أوضة [X]
Sound: urgent
Vibration: pattern [0, 200, 100, 200]
Priority: MAX
Heads-up: true
```

---

## 🎯 Performance Optimization

### **1. Image Optimization:**
```dart
// استخدم cached_network_image للصور
// Logo: compress to < 50KB
// Splash screen: preload
```

### **2. List Performance:**
```dart
// استخدم ListView.builder
// Lazy loading for long lists
```

### **3. Memory Management:**
```dart
// Dispose controllers:
// - AnimationController
// - TextEditingController
// - ScrollController
// - StreamController

// Cancel timers in dispose()
// Close WebSocket in dispose()
```

### **4. Network Optimization:**
```dart
// Cache API responses (5 minutes)
// Debounce refresh (prevent spam)
// Use WebSocket for updates (not polling)
```

---

## 🧪 Testing Scenarios

### **Manual Testing:**

**Scenario 1: First Login**
```
1. Open app → Splash screen appears
2. Enter valid national ID
3. Press login → Loading shows
4. Success → Navigate to Home
5. Biometric prompt appears
6. Accept → Credentials saved
```

**Scenario 2: Biometric Login**
```
1. Open app → Splash screen
2. Biometric button visible
3. Press → Fingerprint/Face ID
4. Success → Auto login
5. Navigate to Home
```

**Scenario 3: No Internet**
```
1. Disconnect WiFi
2. Try login → Error message
3. Message: "تحقق من اتصال الإنترنت"
4. Retry button appears
```

**Scenario 4: Real-time Updates**
```
1. Login successfully
2. View queue status
3. Simulate update from backend
4. Counter updates with animation
5. Progress bar updates
6. "آخر تحديث" shows current time
```

**Scenario 5: Your Turn**
```
1. Backend sends: patients_ahead = 0
2. Notification appears
3. Confetti animation plays
4. Card changes to success gradient
5. Vibration pattern triggers
```

**Scenario 6: Dark Mode**
```
1. Press dark mode toggle
2. Circular reveal animation
3. Colors transition smoothly
4. Preference saved
5. Reopen app → Dark mode persists
```

---

## 📝 Code Organization Best Practices

### **File Naming:**
```
Screens: login_screen.dart
Widgets: gradient_button.dart
Services: api_service.dart
Models: patient.dart (not patient_model.dart)
Providers: auth_provider.dart
```

### **Class Naming:**
```dart
Screens: LoginScreen extends StatefulWidget
Widgets: GradientButton extends StatelessWidget
Services: class ApiService
Models: class Patient
Providers: class AuthNotifier extends Notifier
```

### **Variable Naming:**
```dart
// Descriptive names
final patientName = "أحمد";  ✅
final n = "أحمد";  ❌

// Boolean: use is/has/can
final isLoading = true;  ✅
final loading = true;  ❌

// Collections: plural
final patients = [];  ✅
final patient = [];  ❌
```

### **Comments:**
```dart
// العربي للتوضيح
// English for code documentation

/// API call to get patient data
/// 
/// Parameters:
/// - [nationalId]: 14-digit national ID
/// 
/// Returns:
/// - Patient object if found
/// - null if not found
/// 
/// Throws:
/// - NetworkException on connection error
/// - ServerException on server error
Future<Patient?> getPatient(String nationalId) async {
  // تحقق من صحة الرقم القومي
  if (!_isValidNationalId(nationalId)) {
    throw ValidationException('رقم قومي غير صحيح');
  }
  
  // ... rest of code
}
```

---

## 🚨 Common Pitfalls to Avoid

### **❌ DON'T:**

1. **استخدام setState في كل مكان**
```dart
// ❌ Bad
setState(() {
  _counter++;
  _name = "Ahmed";
  _isLoading = false;
});

// ✅ Good - Use Riverpod
ref.read(counterProvider.notifier).increment();
```

2. **نسيان dispose**
```dart
// ❌ Bad
class _MyScreenState extends State<MyScreen> {
  final _controller = AnimationController(...);
  // No dispose!
}

// ✅ Good
@override
void dispose() {
  _controller.dispose();
  super.dispose();
}
```

3. **Hardcoded values**
```dart
// ❌ Bad
Container(
  padding: EdgeInsets.all(16),
  // ...
)

// ✅ Good
Container(
  padding: EdgeInsets.all(AppDimensions.spacing16),
  // ...
)
```

4. **Nested ternary operators**
```dart
// ❌ Bad
final color = isError ? Colors.red : isWarning ? Colors.orange : Colors.green;

// ✅ Good
Color getStatusColor() {
  if (isError) return Colors.red;
  if (isWarning) return Colors.orange;
  return Colors.green;
}
```

5. **عدم معالجة الأخطاء**
```dart
// ❌ Bad
final data = await api.getData();

// ✅ Good
try {
  final data = await api.getData();
  // Handle success
} on NetworkException {
  // Handle network error
} on ServerException {
  // Handle server error
} catch (e) {
  // Handle unknown error
}
```

---

## 🎓 Learning Resources

### **Flutter:**
- [Flutter Official Docs](https://docs.flutter.dev/)
- [Flutter Animations](https://docs.flutter.dev/development/ui/animations)
- [Flutter Performance](https://docs.flutter.dev/perf)

### **Riverpod:**
- [Riverpod Docs](https://riverpod.dev/)
- [Riverpod Examples](https://github.com/rrousselGit/riverpod/tree/master/examples)

### **Design:**
- [Material Design 3](https://m3.material.io/)
- [Glassmorphism Guide](https://uxdesign.cc/glassmorphism-in-user-interfaces-1f39bb1308c9)
- [Flutter UI Challenges](https://github.com/lohanidamodar/flutter_ui_challenges)

### **WebSocket:**
- [web_socket_channel Package](https://pub.dev/packages/web_socket_channel)
- [WebSocket Best Practices](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)

---

## 🎬 Implementation Order

### **Week 1: Foundation**
1. ✅ Setup project + dependencies
2. ✅ Create folder structure
3. ✅ Setup constants (colors, dimensions, strings)
4. ✅ Create theme configuration
5. ✅ Build core widgets (button, card, loader)

### **Week 2: Data Layer**
1. ✅ Create models (Patient, QueueStatus)
2. ✅ Setup ApiService with Dio
3. ✅ Setup WebSocketService
4. ✅ Setup NotificationService
5. ✅ Setup StorageService
6. ✅ Test all services

### **Week 3: UI Screens**
1. ✅ Build Splash Screen
2. ✅ Build Login Screen (UI only)
3. ✅ Build Home Screen (UI only)
4. ✅ Add animations to all screens
5. ✅ Implement dark mode

### **Week 4: Integration**
1. ✅ Setup Riverpod providers
2. ✅ Connect Login to API
3. ✅ Connect Home to API
4. ✅ Implement WebSocket updates
5. ✅ Add biometric authentication
6. ✅ Test everything

### **Week 5: Polish**
1. ✅ Fix bugs
2. ✅ Optimize performance
3. ✅ Add error handling
4. ✅ Test on real device
5. ✅ Final testing

---

## 📦 Deliverables

### **Must Have:**
1. ✅ Working app (Android APK)
2. ✅ Source code (organized)
3. ✅ README.md with:
   - Setup instructions
   - Screenshots
   - Features list
   - Known issues

### **Nice to Have:**
1. ✨ Demo video
2. ✨ Unit tests
3. ✨ Widget tests
4. ✨ Performance report

---

## 🔧 Environment Setup

### **Android Configuration:**

**`android/app/build.gradle`:**
```gradle
android {
    compileSdkVersion 34
    
    defaultConfig {
        applicationId "com.mediverse.advanced"
        minSdkVersion 24  // For biometric
        targetSdkVersion 34
        versionCode 1
        versionName "2.0.0"
    }
    
    buildTypes {
        release {
            signingConfig signingConfigs.debug
            minifyEnabled true
            shrinkResources true
        }
    }
}
```

**`android/app/src/main/AndroidManifest.xml`:**
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    
    <!-- Permissions -->
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.VIBRATE"/>
    <uses-permission android:name="android.permission.POST_NOTIFICATIONS"/>
    <uses-permission android:name="android.permission.USE_BIOMETRIC"/>
    <uses-permission android:name="android.permission.USE_FINGERPRINT"/>
    
    <application
        android:label="MediVerse"
        android:name="${applicationName}"
        android:icon="@mipmap/ic_launcher"
        android:usesCleartextTraffic="true">
        
        <!-- ... -->
        
    </application>
</manifest>
```

---

## 🎯 Success Criteria

### **The app is considered ADVANCED if:**

✅ **UI/UX:**
- Glassmorphism effects are clearly visible
- All animations are smooth (60 FPS)
- Dark mode looks professional
- No static/boring design elements
- Every interaction has micro-feedback

✅ **Functionality:**
- WebSocket updates work in real-time
- Biometric login works flawlessly
- Notifications appear at correct times
- No crashes or freezes
- Error handling is graceful

✅ **Code Quality:**
- Clean Architecture implemented
- Riverpod used correctly
- No memory leaks
- Proper error handling
- Code is organized and readable

✅ **Performance:**
- App starts in < 2 seconds
- Animations don't lag
- Memory usage is reasonable
- Battery drain is minimal

---

## 🚀 Deployment Checklist

### **Before Release:**

**Code:**
- [ ] Remove all debug prints
- [ ] Remove unused imports
- [ ] Format all files (dart format .)
- [ ] Run flutter analyze (0 issues)
- [ ] Fix all warnings

**Testing:**
- [ ] Test on real Android device
- [ ] Test on different screen sizes
- [ ] Test in poor network conditions
- [ ] Test dark mode thoroughly
- [ ] Test biometric on multiple devices

**Assets:**
- [ ] Optimize all images
- [ ] Add app icon
- [ ] Add splash screen
- [ ] Check all fonts are included

**Build:**
- [ ] Update version number
- [ ] Build release APK
- [ ] Test release APK
- [ ] Check APK size (< 50MB)

---

## 💡 Tips for Success

### **For the AI Model:**

1. **READ THE WHOLE SPEC** before starting to code
2. **Follow the design system** exactly - don't improvise colors/spacing
3. **Implement animations** - they're not optional
4. **Test incrementally** - don't build everything then test
5. **Handle errors gracefully** - assume network will fail
6. **Optimize early** - dispose controllers, cancel timers
7. **Comment your code** - especially complex animations
8. **Use provided widgets** - don't reinvent the wheel
9. **Follow the structure** - don't reorganize folders
10. **Make it beautiful** - this is an ADVANCED app!

---

## 📞 Support & Questions

If you encounter issues:

1. **Read error messages carefully**
2. **Check API responses** in the debug console
3. **Test on real device** if emulator doesn't work
4. **Verify network connectivity**
5. **Check API endpoints** are correct
6. **Review this spec again**

---

## 🎊 Final Notes

This specification is designed to produce a **PROFESSIONAL, ADVANCED** Flutter app that stands out. 

### **Remember:**
- 🎨 **Design matters** - users judge apps by appearance
- ⚡ **Performance matters** - smooth = professional
- 🔧 **Code quality matters** - for maintenance
- 📱 **User experience matters** - make it delightful

### **The Goal:**
Build an app that makes people say **"WOW, this is amazing!"** when they see it.

---

**Good luck! You got this! 🚀💙**

---

*MediVerse Advanced - Technical Specification v2.0*  
*Last Updated: January 2026*  
*For AI Model Implementation*