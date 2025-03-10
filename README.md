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

  <h2>How to Avoid Memory Leaks in Flutter (Simplified)</h2>

<h3>1️⃣ Dispose Controllers (Like TextEditingController, AnimationController, etc.)</h3>
<p>✅ <b>Why?</b> If you don’t dispose of controllers, they keep using memory even when the widget is removed.</p>
<pre>
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  TextEditingController _controller = TextEditingController();

  @override
  void dispose() {
    _controller.dispose();  // ✅ Free up memory
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return TextField(controller: _controller);
  }
}
</pre>

<h3>2️⃣ Cancel Streams & Subscriptions</h3>
<p>✅ <b>Why?</b> Streams keep running in the background if not canceled, leading to memory leaks.</p>
<pre>
late StreamSubscription _subscription;

@override
void initState() {
  super.initState();
  _subscription = someStream.listen((data) {
    print(data);
  });
}

@override
void dispose() {
  _subscription.cancel();  // ✅ Stop the stream
  super.dispose();
}
</pre>

<h3>3️⃣ Close Database Connections (Like SQLite, Firebase)</h3>
<p>✅ <b>Why?</b> Keeping a database connection open when it’s not needed wastes memory.</p>
<pre>
@override
void dispose() {
  database.close();  // ✅ Close database when done
  super.dispose();
}
</pre>

<h3>4️⃣ Remove Listeners (Like ScrollController, FocusNode, etc.)</h3>
<p>✅ <b>Why?</b> If you attach a listener but don’t remove it, it stays in memory.</p>
<pre>
ScrollController _scrollController = ScrollController();

@override
void initState() {
  super.initState();
  _scrollController.addListener(() {
    print("Scrolling...");
  });
}

@override
void dispose() {
  _scrollController.dispose();  // ✅ Remove listener
  super.dispose();
}
</pre>

<h3>5️⃣ Use Stateful Widgets Only When Needed</h3>
<p>✅ <b>Why?</b> Too many <code>StatefulWidgets</code> can hold unnecessary memory.</p>
<p>🚀 <b>Tip:</b> If a widget doesn’t need to change, use <code>StatelessWidget</code> instead!</p>
<pre>
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Text("Hello, Flutter!"); // ✅ No unnecessary state
  }
}
</pre>

<h3>6️⃣ Use ListView.builder Instead of ListView</h3>
<p>✅ <b>Why?</b> <code>ListView.builder</code> loads only the visible items, reducing memory usage.</p>
<pre>
ListView.builder(
  itemCount: 1000,
  itemBuilder: (context, index) {
    return ListTile(title: Text("Item $index"));
  },
);
</pre>

<h3>7️⃣ Use const for Widgets That Don’t Change</h3>
<p>✅ <b>Why?</b> <code>const</code> widgets don’t rebuild unnecessarily, saving memory.</p>
<pre>
const Text("This is a constant text");  // ✅ Won't rebuild
</pre>

<h3>Conclusion</h3>
<ul>
  <li>✅ Dispose controllers (TextEditingController, AnimationController, etc.)</li>
  <li>✅ Cancel streams & subscriptions</li>
  <li>✅ Close database connections when done</li>
  <li>✅ Remove unused listeners</li>
  <li>✅ Use StatefulWidget only when needed</li>
  <li>✅ Use ListView.builder for large lists</li>
  <li>✅ Use const for unchanging widgets</li>
</ul>

  <h2>BLoC Explained in a Super Simple Way 🚀</h2>  

<p>Think of <strong>BLoC (Business Logic Component)</strong> as a <strong>chef</strong> in a restaurant. The <strong>chef (BLoC)</strong> takes <strong>orders (Events)</strong> from customers (users), processes them, and then serves the <strong>prepared dish (State)</strong> back to the customer.</p>  

<h2>🔹 1. BLoC Components</h2>  

<table border="1">
<tr>
<th>Component</th>
<th>What it Does</th>
<th>Example (Cooking) 🍳</th>
</tr>
<tr>
<td><strong>Event</strong></td>
<td>Action triggered by the user</td>
<td>"Make me a pizza!" 🍕</td>
</tr>
<tr>
<td><strong>BLoC</strong></td>
<td>Processes the event and creates a new state</td>
<td>Chef prepares the pizza</td>
</tr>
<tr>
<td><strong>State</strong></td>
<td>The final result that UI displays</td>
<td>A hot, fresh pizza is served! 🍕🔥</td>
</tr>
</table>  

<h2>🔹 2. How BLoC Works? (Step-by-Step)</h2>  
<ol>
<li>User clicks a button <strong>(Event sent to BLoC)</strong></li>
<li>BLoC <strong>processes</strong> the event and updates the <strong>State</strong></li>
<li>UI listens to <strong>State changes</strong> and updates automatically</li>
</ol>  

<h2>🔹 3. Code Example: Counter App 🧮</h2>  

<h3>📌 Step 1: Add BLoC in <code>pubspec.yaml</code></h3>  
<pre>
<code>
dependencies:
  flutter_bloc: ^8.1.3
</code>
</pre>  

<h3>📌 Step 2: Create Counter Events (User Actions)</h3>  
<pre>
<code>
abstract class CounterEvent {}  // Base event class

class IncrementEvent extends CounterEvent {}  // User pressed '+'
class DecrementEvent extends CounterEvent {}  // User pressed '-'
</code>
</pre>  

<h3>📌 Step 3: Create Counter State (UI Updates)</h3>  
<pre>
<code>
class CounterState {
  final int counter;
  CounterState(this.counter);
}
</code>
</pre>  

<h3>📌 Step 4: Create CounterBloc (Brain of the App)</h3>  
<pre>
<code>
import 'package:flutter_bloc/flutter_bloc.dart';

class CounterBloc extends Bloc<CounterEvent, CounterState> {
  CounterBloc() : super(CounterState(0)) {  // Initial state = 0
    on<IncrementEvent>((event, emit) {
      emit(CounterState(state.counter + 1));  // Increase count
    });

    on<DecrementEvent>((event, emit) {
      emit(CounterState(state.counter - 1));  // Decrease count
    });
  }
}
</code>
</pre>  

<h3>📌 Step 5: Use Bloc in UI</h3>  
<pre>
<code>
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: BlocProvider(
        create: (context) => CounterBloc(),
        child: CounterScreen(),
      ),
    );
  }
}

class CounterScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final counterBloc = context.read<CounterBloc>();

    return Scaffold(
      appBar: AppBar(title: Text("BLoC Counter")),
      body: Center(
        child: BlocBuilder<CounterBloc, CounterState>(
          builder: (context, state) {
            return Text("Counter: ${state.counter}",
                style: TextStyle(fontSize: 30));
          },
        ),
      ),
      floatingActionButton: Row(
        mainAxisAlignment: MainAxisAlignment.end,
        children: [
          FloatingActionButton(
            onPressed: () => counterBloc.add(IncrementEvent()),
            child: Icon(Icons.add),
          ),
          SizedBox(width: 10),
          FloatingActionButton(
            onPressed: () => counterBloc.add(DecrementEvent()),
            child: Icon(Icons.remove),
          ),
        ],
      ),
    );
  }
}
</code>
</pre>  

<h2>🔹 4. Summary</h2>  
<table border="1">
<tr>
<th>Step</th>
<th>What to Do?</th>
<th>Code Example</th>
</tr>
<tr>
<td><strong>1️⃣ Create Events</strong></td>
<td>Define user actions (increment, decrement)</td>
<td><code>IncrementEvent, DecrementEvent</code></td>
</tr>
<tr>
<td><strong>2️⃣ Create State</strong></td>
<td>Store the current counter value</td>
<td><code>CounterState(int counter)</code></td>
</tr>
<tr>
<td><strong>3️⃣ Create BLoC</strong></td>
<td>Process events and update state</td>
<td><code>on<IncrementEvent> emit(CounterState(state.counter + 1))</code></td>
</tr>
<tr>
<td><strong>4️⃣ Provide BLoC</strong></td>
<td>Wrap widget with <code>BlocProvider</code></td>
<td><code>BlocProvider(create: (_) => CounterBloc())</code></td>
</tr>
<tr>
<td><strong>5️⃣ Listen to State</strong></td>
<td>Update UI when state changes</td>
<td><code>BlocBuilder<CounterBloc, CounterState></code></td>
</tr>
</table>  

<h2>🚀 Why Use BLoC?</h2>  
<ul>
<li>✅ <strong>Separation of Logic & UI</strong></li>
<li>✅ <strong>Easier to Manage Large Apps</strong></li>
<li>✅ <strong>Predictable State Changes</strong></li>
</ul>  

<h2>👀 Final Thought</h2>  
<p>BLoC is like a chef! 🍳  
You order a dish (Event), the chef (BLoC) prepares it, and you get the final meal (State).</p>  

  <h2>Difference Between StateProvider and ChangeNotifierProvider in Riverpod ?</h2>

<p>In <strong>Flutter's Riverpod</strong>, <code>StateProvider</code> and <code>ChangeNotifierProvider</code> are used for state management, but they have different use cases.</p>

<h3>1️⃣ StateProvider</h3>

<h4>✅ When to use?</h4>
<ul>
  <li>For <strong>simple, mutable state</strong> (e.g., integers, strings, booleans, small objects).</li>
  <li>Ideal when <strong>state updates are straightforward</strong> (e.g., toggling a boolean, incrementing a counter).</li>
</ul>

<h4>💡 Key Characteristics:</h4>
<ul>
  <li>Holds a <strong>single piece of state</strong> that can be updated.</li>
  <li>Updates are <strong>direct and synchronous</strong>.</li>
  <li>Similar to <code>StateNotifierProvider</code>, but without complex logic.</li>
</ul>

<h4>🔥 Example: Counter App</h4>
<p>A simple counter where the state updates directly:</p>
<ul>
  <li><code>final counterProvider = StateProvider&lt;int&gt;((ref) => 0);</code></li>
  <li><code>ref.read(counterProvider.notifier).state++;</code></li>
</ul>

<p><strong>Best for:</strong> Small UI-related state changes.</p>

<hr>

<h3>2️⃣ ChangeNotifierProvider</h3>

<h4>✅ When to use?</h4>
<ul>
  <li>For <strong>complex state management</strong> where multiple properties change.</li>
  <li>When you need <strong>listeners</strong> to notify UI updates.</li>
  <li>Ideal for <strong>handling multiple states</strong> in a single provider.</li>
</ul>

<h4>💡 Key Characteristics:</h4>
<ul>
  <li>Uses <code>ChangeNotifier</code>, meaning multiple UI widgets can listen for updates.</li>
  <li>Good for <strong>business logic</strong> with methods to modify state.</li>
</ul>

<h4>🔥 Example: Todo List</h4>
<p>A todo list where state updates using <code>notifyListeners()</code>:</p>
<ul>
  <li><code>class TodoModel extends ChangeNotifier { List&lt;String&gt; todos = []; void addTodo(String task) { todos.add(task); notifyListeners(); } }</code></li>
  <li><code>final todoProvider = ChangeNotifierProvider((ref) => TodoModel());</code></li>
</ul>

<p><strong>Best for:</strong> Managing <strong>complex states</strong> like lists, API calls, or forms.</p>

<hr>

<h3>🚀 Quick Comparison Table</h3>
<table border="1">
  <tr>
    <th>Feature</th>
    <th>StateProvider</th>
    <th>ChangeNotifierProvider</th>
  </tr>
  <tr>
    <td><strong>Use case</strong></td>
    <td>Simple state (e.g., int, bool)</td>
    <td>Complex state (e.g., lists, objects)</td>
  </tr>
  <tr>
    <td><strong>State type</strong></td>
    <td>Holds a <strong>single value</strong></td>
    <td>Manages <strong>multiple properties</strong></td>
  </tr>
  <tr>
    <td><strong>Notifies UI?</strong></td>
    <td>UI rebuilds on <code>state</code> change</td>
    <td>Uses <code>notifyListeners()</code></td>
  </tr>
  <tr>
    <td><strong>Best for</strong></td>
    <td>Small UI state (e.g., theme mode, counter)</td>
    <td>Business logic (e.g., todo list, form validation)</td>
  </tr>
  <tr>
    <td><strong>Performance</strong></td>
    <td>Lightweight</td>
    <td>Can be heavy if misused</td>
  </tr>
</table>

<h3>🚀 Which one to use?</h3>
<ul>
  <li>If you just <strong>store and update a single variable</strong> → ✅ Use <code>StateProvider</code></li>
  <li>If you need <strong>complex state management with multiple properties</strong> → ✅ Use <code>ChangeNotifierProvider</code></li>
</ul>



  <h2>Difference Between Microtask and Future.delayed</h2>

<p>In Dart, <code>scheduleMicrotask</code> and <code>Future.delayed</code> have different execution priorities and behaviors.</p>

<h3>Microtask Queue</h3>
<ul>
  <li>Microtasks run <strong>before</strong> any event in the event queue.</li>
  <li>They are used for high-priority, short-lived tasks.</li>
  <li>They execute <strong>immediately after</strong> the current synchronous code finishes.</li>
</ul>

<h3>Future.delayed</h3>
<ul>
  <li><code>Future.delayed(Duration.zero, callback)</code> schedules the task in the event queue.</li>
  <li>It runs after microtasks and other already-scheduled futures.</li>
  <li>It ensures UI updates and avoids blocking the event loop.</li>
</ul>

<h3>Example</h3>
<pre>
<code>
import 'dart:async';

void main() {
  print('Start');

  scheduleMicrotask(() => print('Microtask 1'));
  Future(() => print('Future 1'));
  Future.delayed(Duration.zero, () => print('Future.delayed'));

  print('End');
}
</code>
</pre>

<h3>Output</h3>
<pre>
Start
End
Microtask 1
Future 1
Future.delayed
</pre>

<h3>Key Differences</h3>
<table border="1">
<tr>
  <th>Feature</th>
  <th>Microtask</th>
  <th>Future.delayed</th>
</tr>
<tr>
  <td>Execution Order</td>
  <td>Before event queue</td>
  <td>After microtasks</td>
</tr>
<tr>
  <td>Use Case</td>
  <td>High-priority short tasks</td>
  <td>Deferred execution</td>
</tr>
<tr>
  <td>UI Updates</td>
  <td>Might block UI updates</td>
  <td>Ensures smooth UI rendering</td>
</tr>
</table>

<h3>When to Use</h3>
<ul>
  <li>Use <code>scheduleMicrotask</code> for urgent logic that must run immediately.</li>
  <li>Use <code>Future.delayed(Duration.zero)</code> to defer execution and allow UI updates.</li>
</ul>

<h2>Passing Data from Next Screen to Previous Screen in Flutter</h2>

<h3>1. Understanding the Concept</h3>
<p>When navigating back from the next screen (Screen B) to the previous screen (Screen A), we can pass data using <code>Navigator.pop(context, data)</code>. The previous screen receives this data using <code>await Navigator.push()</code>.</p>

<h3>2. Example Code</h3>

<h4>Screen A (Receiving Data)</h4>
<pre>
class ScreenA extends StatefulWidget {
  @override
  _ScreenAState createState() => _ScreenAState();
}

class _ScreenAState extends State&lt;ScreenA&gt; {
  String message = "No Data Received";

  void navigateToScreenB() async {
    final result = await Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => ScreenB()),
    );

    if (result != null) {
      setState(() {
        message = result;
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Screen A")),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(message, style: TextStyle(fontSize: 18)),
            ElevatedButton(
              onPressed: navigateToScreenB,
              child: Text("Go to Screen B"),
            ),
          ],
        ),
      ),
    );
  }
}
</pre>

<h4>Screen B (Sending Data)</h4>
<pre>
class ScreenB extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Screen B")),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.pop(context, "Hello from Screen B!");
          },
          child: Text("Go Back with Data"),
        ),
      ),
    );
  }
}
</pre>

<h3>3. How It Works</h3>
<ul>
  <li>Screen A navigates to Screen B using <code>Navigator.push()</code>.</li>
  <li>Screen B sends data back using <code>Navigator.pop(context, "Hello from Screen B!")</code>.</li>
  <li>Screen A receives the data using <code>await Navigator.push()</code> and updates the UI.</li>
</ul>

<h3>4. Conclusion</h3>
<p>This method allows passing any type of data, including strings, integers, and even model classes, without using any external components.</p>


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

<h2>Difference Between ChangeNotifier and ValueNotifier</h2>

<h2>1. ChangeNotifier</h2>
<ul>
    <li>A broader state management class that allows multiple listeners to subscribe.</li>
    <li>Requires calling <code>notifyListeners()</code> explicitly to inform listeners about state changes.</li>
    <li>Used when managing complex state with multiple properties.</li>
</ul>

<h3>Example:</h3>
<pre>
class CounterModel extends ChangeNotifier { 
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners(); // Notifies all listeners
  }
}
</pre>

<h3>Usage in UI:</h3>
<pre>
ChangeNotifierProvider(
  create: (context) => CounterModel(),
  child: Consumer&lt;CounterModel&gt;(
    builder: (context, counter, child) {
      return Text('${counter.count}');
    },
  ),
)
</pre>

<h2>2. ValueNotifier</h2>
<ul>
    <li>A lightweight alternative for managing a single value.</li>
    <li>Extends <code>ChangeNotifier</code> but optimizes for a single <code>value</code> property.</li>
    <li>Automatically notifies listeners when <code>value</code> changes, so no need to call <code>notifyListeners()</code>.</li>
</ul>

<h3>Example:</h3>
<pre>
ValueNotifier&lt;int&gt; counter = ValueNotifier&lt;int&gt;(0);

void increment() {
  counter.value++; // No need for notifyListeners()
}
</pre>

<h3>Usage in UI:</h3>
<pre>
ValueListenableBuilder&lt;int&gt;(
  valueListenable: counter,
  builder: (context, value, child) {
    return Text('$value');
  },
)
</pre>

<h2>Key Differences</h2>
<table border="1">
    <tr>
        <th>Feature</th>
        <th>ChangeNotifier</th>
        <th>ValueNotifier</th>
    </tr>
    <tr>
        <td>Notifies listeners</td>
        <td>Requires <code>notifyListeners()</code></td>
        <td>Automatically updates</td>
    </tr>
    <tr>
        <td>Ideal for</td>
        <td>Managing multiple state variables</td>
        <td>Managing a single value</td>
    </tr>
    <tr>
        <td>Performance</td>
        <td>Slightly heavier</td>
        <td>More lightweight</td>
    </tr>
    <tr>
        <td>Usage with Provider</td>
        <td><code>ChangeNotifierProvider</code></td>
        <td>Used with <code>ValueListenableBuilder</code></td>
    </tr>
</table>

<h2>When to Use What?</h2>
<ul>
    <li>Use <b>ChangeNotifier</b> when you have <i>multiple state variables</i> in a model.</li>
    <li>Use <b>ValueNotifier</b> when you need to track a <i>single value</i> with minimal overhead.</li>
</ul>

<h2>Provider in Flutter</h2>
<p><code>Provider</code> is a state management solution in Flutter that helps manage and propagate state across the widget tree efficiently. It allows widgets to listen to changes and rebuild when necessary.</p>

<h3>1. What is Class Provider?</h3>
<p><code>Provider</code> is a generic class that exposes an object to the widget tree. It helps manage state without requiring manual <code>setState()</code>.</p>

<h4>Example:</h4>
<pre>
<code>
class Counter extends ChangeNotifier {
  int count = 0;

  void increment() {
    count++;
    notifyListeners(); // Notifies listeners about changes
  }
}

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => Counter(),
      child: MyApp(),
    ),
  );
}
</code>
</pre>

<h3>2. What is MultiProvider?</h3>
<p><code>MultiProvider</code> allows multiple providers to be combined and passed down the widget tree. It helps avoid nesting multiple <code>Provider</code> widgets.</p>

<h4>Example:</h4>
<pre>
<code>
void main() {
  runApp(
    MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (context) => Counter()),
        Provider<String>(create: (context) => "Hello, Provider!"),
      ],
      child: MyApp(),
    ),
  );
}
</code>
</pre>
<p>This ensures both <code>Counter</code> and <code>String</code> data can be accessed anywhere in the app.</p>

<h3>3. What is Watch in Provider?</h3>
<p>The <code>.watch</code> method listens for changes in the provider and rebuilds the widget when the provider updates.</p>

<h4>Example:</h4>
<pre>
<code>
class Counter extends ChangeNotifier {
  int count = 0;

  void increment() {
    count++;
    notifyListeners();
  }
}

@override
Widget build(BuildContext context) {
  int count = context.watch&lt;Counter&gt;().count; // Watches for changes

  return Column(
    children: [
      Text("Count: " + count.toString()),
      ElevatedButton(
        onPressed: () => context.read&lt;Counter&gt;().increment(),
        child: Text("Increment"),
      ),
    ],
  );
}
</code>
</pre>
<p><strong><code>watch&lt;T&gt;()</code></strong> → Listens to provider changes and triggers a rebuild.</p>

<h3>4. What is Read in Provider?</h3>
<p>The <code>.read</code> method accesses the provider <strong>without listening</strong> for changes. It is useful when calling methods inside button clicks or event handlers.</p>

<h4>Example:</h4>
<pre>
<code>
@override
Widget build(BuildContext context) {
  return ElevatedButton(
    onPressed: () {
      context.read&lt;Counter&gt;().increment(); // Reads the provider without listening
    },
    child: Text("Increment"),
  );
}
</code>
</pre>
<p><strong><code>read&lt;T&gt;()</code></strong> → Reads the provider <strong>only once</strong>, does not rebuild the widget when the provider changes.</p>

<h3>Summary of Provider Methods</h3>
<table border="1">
<tr>
  <th>Method</th>
  <th>Usage</th>
  <th>Triggers Rebuild?</th>
</tr>
<tr>
  <td><code>watch&lt;T&gt;()</code></td>
  <td>Accesses and listens for changes</td>
  <td>✅ Yes</td>
</tr>
<tr>
  <td><code>read&lt;T&gt;()</code></td>
  <td>Accesses without listening</td>
  <td>❌ No</td>
</tr>
</table>

<h2>Using Consumer</h2>

<h3>When to use?</h3>
<ul>
    <li>When you want to rebuild only a specific widget instead of the entire widget tree.</li>
    <li>Useful when only a part of the widget depends on the provider.</li>
    <li>Helps optimize performance by minimizing unnecessary widget rebuilds.</li>
</ul>

<h3>Example:</h3>
<pre>
    <code>
    Consumer&lt;CounterProvider&gt;(
      builder: (context, provider, child) {
        return Text('Count: ${provider.count}');
      },
    );
    </code>
</pre>
<p>Here, only the Text widget rebuilds when count changes, not the entire widget tree.</p>

<h2>Using context.watch&lt;T&gt;()</h2>

<h3>When to use?</h3>
<ul>
    <li>When you are inside a build method and want to rebuild the entire widget when the provider updates.</li>
    <li>Should be used directly inside the build method.</li>
    <li>Avoid using watch inside initState or onPressed, as it causes rebuilds.</li>
</ul>

<h3>Example:</h3>
<pre>
    <code>
    @override
    Widget build(BuildContext context) {
      final counterProvider = context.watch&lt;CounterProvider&gt;();
      return Text('Count: ${counterProvider.count}');
    }
    </code>
</pre>
<p>Here, the entire widget rebuilds when count changes.</p>

<h2>When to Use What?</h2>
<table border="1">
    <tr>
        <th>Scenario</th>
        <th>Use Consumer</th>
        <th>Use watch</th>
    </tr>
    <tr>
        <td>Rebuild a specific widget only</td>
        <td>Yes</td>
        <td>No</td>
    </tr>
    <tr>
        <td>Rebuild the entire widget</td>
        <td>No</td>
        <td>Yes</td>
    </tr>
    <tr>
        <td>Inside build() method</td>
        <td>Not needed</td>
        <td>Yes</td>
    </tr>
    <tr>
        <td>Inside initState() or onPressed()</td>
        <td>No</td>
        <td>No (use read instead)</td>
    </tr>
</table>

<h2>Bonus: When to Use read?</h2>
<p>If you only want to access the provider without listening for updates, use read:</p>
<pre>
    <code>
    final counterProvider = context.read&lt;CounterProvider&gt;();
    counterProvider.increment(); // Does not rebuild the widget
    </code>
</pre>

<h2>Final Tip</h2>
<ul>
    <li>Use watch when the entire widget needs rebuilding.</li>
    <li>Use Consumer when only part of the widget should rebuild.</li>
    <li>Use read when you just need to access the provider without listening.</li>
</ul>

<h2>Platform Channels in Flutter</h2>

<p>Flutter’s UI runs on Dart, but sometimes we need to communicate with native Android (Kotlin) or iOS (Swift) code for device-specific features like battery info, sensors, or Bluetooth. <strong>Platform Channels</strong> make this possible.</p>

<h3>⚡ Types of Platform Channels</h3>

<ul>
  <li><strong>MethodChannel</strong> → Call a native method and get a response.</li>
  <ul>
    <li><strong>Example:</strong> Getting battery level from Android/iOS.</li>
    <li><strong>Example:</strong> Fetching the <strong>device model name</strong> (Perfect use case for <code>MethodChannel</code>).</li>
  </ul>
  <li><strong>EventChannel</strong> → Listen to a continuous stream of native events.</li>
  <ul>
    <li><strong>Example:</strong> Battery charging state updates.</li>
  </ul>
  <li><strong>BasicMessageChannel</strong> → Send and receive messages between Dart and native code.</li>
  <ul>
    <li><strong>Example:</strong> Sending/receiving simple data like JSON.</li>
  </ul>
</ul>

<h3>🛠 How It Works?</h3>

<ol>
  <li>Dart sends a request via a channel.</li>
  <li>Native code handles it (Android/iOS).</li>
  <li>Response is sent back to Dart.</li>
</ol>

<h3>📌 Example: Fetch Device Model Name using MethodChannel</h3>

<p>Since a <strong>device model does not change frequently</strong>, it is an ideal use case for <code>MethodChannel</code>.</p>

<h3>🚀 Why is this a perfect example for MethodChannel?</h3>

<ul>
  <li>✅ <strong>One-time request</strong> – The device model does not change frequently.</li>
  <li>✅ <strong>Native API required</strong> – This info comes from Android's <code>Build.MODEL</code>.</li>
  <li>✅ <strong>Instant response</strong> – No need for real-time updates.</li>
</ul>

<p>This is a <strong>classic use case</strong> where <code>MethodChannel</code> fits perfectly.</p>


<h1> Explain type of Streams in flutter ? </h1>

<h2>1. Single-Subscription Stream</h2>
<p><strong>Description:</strong> A <code>Stream</code> that can only be listened to once. This type of stream is generally used for data that is emitted once and not repeatedly (e.g., a result from a network request, or a file download).</p>
<p><strong>Use Case:</strong> For handling asynchronous events that occur once (e.g., data loading from an API, a one-time sensor reading).</p>
<pre>
<code>
Stream<int> fetchData() async* {
  await Future.delayed(Duration(seconds: 2));
  yield 42; // Emits a single value after 2 seconds
}

fetchData().listen((data) {
  print(data); // Output: 42
});
</code>
</pre>

<h2>2. Broadcast Stream</h2>
<p><strong>Description:</strong> A <code>BroadcastStream</code> can be listened to by multiple listeners. This allows multiple parts of the app to listen to the same stream of data simultaneously. It doesn't provide "backpressure" (i.e., listeners can join and leave the stream at any time).</p>
<p><strong>Use Case:</strong> For broadcasting events to multiple listeners or UI components. Commonly used in scenarios like UI updates, user input events, or when multiple widgets need to respond to the same event (e.g., button clicks or location updates).</p>
<pre>
<code>
Stream<int> timerStream = Stream<int>.periodic(Duration(seconds: 1), (x) => x);

// Multiple listeners
timerStream.listen((data) {
  print('Listener 1: $data');
});

timerStream.listen((data) {
  print('Listener 2: $data');
});
</code>
</pre>
<p>To create a <code>BroadcastStream</code>, you can use <code>.asBroadcastStream()</code>:</p>
<pre>
<code>
Stream<int> broadcastStream = fetchData().asBroadcastStream();
</code>
</pre>

<h2>3. Controller Streams (<code>StreamController</code>)</h2>
<p><strong>Description:</strong> A <code>StreamController</code> allows you to manually control the flow of events in a stream. You can add events to the stream, close it, and listen to it. <code>StreamController</code> can be used for both single-subscription and broadcast streams.</p>
<p><strong>Use Case:</strong> When you want to create a custom stream and manually add or manipulate data/events.</p>
<pre>
<code>
StreamController<int> controller = StreamController<int>();

// Adding data to the stream
controller.add(1);
controller.add(2);

// Listening to the stream
controller.stream.listen((data) {
  print(data); // Output: 1, then 2
});

// Closing the controller
controller.close();
</code>
</pre>
<p>You can specify whether the stream is single-subscription or broadcast when creating a <code>StreamController</code>. For a broadcast stream:</p>
<pre>
<code>
StreamController<int> controller = StreamController<int>.broadcast();
</code>
</pre>

<h2>4. Asynchronous Generators (<code>async*</code> streams)</h2>
<p><strong>Description:</strong> Streams can also be created using <code>async*</code> functions. These are streams where the values are lazily generated asynchronously using the <code>yield</code> keyword. You can use <code>async*</code> to create a stream of data that may be emitted over time.</p>
<p><strong>Use Case:</strong> When you want to generate values asynchronously, like periodic data or data streams from a device.</p>
<pre>
<code>
Stream<int> asyncStream() async* {
  yield 1;
  await Future.delayed(Duration(seconds: 1));
  yield 2;
  await Future.delayed(Duration(seconds: 1));
  yield 3;
}

asyncStream().listen((data) {
  print(data); // Output: 1, 2, 3 (with delays in between)
});
</code>
</pre>

<h2>5. Error Streams</h2>
<p><strong>Description:</strong> A stream can emit errors. The stream’s <code>onError</code> handler allows you to catch and handle errors asynchronously.</p>
<p><strong>Use Case:</strong> When you expect errors or failures while processing the stream (e.g., network failures, invalid data).</p>
<pre>
<code>
Stream<int> errorStream() async* {
  yield 1;
  yield 2;
  throw Exception('An error occurred!');
}

errorStream().listen(
  (data) {
    print(data);
  },
  onError: (error) {
    print('Error: $error');
  },
);
</code>
</pre>

<h2>6. Stream of <code>StreamSubscription</code></h2>
<p><strong>Description:</strong> A <code>StreamSubscription</code> allows you to manage the lifecycle of a stream (pause, resume, cancel). You can pause and resume a stream's data flow based on certain conditions.</p>
<p><strong>Use Case:</strong> When you need to control the flow of data, for example, pausing or canceling a stream based on some logic (like app lifecycle state).</p>
<pre>
<code>
Stream<int> stream = Stream<int>.periodic(Duration(seconds: 1), (x) => x);
StreamSubscription<int> subscription = stream.listen((data) {
  print(data); // Output: 0, 1, 2...
});

// Pause the stream after 3 seconds
Future.delayed(Duration(seconds: 3), () {
  subscription.pause();
});

// Resume the stream after 5 seconds
Future.delayed(Duration(seconds: 5), () {
  subscription.resume();
});

// Cancel the subscription after 10 seconds
Future.delayed(Duration(seconds: 10), () {
  subscription.cancel();
});
</code>
</pre>

<h2>Summary of Stream Types:</h2>
<ul>
    <li><strong>Single-Subscription Stream</strong>: Can only be listened to once.</li>
    <li><strong>Broadcast Stream</strong>: Can be listened to by multiple listeners simultaneously.</li>
    <li><strong>StreamController</strong>: Allows you to create and manage custom streams.</li>
    <li><strong>Asynchronous Generators (<code>async*</code>)</strong>: Streams that generate values lazily, using <code>yield</code>.</li>
    <li><strong>Error Streams</strong>: Streams that may emit errors that you can handle.</li>
    <li><strong>StreamSubscription</strong>: Allows you to control the flow of events in a stream (pause, resume, cancel).</li>
</ul>

<h2>Find Unused Widget in Flutter Widget Tree</h2>
<p>To find unused widgets in a Flutter project during the final build, there are a few approaches you can use:</p>

<h3>1. Using the <code>flutter analyze</code> Command</h3>
<p><strong>Description:</strong> The <code>flutter analyze</code> command helps to analyze your codebase and find potential issues like unused imports or code. While it won’t directly find unused widgets, it can help to identify unused code or imports which might include widgets that are no longer in use.</p>
<pre>
<code>
flutter analyze
</code>
</pre>
<p>This command will identify unused imports, which can indirectly help you find widgets that are not used.</p>

<h3>2. Manual Methods / IDE Tools</h3>
<p><strong>Visual Studio Code:</strong> In Visual Studio Code, unused imports, variables, and code are highlighted. It can help identify widgets that are not being used in the widget tree.</p>
<p><strong>Android Studio:</strong> Android Studio also provides built-in features to highlight unused code. You can easily spot areas in the widget tree where a widget may not be in use.</p>
<p>For <strong>unused widgets</strong> specifically, Flutter doesn’t provide an out-of-the-box tool to find widgets that are not being used in the widget tree.</p>

<h3>3. Run Widget Tree Inspection</h3>
<p>If you want to manually inspect your widget tree, you can:</p>
<ul>
    <li>Check for unused widget imports in your widget files.</li>
    <li>If a widget is defined but not used anywhere in the widget tree (i.e., not referenced in any other widgets), it might be unused.</li>
</ul>
<p>Look through the widget files and remove any widgets that aren’t being used. Ensure to check the hot reload behavior to make sure no errors occur when removing suspected unused widgets.</p>

<h3>4. Tree Shaking (Dead Code Elimination)</h3>
<p><strong>Description:</strong> Flutter's tree shaking process removes unused code, including unused widgets, during the final build for release mode.</p>
<p><strong>Use Case:</strong> Tree shaking works automatically when building for production, removing unused methods, variables, and widgets.</p>
<pre>
<code>
flutter build apk --release
</code>
</pre>

<h3>Example</h3>
<p>Here’s an example of how to check if a widget is unused:</p>
<pre>
<code>
// unused_widget.dart
class UnusedWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container();
  }
}

// main.dart
import 'unused_widget.dart'; // Check if this import is necessary

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: Text("Hello World"),
        ),
      ),
    );
  }
}
</code>
</pre>
<p>In this example:</p>
<ul>
    <li><strong>UnusedWidget</strong> is imported in <code>main.dart</code>, but it's not used anywhere in the widget tree.</li>
    <li>Running <code>flutter analyze</code> will help identify if this import is unused.</li>
</ul>

<h3>Automated Tool Approach</h3>
<p>There isn’t an official Flutter tool that directly highlights unused widgets, but you can use <strong>Flutter DevTools</strong> to inspect the UI and widget tree, which can help identify areas that are not in use.</p>

<h3>Conclusion</h3>
<ul>
    <li>Use the <code>flutter analyze</code> command to find unused imports and general code issues.</li>
    <li>Leverage IDE tools like <strong>Visual Studio Code</strong> or <strong>Android Studio</strong> for easier navigation and identification of unused code.</li>
    <li>Flutter's <strong>tree shaking</strong> process automatically removes unused code, including unused widgets, during release builds.</li>
</ul>

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

<h2>How to Register Multiple Providers</h2>

<p>You can register multiple providers in Flutter using <strong>MultiProvider</strong>. This allows managing different pieces of state efficiently.</p>

<h3>1️⃣ Using MultiProvider (Global Providers)</h3>

<pre><code>
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (context) => CounterProvider()),
        ChangeNotifierProvider(create: (context) => ThemeProvider()),
      ],
      child: MyApp(),
    ),
  );
}
</code></pre>

<p><strong>MultiProvider</strong> efficiently wraps multiple providers.</p>

<h3>2️⃣ Accessing Multiple Providers in UI</h3>

<pre><code>
class CounterProvider extends ChangeNotifier {
  int _count = 0;
  int get count => _count;
  
  void increment() {
    _count++;
    notifyListeners();
  }
}

class ThemeProvider extends ChangeNotifier {
  bool _isDarkMode = false;
  bool get isDarkMode => _isDarkMode;

  void toggleTheme() {
    _isDarkMode = !_isDarkMode;
    notifyListeners();
  }
}
</code></pre>

<h3>Using Providers in UI</h3>

<pre><code>
class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var counterProvider = Provider.of&lt;CounterProvider&gt;(context);
    var themeProvider = Provider.of&lt;ThemeProvider&gt;(context);

    return Scaffold(
      appBar: AppBar(title: Text("MultiProvider Example")),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text("Counter: ${counterProvider.count}", style: TextStyle(fontSize: 20)),
            ElevatedButton(
              onPressed: () => counterProvider.increment(),
              child: Text("Increment Counter"),
            ),
            Switch(
              value: themeProvider.isDarkMode,
              onChanged: (value) => themeProvider.toggleTheme(),
            ),
            Text(themeProvider.isDarkMode ? "Dark Mode" : "Light Mode"),
          ],
        ),
      ),
    );
  }
}
</code></pre>

<h3>3️⃣ Local Providers (For Specific Widgets)</h3>

<pre><code>
@override
Widget build(BuildContext context) {
  return ChangeNotifierProvider(
    create: (context) => LocalProvider(),
    child: SomeWidget(),
  );
}
</code></pre>

<h3>✅ Summary</h3>

<p><strong>Multiple global providers:</strong> Use <strong>MultiProvider</strong> in main.dart.<br>
<strong>Local provider for a widget:</strong> Use <strong>ChangeNotifierProvider</strong> inside build().</p>


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


