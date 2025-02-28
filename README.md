# FlutterQuestions2025

  <h1>Flutter Interview Questions & Answers</h1>
    
  <h2>1. What is Flutter?</h2>
  <p>Flutter is an open-source UI toolkit developed by Google for building natively compiled applications for mobile, web, and desktop from a single codebase.</p>
    
  <h2>2. Difference between StatelessWidget and StatefulWidget?</h2>
  <p><strong>StatelessWidget:</strong> Immutable and cannot change its state after it is built.</p>
  <p><strong>StatefulWidget:</strong> Can change state over time and requires a separate State class.</p>

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

    
