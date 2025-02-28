# FlutterQuestions2025

  <h1>Flutter Interview Questions & Answers</h1>
    
  <h2>1. What is Flutter?</h2>
  <p>Flutter is an open-source UI toolkit developed by Google for building natively compiled applications for mobile, web, and desktop from a single codebase.</p>

<h2>2. SOLID Principles in Flutter</h2>

<h3>1. Single Responsibility Principle (SRP)</h3>
<p>A class should have only one reason to change.</p>
<pre>
class UserRepository {
  Future<String> fetchUserName() async {
    return "John Doe";
  }
}
</pre>

<h3>2. Open/Closed Principle (OCP)</h3>
<p>A class should be open for extension but closed for modification.</p>
<pre>
abstract class PaymentMethod {
  void pay(double amount);
}

class CreditCardPayment implements PaymentMethod {
  @override
  void pay(double amount) {
    print("Paid $amount using Credit Card");
  }
}
</pre>

<h3>3. Liskov Substitution Principle (LSP)</h3>
<p>Derived classes must be substitutable for their base classes.</p>
<pre>
abstract class Bird {}

abstract class FlyingBird extends Bird {
  void fly();
}

class Sparrow extends FlyingBird {
  @override
  void fly() => print("Sparrow is flying");
}
</pre>

<h3>4. Interface Segregation Principle (ISP)</h3>
<p>A class should not be forced to implement methods it does not use.</p>
<pre>
abstract class Workable {
  void work();
}

abstract class Eatable {
  void eat();
}

class Robot implements Workable {
  @override
  void work() => print("Robot working");
}
</pre>

<h3>5. Dependency Inversion Principle (DIP)</h3>
<p>High-level modules should not depend on low-level modules. Both should depend on abstractions.</p>
<pre>
abstract class DatabaseService {
  void save(String data);
}

class FirebaseService implements DatabaseService {
  @override
  void save(String data) {
    print("Saving data to Firebase: $data");
  }
}
</pre>

<h3>Summary Table</h3>
<table border="1">
  <tr>
    <th>SOLID Principle</th>
    <th>Flutter Example</th>
  </tr>
  <tr>
    <td>Single Responsibility</td>
    <td>Separate UI, business logic, and data fetching</td>
  </tr>
  <tr>
    <td>Open/Closed</td>
    <td>Use abstract classes or interfaces for extensibility</td>
  </tr>
  <tr>
    <td>Liskov Substitution</td>
    <td>Ensure child classes can replace parent classes without breaking behavior</td>
  </tr>
  <tr>
    <td>Interface Segregation</td>
    <td>Use small, specific interfaces instead of large ones</td>
  </tr>
  <tr>
    <td>Dependency Inversion</td>
    <td>Inject dependencies via constructors instead of hardcoding</td>
  </tr>
</table>


<h2>Stateful Lifecycle Methods in Flutter</h2>

<h3>Key Stateful Lifecycle Methods</h3>

<h4>initState()</h4>
<p>Called once when the widget is inserted into the widget tree.</p>
<p>Used for one-time initializations, such as setting up controllers or fetching data.</p>

<pre>
@override
void initState() {
  super.initState();
  print("Widget Initialized");
}
</pre>

<h4>didChangeDependencies()</h4>
<p>Called when an inherited widget (like Provider, InheritedWidget) the widget depends on changes.</p>
<p>Called after initState().</p>
<p>Useful when fetching data that depends on inherited widgets.</p>

<pre>
@override
void didChangeDependencies() {
  super.didChangeDependencies();
  print("Dependencies Changed");
}
</pre>

<h4>build(BuildContext context)</h4>
<p>Called every time the widget needs to be rebuilt.</p>
<p>Should be pure (avoid side effects).</p>

<pre>
@override
Widget build(BuildContext context) {
  return Text("Hello, Flutter!");
}
</pre>

<h4>setState(fn)</h4>
<p>Triggers a rebuild of the widget when the internal state changes.</p>

<pre>
void incrementCounter() {
  setState(() {
    counter++;
  });
}
</pre>

<h4>didUpdateWidget(covariant T oldWidget)</h4>
<p>Called when the parent widget updates and needs to rebuild the State object.</p>
<p>Useful when reconfiguring based on widget properties.</p>

<pre>
@override
void didUpdateWidget(covariant MyWidget oldWidget) {
  super.didUpdateWidget(oldWidget);
  print("Widget Updated");
}
</pre>

<h4>deactivate()</h4>
<p>Called when the widget is removed from the widget tree.</p>
<p>Might be reinserted later.</p>

<pre>
@override
void deactivate() {
  super.deactivate();
  print("Widget Deactivated");
}
</pre>

<h4>dispose()</h4>
<p>Called when the widget is permanently removed.</p>
<p>Used to release resources (e.g., controllers, streams, animations).</p>

<pre>
@override
void dispose() {
  myController.dispose();
  super.dispose();
  print("Widget Disposed");
}
</pre>

<h3>Lifecycle Flow</h3>

<pre>
initState() → didChangeDependencies() → build()
→ (State Changes) → setState() → build()
→ didUpdateWidget() → build()
→ deactivate() → dispose()
</pre>

<h3>Use Case Example</h3>

<pre>
class MyStatefulWidget extends StatefulWidget {
  @override
  _MyStatefulWidgetState createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  int counter = 0;

  @override
  void initState() {
    super.initState();
    print("initState: Widget Initialized");
  }

  @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    print("didChangeDependencies: Dependencies Changed");
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text("Counter: $counter"),
        ElevatedButton(
          onPressed: () => setState(() => counter++),
          child: Text("Increment"),
        ),
      ],
    );
  }

  @override
  void didUpdateWidget(covariant MyStatefulWidget oldWidget) {
    super.didUpdateWidget(oldWidget);
    print("didUpdateWidget: Widget Updated");
  }

  @override
  void deactivate() {
    super.deactivate();
    print("deactivate: Widget Removed");
  }

  @override
  void dispose() {
    super.dispose();
    print("dispose: Widget Destroyed");
  }
}
</pre>

<div>
  <h3>1️⃣ Using setState() (For Local Widget State)</h3>
  <p>If you want to update a widget inside its own <code>StatefulWidget</code>, use <code>setState()</code>:</p>
  <pre>
    <code>
class CounterWidget extends StatefulWidget {
  @override
  _CounterWidgetState createState() => _CounterWidgetState();
}

class _CounterWidgetState extends State&lt;CounterWidget&gt; {
  int counter = 0;

  void incrementCounter() {
    setState(() {
      counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text("Counter: $counter"),
        ElevatedButton(
          onPressed: incrementCounter,
          child: Text("Increment"),
        ),
      ],
    );
  }
}
    </code>
  </pre>
  <p>✅ Best for: Self-contained widgets that manage their own state.</p>
</div>

<div>
  <h3>2️⃣ Using Callbacks (For Parent-Child Communication)</h3>
  <p>If a parent widget wants to change a child widget's state, you can pass a function (callback) to the child.</p>
  <pre>
    <code>
class ParentWidget extends StatefulWidget {
  @override
  _ParentWidgetState createState() => _ParentWidgetState();
}

class _ParentWidgetState extends State&lt;ParentWidget&gt; {
  int counter = 0;

  void incrementCounter() {
    setState(() {
      counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text("Parent Counter: $counter"),
        ChildWidget(onPressed: incrementCounter),
      ],
    );
  }
}

class ChildWidget extends StatelessWidget {
  final VoidCallback onPressed;

  ChildWidget({required this.onPressed});

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: onPressed,
      child: Text("Increment Parent Counter"),
    );
  }
}
    </code>
  </pre>
  <p>✅ Best for: When a parent needs to change a child’s state.</p>
</div>

<div>
  <h3>3️⃣ Using GlobalKey (For Changing State from Outside)</h3>
  <p>If you need to update a specific widget from anywhere in the widget tree, use a <code>GlobalKey</code>.</p>
  <pre>
    <code>
class _CounterWidgetState extends State&lt;CounterWidget&gt; {
  int counter = 0;

  void incrementCounter() {
    setState(() {
      counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Text("Counter: $counter");
  }
}

class ParentWidget extends StatelessWidget {
  final GlobalKey&lt;_CounterWidgetState&gt; counterKey = GlobalKey();

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        CounterWidget(key: counterKey),
        ElevatedButton(
          onPressed: () => counterKey.currentState?.incrementCounter(),
          child: Text("Increment"),
        ),
      ],
    );
  }
}
    </code>
  </pre>
  <p>✅ Best for: When you need to change a widget's state from outside its build context.</p>
</div>

<div>
  <h3>4️⃣ Using State Management (Provider, Riverpod, Bloc, GetX)</h3>
  <p>For complex apps, use state management solutions like <strong>Provider, Riverpod, GetX, or Bloc</strong>.</p>
  <pre>
    <code>
class CounterProvider with ChangeNotifier {
  int counter = 0;

  void increment() {
    counter++;
    notifyListeners();
  }
}

void main() {
  runApp(ChangeNotifierProvider(
    create: (_) => CounterProvider(),
    child: MyApp(),
  ));
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Column(
          children: [
            Consumer&lt;CounterProvider&gt;(
              builder: (context, provider, child) {
                return Text("Counter: ${provider.counter}");
              },
            ),
            ElevatedButton(
              onPressed: () => context.read&lt;CounterProvider&gt;().increment(),
              child: Text("Increment"),
            ),
          ],
        ),
      ),
    );
  }
}
    </code>
  </pre>
  <p>✅ Best for: Managing global state across multiple widgets.</p>
</div>

<div>
  <h3>💡 Which Approach to Choose?</h3>
  <table border="1">
    <tr>
      <th>Approach</th>
      <th>Best Use Case</th>
    </tr>
    <tr>
      <td><code>setState()</code></td>
      <td>When the state change is local to a widget</td>
    </tr>
    <tr>
      <td>Callbacks</td>
      <td>When a parent needs to change a child’s state</td>
    </tr>
    <tr>
      <td><code>GlobalKey</code></td>
      <td>When you need to access a widget’s state from outside</td>
    </tr>
    <tr>
      <td>State Management</td>
      <td>For managing state across multiple widgets efficiently</td>
    </tr>
  </table>
</div>
    
  <h2>2. Difference between StatelessWidget and StatefulWidget?</h2>
  <p><strong>StatelessWidget:</strong> Immutable and cannot change its state after it is built.</p>
  <p><strong>StatefulWidget:</strong> Can change state over time and requires a separate State class.</p>


The SOLID principles are a set of design guidelines that help in creating maintainable, scalable, and testable software. These principles apply to Flutter development just as they do in other object-oriented programming environments.



  <h2>3. What is BuildContext in Flutter?</h2>
  <p>BuildContext is a handle to the location of a widget in the widget tree. It allows access to theme data, navigation, and widget positioning.</p>

  <h2>4. What is Scaffold in Flutter?</h2>
  <p>Scaffold provides a basic structure for a Material Design layout, including an app bar, body, floating action button, bottom navigation, and more.</p>
  <pre><code>Scaffold(
  appBar: AppBar(title: Text("My App")),
  body: Center(child: Text("Hello, Flutter!")),
  floatingActionButton: FloatingActionButton(onPressed: () {}, child: Icon(Icons.add)),
);</code></pre>

  <h2>5. What are the different state management techniques in Flutter?</h2>
    <ul>
        <li>setState</li>
        <li>Provider</li>
        <li>Riverpod</li>
        <li>BLoC (Business Logic Component)</li>
        <li>GetX</li>
    </ul>

  <h2>6. How do you make an API call in Flutter?</h2>
    <p>Use the <code>http</code> package for making API calls.</p>
  
  <pre><code>import 'package:http/http.dart' as http;
Future<void> fetchData() async {
  var response = await http.get(Uri.parse('https://api.example.com/data'));
  print(response.body);
}</code></pre>

<h2>7. What is the difference between final and const in Flutter?</h2>
    <ul>
        <li><strong>final:</strong> Can be assigned only once and is determined at runtime.</li>
        <li><strong>const:</strong> Compile-time constant that cannot change.</li>
    </ul>
    
<h2>8. How do you navigate between screens in Flutter?</h2>
<pre><code>Navigator.push(context, MaterialPageRoute(builder: (context) => SecondScreen()));</code></pre>

<h2>9. What is FutureBuilder in Flutter?</h2>
<p>FutureBuilder is a widget that builds itself based on the latest snapshot of a Future.</p>

<h2>10. What is the purpose of the main() function in Flutter?</h2>
<p>The <code>main()</code> function is the entry point of a Flutter application and calls <code>runApp()</code> to launch the app.</p>

<h2>11. What are Slivers in Flutter?</h2>
<p>Slivers are scrollable areas that create custom scrolling effects like parallax and collapsing app bars.</p>

<h2>12. What is a WebSocket in Flutter?</h2>
<p>WebSockets allow real-time communication between a client and server, maintaining an open connection.</p>

<h2>13. What is the difference between Hot Reload and Hot Restart?</h2>
<ul>
        <li><strong>Hot Reload:</strong> Preserves the app state while applying code changes.</li>
        <li><strong>Hot Restart:</strong> Restarts the entire app, clearing its state.</li>
</ul>

<h2>14. How do you handle background tasks in Flutter?</h2>
    <ul>
        <li>Using Isolates</li>
        <li>Using WorkManager plugin</li>
        <li>Using Firebase Cloud Functions</li>
    </ul>

<h2>15. What is the Observer Pattern in Flutter?</h2>
<p>Flutter's ChangeNotifier and Provider use the Observer pattern to notify UI elements of state changes.</p>

<h2>16. What is GetX in Flutter?</h2>
<p>GetX is a lightweight and powerful Flutter framework for state management, dependency injection, and route management.</p>

<h2>17. What is a singleton in Flutter?</h2>
    <p>A singleton is a design pattern ensuring a class has only one instance across the app lifecycle.</p>
    <pre><code>class Singleton {
  static final Singleton _instance = Singleton._internal();
  factory Singleton() => _instance;
  Singleton._internal();
}</code></pre>

<h2>18. How do you handle errors in Flutter?</h2>
    <ul>
        <li>Using try-catch blocks</li>
        <li>Using FlutterError.onError</li>
        <li>Using custom error handlers</li>
</ul>

<h2>19. How do you optimize Flutter app performance?</h2>
    <ul>
        <li>Minimize widget rebuilds</li>
        <li>Use const constructors</li>
        <li>Use efficient image loading techniques</li>
        <li>Profile using Flutter DevTools</li>
</ul>

<h2>20. What are the advantages of Flutter?</h2>
    <ul>
        <li>Single codebase for multiple platforms</li>
        <li>Fast performance with Skia rendering engine</li>
        <li>Hot reload feature</li>
        <li>Rich widget library</li>
    </ul>

<h2>21. How does Flutter handle responsive UI design?</h2>
<p>Flutter provides widgets like MediaQuery, LayoutBuilder, and packages like flutter_screenutil to adapt UI based on screen size.</p>

<h2>22. What is the difference between Flexible and Expanded?</h2>
<p><strong>Flexible:</strong> Allows a widget to occupy available space but does not force it.</p>
<p><strong>Expanded:</strong> Forces a widget to take all available space.</p>

<h2>23. What is the difference between SizedBox and Container?</h2>
<p><strong>SizedBox:</strong> Used to define a specific width and height without additional properties.</p>
<p><strong>Container:</strong> More flexible, allowing padding, decoration, margin, etc.</p>

<h2>24. Explain the role of MediaQuery in Flutter.</h2>
<p>MediaQuery provides information about the screen size, orientation, and other display properties, helping in building responsive UIs.</p>

<h2>25. What are Slivers, and why are they used?</h2>
<p>Slivers are scrollable areas used within CustomScrollView to create smooth scrolling effects.</p>

<h2>26. What is the difference between Stack and Column/Row?</h2>
<p>Stack positions widgets on top of each other, whereas Column and Row align widgets in a vertical or horizontal sequence.</p>

<h2>27. How do you handle screen orientation changes in Flutter?</h2>
<p>Use the OrientationBuilder widget to rebuild UI when the device orientation changes.</p>

<h2>28. What is the use of CustomPainter in Flutter?</h2>
<p>CustomPainter allows creating complex custom shapes, graphics, and animations using the Canvas API.</p>

<h2>29. What is Hero animation, and how does it work?</h2>
<p>Hero animations provide seamless transitions between screens using shared elements identified by a Hero tag.</p>

<h2>30. How do you create a custom widget in Flutter?</h2>
<p>Create a reusable StatelessWidget or StatefulWidget by extending the respective class.</p>

<h2>31. How do you make an API call with Dio in Flutter?</h2>
<pre><code>import 'package:dio/dio.dart';
Dio dio = Dio();
Future<void> fetchData() async {
  var response = await dio.get('https://api.example.com/data');
  print(response.data);
}</code></pre>

<h2>32. How do you handle API errors in Flutter?</h2>
<p>Use try-catch blocks and handle different HTTP status codes gracefully.</p>

<h2>33. How can you implement pagination in a ListView?</h2>
<p>Use ListView.builder along with a scroll listener to fetch more data when reaching the end.</p>

<h2>34. What is the difference between FutureBuilder and StreamBuilder?</h2>
<p><strong>FutureBuilder:</strong> Used for handling one-time async operations.</p>
<p><strong>StreamBuilder:</strong> Used for continuous data streams like WebSockets.</p>

<h2>35. How do you implement WebSocket communication in Flutter?</h2>
<pre><code>import 'dart:io';
WebSocket.connect('ws://example.com/socket').then((WebSocket socket) {
  socket.listen((data) {
    print("Received: \$data");
  });
});</code></pre>

<h2>36. How do you cache API responses in Flutter?</h2>
<p>Use shared_preferences, hive, or dio_cache_interceptor to store API responses locally.</p>

<h2>37. What is the use of GraphQL in Flutter?</h2>
<p>GraphQL allows fetching only the required data instead of entire endpoints, reducing network usage.</p>

<h2>38. How do you handle authentication tokens in Flutter apps?</h2>
<p>Store tokens securely using flutter_secure_storage or shared_preferences.</p>

<h2>39. How do you upload an image to a server using Flutter?</h2>
<pre><code>import 'package:http/http.dart' as http;
import 'dart:io';
Future<void> uploadImage(File image) async {
  var request = http.MultipartRequest('POST', Uri.parse('https://api.example.com/upload'));
  request.files.add(await http.MultipartFile.fromPath('image', image.path));
  var response = await request.send();
}</code></pre>

<h2>40. How do you handle deep linking in Flutter?</h2>
<p>Use Firebase Dynamic Links or go_router package to handle deep links efficiently.</p>

<h2>41. What are the different local storage options in Flutter?</h2>
<p>Flutter provides options like SharedPreferences, Hive, Sqflite, and SecureStorage for storing data locally.</p>

<h2>42. How do you use SharedPreferences in Flutter?</h2>
<pre><code>import 'package:shared_preferences/shared_preferences.dart';
Future<void> saveData() async {
  final prefs = await SharedPreferences.getInstance();
  await prefs.setString('username', 'JohnDoe');
}</code></pre>

<h2>43. What is Hive, and how does it compare to Sqflite?</h2>
<p>Hive is a NoSQL key-value database optimized for performance, while Sqflite is a SQL-based relational database.</p>

<h2>44. Explain Firebase Firestore vs Firebase Realtime Database.</h2>
<p>Firestore is a scalable document-based database, whereas Realtime Database stores data in JSON format.</p>

<h2>45. How do you implement SQLite in Flutter?</h2>
<pre><code>import 'package:sqflite/sqflite.dart';
Database database = await openDatabase('my_db.db');</code></pre>

<h2>46. What is the use of Isar database?</h2>
<p>Isar is a fast, lightweight NoSQL database that supports complex queries and relationships.</p>

<h2>47. How do you store encrypted data in Flutter?</h2>
<p>Use flutter_secure_storage or encrypt package to store encrypted data securely.</p>

<h2>48. How do you handle large amounts of data efficiently in Flutter?</h2>
<p>Use pagination, lazy loading, and efficient database queries to handle large data sets.</p>

<h2>49. What is ObjectBox, and why is it useful?</h2>
<p>ObjectBox is a high-performance NoSQL database with support for reactive queries.</p>

<h2>50. Explain the use of Secure Storage in Flutter.</h2>
<p>Secure Storage ensures sensitive data is encrypted and stored safely on a device.</p>

<h2>51. How do you improve the performance of a Flutter app?</h2>
<p>Optimize widget rebuilds, use const constructors, and reduce unnecessary UI redraws.</p>

<h2>52. What is tree shaking, and how does it help in Flutter?</h2>
<p>Tree shaking removes unused code during compilation, reducing app size.</p>

<h2>53. How do you profile a Flutter app using DevTools?</h2>
<p>Use Flutter DevTools to analyze UI performance, memory usage, and CPU profiling.</p>

<h2>54. What is repaint boundary, and how does it improve performance?</h2>
<p>Repaint boundaries limit the area that needs to be redrawn, improving efficiency.</p>

<h2>55. What is Flutter's rendering pipeline, and how does it work?</h2>
<p>Flutter's rendering pipeline consists of build, layout, paint, and compositing phases.</p>

<h2>56. How do you reduce widget rebuilds in Flutter?</h2>
<p>Use const constructors, ValueListenableBuilder, and Efficient ListView builders.</p>

<h2>57. What is laggy scrolling, and how do you optimize it?</h2>
<p>Laggy scrolling happens due to expensive UI operations; use ListView.builder and caching.</p>

<h2>58. What is the difference between const and final in Flutter?</h2>
<p>const is a compile-time constant, while final is determined at runtime.</p>

<h2>59. How do you optimize memory usage in Flutter?</h2>
<p>Dispose of controllers, avoid memory leaks, and use efficient data structures.</p>

<h2>60. How do you use isolate for background processing?</h2>
<pre><code>import 'dart:isolate';
void startBackgroundTask(SendPort sendPort) {
  sendPort.send("Task Completed");
}</code></pre>

<h2>61. What is Navigator 1.0 vs Navigator 2.0?</h2>
<p>Navigator 1.0 uses a stack-based approach with push/pop methods, whereas Navigator 2.0 provides declarative navigation using Router and Page APIs.</p>

<h2>62. How do you pass data between two screens in Flutter?</h2>
<pre><code>Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => SecondScreen(data: 'Hello'),
  ),
);</code></pre>

<h2>63. What is named routing, and why is it useful?</h2>
<p>Named routes simplify navigation by defining route names in a centralized way.</p>

<h2>64. How do you implement deep linking in Flutter?</h2>
<p>Use Firebase Dynamic Links or go_router to handle deep links efficiently.</p>

<h2>65. What is GoRouter, and how does it work?</h2>
<p>GoRouter is a declarative routing package for Flutter that simplifies navigation, deep linking, and redirections.</p>

<h2>66. How do you implement bottom navigation in Flutter?</h2>
<pre><code>BottomNavigationBar(
  items: [
    BottomNavigationBarItem(icon: Icon(Icons.home), label: 'Home'),
    BottomNavigationBarItem(icon: Icon(Icons.settings), label: 'Settings'),
  ],
);</code></pre>

<h2>67. How do you use PageView for swipe navigation?</h2>
<pre><code>PageView(
  children: [Page1(), Page2(), Page3()],
);</code></pre>

<h2>68. How does WillPopScope work in Flutter?</h2>
<p>WillPopScope prevents users from exiting a screen unless a condition is met.</p>

<h2>69. What is modal bottom sheet, and how is it different from a dialog?</h2>
<p>A modal bottom sheet appears from the bottom, while a dialog appears in the center.</p>

<h2>70. What is auto_route, and why should you use it?</h2>
<p>auto_route is a code-generation package that simplifies navigation management in Flutter apps.</p>

<h2>71. What are the different types of animations in Flutter?</h2>
<ul>
    <li>Implicit Animations (AnimatedContainer, AnimatedOpacity)</li>
    <li>Explicit Animations (AnimationController, Tween)</li>
</ul>

<h2>72. How does the AnimationController work?</h2>
<p>AnimationController controls the timing of an animation, providing control over start, stop, and repeat.</p>

<h2>73. What is TweenAnimationBuilder, and how is it useful?</h2>
<p>TweenAnimationBuilder animates between two values over a specified duration.</p>

<h2>74. How do you implement fade animations in Flutter?</h2>
<pre><code>FadeTransition(
  opacity: animation,
  child: MyWidget(),
);</code></pre>

<h2>75. What is the difference between AnimatedContainer and Container?</h2>
<p>AnimatedContainer automatically animates changes, while Container updates instantly.</p>

<h2>76. What is Lottie animation, and how do you use it?</h2>
<p>Lottie allows using JSON-based animations in Flutter.</p>

<h2>77. How do you create a custom animation in Flutter?</h2>
<p>Use AnimationController and Tween for custom animations.</p>

<h2>78. How do you implement physics-based animations?</h2>
<p>Use the physics package or SpringSimulation for realistic animations.</p>

<h2>79. What is Flare animation, and how does it work?</h2>
<p>Flare is an advanced animation tool that allows vector-based animations.</p>

<h2>80. How do you use AnimationBuilder in Flutter?</h2>
<pre><code>AnimatedBuilder(
  animation: animation,
  builder: (context, child) {
    return Transform.scale(scale: animation.value, child: child);
  },
  child: MyWidget(),
);</code></pre>

<h2>81. What are the different types of testing in Flutter?</h2>
<ul>
    <li>Unit Tests</li>
    <li>Widget Tests</li>
    <li>Integration Tests</li>
</ul>

<h2>82. How do you write unit tests in Flutter?</h2>
<p>Use the flutter_test package to test business logic.</p>

<h2>83. How do you write widget tests in Flutter?</h2>
<p>Use WidgetTester to simulate UI interactions.</p>

<h2>84. What is mocking, and why is it used in testing?</h2>
<p>Mocking simulates dependencies for unit testing.</p>

<h2>85. How do you debug a Flutter app using Flutter DevTools?</h2>
<p>Use DevTools to inspect UI, analyze performance, and debug memory usage.</p>

<h2>86. What are golden tests, and when should you use them?</h2>
<p>Golden tests compare UI snapshots to detect visual changes.</p>

<h2>87. What is the difference between Flutter Inspector and Debug Console?</h2>
<p>Flutter Inspector visualizes UI hierarchy, while Debug Console logs errors and prints statements.</p>

<h2>88. How do you handle errors in Flutter?</h2>
<p>Use try-catch, ErrorWidget.builder, and FlutterError.onError.</p>

<h2>89. What is the use of FlutterError.onError?</h2>
<p>FlutterError.onError captures and handles framework errors globally.</p>

<h2>90. How do you test API calls in Flutter?</h2>
<p>Use the mockito package to mock API responses.</p>

<h2>91. What is Flutter Web, and how does it work?</h2>
<p>Flutter Web compiles Dart code to JavaScript for web applications.</p>

<h2>92. How do you create a Flutter plugin?</h2>
<p>Use the flutter create --template=plugin command.</p>

<h2>93. What is Platform Channels, and how do they work?</h2>
<p>Platform Channels allow Flutter to communicate with native Android/iOS code.</p>

<h2>94. How do you integrate native code (Kotlin/Swift) in Flutter?</h2>
<p>Use MethodChannel to invoke native methods.</p>

<h2>95. What is the difference between MethodChannel and EventChannel?</h2>
<p>MethodChannel is for single responses, while EventChannel streams continuous data.</p>

<h2>96. How do you build a Flutter app for desktop?</h2>
<p>Enable desktop support using flutter config --enable-windows-desktop.</p>

<h2>97. What is Flutter FFI, and when should you use it?</h2>
<p>FFI (Foreign Function Interface) allows calling native C code from Flutter.</p>

<h2>98. How do you handle background tasks in Flutter?</h2>
<p>Use isolates, background services, and WorkManager.</p>

<h2>99. How do you optimize Flutter Web apps?</h2>
<p>Minimize asset sizes, use deferred loading, and optimize JavaScript output.</p>

<h2>100. What are Flutter’s limitations, and how can they be overcome?</h2>
<p>Flutter lacks advanced platform-specific APIs, but using plugins and platform channels helps mitigate this.</p>
<p>We are continuously updating this guide. Stay tuned for more interview questions and answers.</p>
<p>We are continuously updating this guide. Stay tuned for more interview questions and answers.</p>
    <p>We are continuously updating this guide. Stay tuned for more interview questions and answers.</p>


