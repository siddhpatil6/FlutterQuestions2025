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
<p>object of the child class must be able to replace the object of the parent class without breaking the application</p>
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
<h1>1️⃣ createState()</h1>
  <p>📌 What it does?</p>
  <p>- Called once when the widget is first created.</p>
  <p>- Returns an instance of the State class.</p>
  <p>📝 Example:</p>
  <code>
    class MyWidget extends StatefulWidget {<br>
      @override<br>
      _MyWidgetState createState() {<br>
        print("createState() called");<br>
        return _MyWidgetState();<br>
      }<br>
    }
  </code>
  <p>🔹 Key Points:</p>
  <p>✔️ Used to create the state object.</p>
  <p>✔️ Called only once when the widget is first inserted.</p>

  <h1>2️⃣ initState()</h1>
  <p>📌 What it does?</p>
  <p>- Called once when the widget is first added to the widget tree.</p>
  <p>- Used for initialization, like setting up API calls, animation controllers, and streams.</p>
  <p>📝 Example: Fetching API Data</p>
  <code>
    class _MyWidgetState extends State&lt;MyWidget&gt; {<br>
      @override<br>
      void initState() {<br>
        super.initState();<br>
        print("initState() called");<br>
      }<br>
    }
  </code>
  <p>🔹 Key Points:</p>
  <p>✔️ Runs only once when the widget is created.</p>
  <p>✔️ Used for fetching API data, initializing variables, or setting up listeners.</p>

  <h1>3️⃣ didChangeDependencies()</h1>
  <p>📌 What it does?</p>
  <p>- Called when inherited widgets (like Theme or Locale) change.</p>
  <p>- Runs after initState().</p>
  <p>📝 Example: Listening for Theme Changes</p>
  <code>
    class _MyWidgetState extends State&lt;MyWidget&gt; {<br>
      @override<br>
      void didChangeDependencies() {<br>
        super.didChangeDependencies();<br>
        print("didChangeDependencies() called");<br>
      }<br>
    }
  </code>
  <p>🔹 Key Points:</p>
  <p>✔️ Useful when using MediaQuery or Theme.of(context).</p>
  <p>✔️ Called when dependencies change (e.g., after setState() in a parent widget).</p>

  <h1>4️⃣ build()</h1>
  <p>📌 What it does?</p>
  <p>- Called every time the UI needs to be redrawn.</p>
  <p>- Returns the widget tree that defines the UI.</p>
  <p>📝 Example: Button to Change State</p>
  <code>
    class _MyWidgetState extends State&lt;MyWidget&gt; {<br>
      int counter = 0;<br>
      @override<br>
      Widget build(BuildContext context) {<br>
        print("build() called");<br>
        return Column(<br>
          children: [<br>
            Text("Counter: $counter"),<br>
            ElevatedButton(<br>
              onPressed: () {<br>
                setState(() {<br>
                  counter++;<br>
                });<br>
              },<br>
              child: Text("Increment"),<br>
            ),<br>
          ],<br>
        );<br>
      }<br>
    }
  </code>
  <p>🔹 Key Points:</p>
  <p>✔️ Runs every time setState() is called.</p>
  <p>✔️ Used to create UI elements dynamically.</p>

  <h1>5️⃣ didUpdateWidget()</h1>
  <p>📌 What it does?</p>
  <p>- Called when the parent widget rebuilds and provides new properties to the child.</p>
  <p>- Useful when the widget reuses state instead of creating a new instance.</p>
  <p>📝 Example: Detecting Prop Changes</p>
  <code>
    class _MyWidgetState extends State&lt;MyWidget&gt; {<br>
      @override<br>
      void didUpdateWidget(covariant MyWidget oldWidget) {<br>
        super.didUpdateWidget(oldWidget);<br>
        print("didUpdateWidget() called - Old: ${oldWidget.text}, New: ${widget.text}");<br>
      }<br>
    }
  </code>

  <h1>6️⃣ deactivate()</h1>
  <p>📌 What it does?</p>
  <p>- Called before a widget is removed from the widget tree.</p>
  <p>- Happens when the widget moves to another part of the tree but is not destroyed.</p>
  <p>📝 Example: Tracking Widget Movement</p>
  <code>
    class _MyWidgetState extends State&lt;MyWidget&gt; {<br>
      @override<br>
      void deactivate() {<br>
        super.deactivate();<br>
        print("deactivate() called");<br>
      }<br>
    }
  </code>

  <h1>7️⃣ dispose()</h1>
  <p>📌 What it does?</p>
  <p>- Called when the widget is permanently removed from the widget tree.</p>
  <p>- Used to clean up resources (e.g., close streams, cancel timers, dispose controllers).</p>
  <p>📝 Example: Closing a Stream</p>
  <code>
    class _MyWidgetState extends State&lt;MyWidget&gt; {<br>
      late StreamController&lt;int&gt; _controller;<br>
      @override<br>
      void initState() {<br>
        super.initState();<br>
        _controller = StreamController&lt;int&gt;();<br>
      }<br>
      @override<br>
      void dispose() {<br>
        _controller.close(); // Free up resources<br>
        print("dispose() called");<br>
        super.dispose();<br>
      }<br>
    }
  </code>

  <h1>🚀 Lifecycle Flow</h1>
  <p>1️⃣ createState() → Creates the state object</p>
  <p>2️⃣ initState() → Initialize variables, API calls, etc.</p>
  <p>3️⃣ didChangeDependencies() → Runs if inherited widgets (Theme, Locale) change</p>
  <p>4️⃣ build() → Draws the UI</p>
  <p>🔄 didUpdateWidget() → Called when widget properties change</p>
  <p>🔽 deactivate() → Called before removal</p>
  <p>🛑 dispose() → Clean up resources before destruction</p>

  <h1>🚀 Summary Table</h1>
  <table border="1">
    <tr>
      <th>Lifecycle Method</th>
      <th>Purpose</th>
    </tr>
    <tr>
      <td>createState()</td>
      <td>Creates the State object</td>
    </tr>
    <tr>
      <td>initState()</td>
      <td>Initialize variables, controllers, API calls</td>
    </tr>
    <tr>
      <td>didChangeDependencies()</td>
      <td>Runs when InheritedWidget (like Theme) changes</td>
    </tr>
    <tr>
      <td>build()</td>
      <td>Builds UI, called on setState()</td>
    </tr>
    <tr>
      <td>didUpdateWidget()</td>
      <td>Runs when widget properties change</td>
    </tr>
    <tr>
      <td>deactivate()</td>
      <td>Runs before the widget is removed/moved</td>
    </tr>
    <tr>
      <td>dispose()</td>
      <td>Cleanup: Close streams, controllers, etc.</td>
    </tr>
  </table>

  <h2>What is ChangeNotifier in Provider?</h2>

<p>In Flutter, <strong>ChangeNotifier</strong> helps manage state efficiently with the <strong>Provider</strong> package. It notifies widgets when state changes, triggering UI rebuilds.</p>

<h2>Key Points</h2>
<ul>
  <li>Part of Flutter's foundation library.</li>
  <li>Notifies listeners when state changes.</li>
  <li>Used with <strong>Provider</strong> for state management.</li>
</ul>

<h2>How ChangeNotifier Works</h2>
<p>1. Extend <strong>ChangeNotifier</strong> in a class.<br>
2. Call <strong>notifyListeners()</strong> to notify changes.<br>
3. Wrap app with <strong>ChangeNotifierProvider</strong>.<br>
4. Use <strong>context.watch&lt;T&gt;()</strong> or <strong>context.read&lt;T&gt;()</strong> to access state.</p>

<h2>Example</h2>

<h3>Step 1: Create a ChangeNotifier Class</h3>
<pre><code>
import 'package:flutter/material.dart';

class CounterProvider extends ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners(); // Notify UI to rebuild
  }
}
</code></pre>

<h3>Step 2: Register Provider</h3>
<pre><code>
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'counter_provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => CounterProvider(),
      child: MyApp(),
    ),
  );
}
</code></pre>

<h3>Step 3: Access Provider in UI</h3>
<pre><code>
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'counter_provider.dart';

class CounterScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Provider Example")),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Counter: ${context.watch&lt;CounterProvider&gt;().count}',
              style: TextStyle(fontSize: 20),
            ),
            ElevatedButton(
              onPressed: () {
                context.read&lt;CounterProvider&gt;().increment();
              },
              child: Text("Increment"),
            ),
          ],
        ),
      ),
    );
  }
}
</code></pre>

<h2>Explanation</h2>
<ul>
  <li><strong>ChangeNotifierProvider</strong> provides <strong>CounterProvider</strong> to the widget tree.</li>
  <li><strong>context.watch&lt;T&gt;()</strong> listens for changes and rebuilds UI.</li>
  <li><strong>context.read&lt;T&gt;()</strong> gets instance without listening (used for actions).</li>
</ul>

<h2>Benefits</h2>
<ul>
  <li>Separates state from UI.</li>
  <li>Improves performance.</li>
  <li>Scalable state management.</li>
</ul>

<p>Using <strong>ChangeNotifier</strong> with <strong>Provider</strong> makes Flutter apps efficient and maintainable! 🚀</p>


<h1>How can I change state of particular widget? </h1>

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

<h2>When to Choose Flutter vs Native App Development</h2>

<h3>When to Choose Flutter</h3>

<ul>
  <li><strong>Simple Business Apps / CRUD Applications:</strong>
    <p>Example: A simple inventory management app, a note-taking app, or a to-do list.</p>
    <p>Why Flutter: Flutter is perfect for apps that don't require complex native features and are more about displaying data, user interaction, and simple logic. It enables fast development for cross-platform apps with consistent UI/UX.</p>
  </li>
  <li><strong>Apps with Basic Navigation & Forms:</strong>
    <p>Example: E-commerce apps with basic shopping cart functionality or a form-based app (e.g., job application forms).</p>
    <p>Why Flutter: The navigation system in Flutter is easy to use and set up, and creating forms and data-entry screens is straightforward. Flutter’s widget system allows for easy customization and a good UI experience on both iOS and Android.</p>
  </li>
  <li><strong>Cross-Platform Apps with Consistent UI/UX:</strong>
    <p>Example: News reader apps, blogs, or media apps with similar layout requirements across both platforms.</p>
    <p>Why Flutter: Since Flutter uses a single codebase for both iOS and Android, it helps maintain consistent design and behavior across platforms without extra work.</p>
  </li>
  <li><strong>Prototyping & MVP Development:</strong>
    <p>Example: A prototype for a fitness tracking app or an event booking app.</p>
    <p>Why Flutter: Flutter’s "hot reload" feature makes it ideal for building prototypes quickly and iterating without waiting for long compilation times. It helps developers rapidly test and adjust UI elements and logic.</p>
  </li>
  <li><strong>Apps with Moderate Performance Needs:</strong>
    <p>Example: Social media apps, travel apps, or educational apps.</p>
    <p>Why Flutter: Flutter provides near-native performance for most use cases. It’s ideal for apps where you don’t require complex animations or very high performance but still want a smooth and responsive experience.</p>
  </li>
</ul>

<h3>When to Choose Native Development</h3>

<ul>
  <li><strong>Heavy Graphics & Gaming Apps:</strong>
    <p>Example: High-performance games or AR apps.</p>
    <p>Why Native: Native development gives you direct access to platform-specific graphics APIs (e.g., Metal for iOS, Vulkan for Android), allowing for better optimization and rendering. Flutter is not designed for high-end 3D games or complex real-time graphics.</p>
  </li>
  <li><strong>Apps with Intensive Background Processing:</strong>
    <p>Example: Fitness apps that track real-time heart rate or a GPS tracking app that needs to constantly run in the background.</p>
    <p>Why Native: Native development provides more control over background tasks and allows deeper integration with the OS for things like persistent background services, more efficient resource management, and handling long-running processes.</p>
  </li>
  <li><strong>Complex Animations and Transitions:</strong>
    <p>Example: Complex animation sequences in design-heavy apps like video editing tools or apps with intricate transitions.</p>
    <p>Why Native: Native SDKs provide more powerful and optimized tools for creating complex animations. You can better control the animation performance and behavior, and ensure smooth transitions tailored to each platform.</p>
  </li>
  <li><strong>Advanced Hardware Interactions:</strong>
    <p>Example: Apps using the camera, microphone, or sensors in unique ways (e.g., facial recognition or augmented reality).</p>
    <p>Why Native: Native development allows for full access to platform-specific hardware APIs, which is critical for apps that need to interact with the camera, GPS, accelerometer, or other sensors in real-time. While Flutter supports plugins for these features, native code often offers more stability and speed.</p>
  </li>
  <li><strong>Platform-Specific User Interface and Behavior:</strong>
    <p>Example: An app that needs to integrate deeply with iOS or Android-specific UI components, such as push notifications, widget-based home screen elements (Android), or Siri/Google Assistant integration.</p>
    <p>Why Native: Native development allows you to follow the platform-specific UI/UX guidelines more closely, ensuring that your app feels fully integrated with the OS. For example, Apple’s design principles (e.g., use of swipe gestures) are more easily implemented using Swift or Objective-C, whereas Android’s material design can be fully leveraged with Kotlin or Java.</p>
  </li>
  <li><strong>Native SDK & APIs Integration:</strong>
    <p>Example: Apps requiring third-party integrations, such as payment systems (e.g., Apple Pay, Google Pay) or platform-specific services (e.g., iCloud or Firebase Cloud Messaging).</p>
    <p>Why Native: While Flutter supports third-party plugins, some newer or more complex native SDKs may not have full support or may require additional development work. In cases where you need deep integration with a platform’s SDK or API, native code offers direct access and greater flexibility.</p>
  </li>
</ul>

<h3>Summary of When to Choose Native vs Flutter</h3>

<table border="1">
  <thead>
    <tr>
      <th>Feature</th>
      <th>Use Flutter</th>
      <th>Use Native</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Basic Business Apps / CRUD</td>
      <td>✅ Flutter</td>
      <td>❌ Native</td>
    </tr>
    <tr>
      <td>Cross-Platform UI Consistency</td>
      <td>✅ Flutter</td>
      <td>❌ Native (needs separate codebases for iOS and Android)</td>
    </tr>
    <tr>
      <td>Complex Animations</td>
      <td>❌ Flutter (limited in complex animations)</td>
      <td>✅ Native (better performance & fine-grained control)</td>
    </tr>
    <tr>
      <td>Real-Time Graphics or Gaming</td>
      <td>❌ Flutter (limited for complex games)</td>
      <td>✅ Native (best for high-end graphics and gaming)</td>
    </tr>
    <tr>
      <td>Background Processing (e.g., GPS tracking)</td>
      <td>❌ Flutter (limited background task handling)</td>
      <td>✅ Native (better handling of background tasks)</td>
    </tr>
    <tr>
      <td>Hardware Interaction (e.g., Camera, Sensors)</td>
      <td>✅ Flutter (via plugins, but may be slower)</td>
      <td>✅ Native (full access to platform-specific features)</td>
    </tr>
    <tr>
      <td>Advanced UI Customization (Native look)</td>
      <td>✅ Flutter (if cross-platform consistency is needed)</td>
      <td>✅ Native (for platform-specific UI feel)</td>
    </tr>
    <tr>
      <td>Deep Integration with Platform-Specific SDKs</td>
      <td>✅ Flutter (via plugins, but may need workarounds)</td>
      <td>✅ Native (full control and access to SDKs/APIs)</td>
    </tr>
  </tbody>
</table>


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


