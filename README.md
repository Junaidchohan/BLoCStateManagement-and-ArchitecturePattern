# Flutter Bloc vs Cubit – Counter State Management Example

This repository demonstrates **Flutter state management using both Cubit and Bloc** with a simple counter example.

The purpose of this project is to clearly explain:
- How **Cubit** works
- How **Bloc** works
- The **architectural difference** between them
- When to use Cubit vs Bloc in real projects

## 📂 Project Structure

lib/
├── cubit/
│ └── counter_cubit.dart
├── bloc/
│ ├── counter_bloc.dart
│ └── counter_events.dart
├── ui/
│ ├── home_page.dart
│ └── inc_dec_page.dart
└── main.dart

## 🔹 CounterCubit (Function-based State Management)

### Implementation
```code
class CounterCubit extends Cubit<int> {
  CounterCubit() : super(0);

  void increment() {
    emit(state + 1);
  }

  void decrement() {
    if (state == 0) return;
    emit(state - 1);
  }
}


How Cubit Works
UI directly calls a function
That function emits a new state
No events are involved
emit() is accessible inside all Cubit methods

Characteristics
Minimal boilerplate
Easy to read and maintain
Ideal for simple to medium complexity logic
Faster development

🔹 CounterBloc (Event-driven State Management)
Bloc Implementation
dart
Copy code
class CounterBloc extends Bloc<CounterEvent, int> {
  CounterBloc() : super(0) {
    on<CounterIncremented>((event, emit) {
      emit(state + 1);
    });

    on<CounterDecremented>((event, emit) {
      if (state == 0) return;
      emit(state - 1);
    });
  }
}
Event Definitions
sealed class CounterEvent {}

class CounterIncremented extends CounterEvent {}
class CounterDecremented extends CounterEvent {}
How Bloc Works
UI dispatches an event
Bloc listens to the event
Business logic is handled inside event handlers
State is emitted from the handler only

Characteristics
Strict separation of concerns
Better for complex business logic
Highly scalable
More boilerplate than Cubit

⚠️ Important Architectural Difference
Cubit
State changes happen via method calls
emit() is available inside all methods
Bloc
State changes happen via events
emit() is only available inside event handlers
UI cannot directly change state

🔍 Internal Insight
Both Cubit and Bloc extend BlocBase, meaning:
They share the same core public API
Both expose state and stream
The difference is architectural, not technical
Bloc is essentially Cubit with an additional event layer.

📊 Cubit vs Bloc Comparison
Feature	Cubit	Bloc
Trigger	Function call	Event dispatch
Boilerplate	Low	High
emit() scope	All methods	Event handlers only
Learning curve	Easy	Moderate
Best for	Simple logic	Complex workflows

✅ When to Use Cubit
Simple UI state
Counters, toggles, form state
Rapid development
Fewer moving parts

✅ When to Use Bloc
Complex business rules
Multiple events affecting the same state
Enterprise-level applications
Strong architecture enforcement

🚀 Purpose of This Repository
Learn Flutter Bloc internals
Compare Cubit and Bloc side by side
Apply clean architecture principles
Serve as a reference for real projects

🧠 Final Thought
Choose Cubit for simplicity and Bloc for structure.
Both are powerful when used correctly.

## Final instruction to you
Commit with:
git add .
git commit -m "Add CounterCubit and CounterBloc examples to demonstrate Cubit vs Bloc state management"
git push origin main

This README is **portfolio-safe**.  
If you want, next we can:
- Add unit tests
- Add architecture diagram
- Convert this into a reusable template repo
