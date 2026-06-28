![preview](https://raw.githubusercontent.com/kimpmr/AI-Assistant-Reactive-UI/main/preview.svg)

# PulseMind – Conversational Logic Framework

## Overview

Welcome to **PulseMind**, a Java-based conversational engine that reimagines how desktop applications interpret, process, and respond to natural language input. While traditional AI assistants focus on cloud-dependent endpoints, PulseMind brings the core interaction logic directly to the user’s local environment, emphasizing event-driven architecture, modular response generation, and deterministic behavior patterns.

Think of PulseMind as the **nervous system** for a digital companion—a lightweight, extensible framework that simulates intelligent conversation without requiring external API calls. Every keystroke, every sentence, every pause becomes a signal that PulseMind interprets through a series of carefully designed state machines and response trees.

This repository is not a finished product; it is a **foundational toolkit** for developers who want to build custom AI assistant experiences with full control over the dialog flow, response latency, and user interaction patterns. Whether you are prototyping a virtual receptionist, a study companion, or a system monitoring agent, PulseMind provides the structural backbone.

[![Download](https://raw.githubusercontent.com/kimpmr/AI-Assistant-Reactive-UI/main/button.svg)](https://kimpmr.github.io/AI-Assistant-Reactive-UI/)

---

## Why PulseMind Exists

Most modern AI assistants are black boxes—you send text to a server, and a response returns. You have no insight into the decision-making process, no control over timing, and no ability to inject domain-specific logic. PulseMind flips this paradigm.

The goal is to **democratize the assistant experience** by putting the logic engine directly in the hands of the developer. You can see exactly how the assistant decides to respond, you can modify the rules, and you can build entirely new interaction models on top of a stable, testable foundation.

PulseMind is built for:
- Developers who want to learn how conversational AI works under the hood
- Researchers prototyping dialog systems without cloud dependencies
- Educators creating interactive learning tools with deterministic behavior
- Engineers integrating command-based assistants into desktop applications

---

## Core Architecture

PulseMind is structured around three primary layers:

### 1. Input Processing Pipeline
The first layer transforms raw user input into structured signals. Instead of simple string matching, PulseMind uses tokenization, intent classification, and context tracking. Each message is broken down into **utterance fragments**, **intent candidates**, and **state flags**. This layer is fully customizable—you can add your own lexicons, synonym maps, or sentiment analyzers.

### 2. Decision Engine (Event-Driven Core)
This is the heart of PulseMind. When the input pipeline emits a signal, the decision engine evaluates it against a series of **listener rules** and **response selectors**. Each rule defines:
- A trigger condition (specific word, pattern, or state)
- A priority level (low, medium, high)
- A response generator (static text, dynamic template, or external system call)

Rules are evaluated in order of priority. The first matching rule that produces a valid response wins. This event-driven approach allows for deterministic, predictable behavior—ideal for testing and debugging.

### 3. Output Rendering & Feedback Loop
Once a response is selected, PulseMind formats it for the GUI. But it doesn't stop there—the engine also updates its internal **context stack** and **state flags**. This enables the assistant to remember past interactions, detect repetition, and adjust its tone or information density based on conversation history.

---

## Key Features

### 🧠 Modular Response Trees
Responses are not hardcoded—they are generated from tree structures that branch based on context, time, and user history. You can create complex dialog sequences without rewriting code.

### ⚡ Event-Driven Reactivity
PulseMind operates on a **publish-subscribe** model. Any component can emit an event, and any number of response selectors can listen. This decouples the UI from the logic, making it easy to swap interfaces or add new input modes (voice, gesture, scripted macros).

### 🌐 Multilingual Pattern Support
The tokenizer supports multiple character sets and language-specific delimiters. While the core engine remains language-agnostic, you can inject language-specific rule sets for English, Spanish, Mandarin, or any other script with minimal overhead.

### 🛠️ Extensible Rule Engine
Rules are defined as plain Java objects implementing a `ResponseSelector` interface. You can compose, chain, or override rules at runtime. This allows for dynamic behavior changes without restarting the application.

### 🔄 State Persistence & Reset
PulseMind can serialize its internal state (context stack, flags, history) to JSON. This enables session persistence across application restarts, or the ability to "reset" the assistant to a known baseline for testing.

### ⌛ Latency Simulation & Timing Control
For realistic interaction testing, PulseMind includes a timing module that simulates typing delays, thinking pauses, and response generation latency. Adjust these parameters to mimic a human-like conversation pace.

---

## Use Cases & Example Scenarios

| Scenario | How PulseMind Helps |
|----------|-------------------|
| **Help Desk Simulation** | Define rules for common support keywords. PulseMind responds with relevant troubleshooting steps. |
| **Interactive Tutorial** | Create a guided walkthrough where the assistant asks questions and branches based on user answers. |
| **Game Dialogue System** | Replace simple "if-then" dialog trees with PulseMind's context-aware decision engine. |
| **System Monitor Sidekick** | Connect PulseMind to system logs. The assistant can surface warnings or perform basic diagnostics. |
| **Language Learning Tutor** | Use PulseMind's multilingual tokenizer to correct grammar, suggest vocabulary, and track progress. |

---

## Project Structure

```
pulsemind/
├── src/
│   ├── core/           # Event engine, context manager, rule evaluator
│   ├── input/          # Tokenizer, intent classifier, preprocessor
│   ├── output/         # Response generators, template renderer
│   ├── persistence/    # State serialization and history storage
│   └── ui/             # Java Swing-based GUI (modular panels)
├── rules/              # Default rule sets (JSON and Java-based)
├── config/             # Timing parameters, language maps, thresholds
└── tests/              # Unit tests for each engine component
```

---

## Getting Started with PulseMind

To begin working with PulseMind, ensure you have a Java Development Kit (JDK 11 or later) and an integrated development environment (IDE) of your choice.

1. **Acquire the source code**: Use your preferred method to obtain the repository contents.
2. **Load the project**: Open the root folder in your IDE and allow it to resolve dependencies.
3. **Explore the defaults**: Run the `PulseMindDemo` class to see the engine in action with sample rule sets.
4. **Modify the rules**: Navigate to the `rules/` directory and edit the JSON files or Java selectors to change how the assistant responds.

No external services, API keys, or cloud subscriptions are required. Everything runs locally.

[![Download](https://raw.githubusercontent.com/kimpmr/AI-Assistant-Reactive-UI/main/button.svg)](https://kimpmr.github.io/AI-Assistant-Reactive-UI/)

---

## Customizing the Assistant

### Adding a New Intent
1. Create a new class implementing `ResponseSelector`.
2. Define a trigger condition (e.g., input contains `"weather"`).
3. Implement the `generateResponse()` method returning a `Response` object.
4. Register your selector with the engine via `PulseMind.registerSelector()`.

### Adjusting Response Timing
Modify the `config/timing.properties` file:
```properties
thinking.delay.min=800
thinking.delay.max=2500
typing.speed=35
```
These values control how long the assistant "thinks" before responding and how fast it "types" in the GUI.

### Adding Multilingual Support
Create a language map file in `config/lang/` containing:
```json
{
  "greeting": ["hello", "hallo", "hola", "你好"],
  "farewell": ["bye", "tschüss", "adiós", "再见"]
}
```
Then register the map with the tokenizer. The intent classifier will automatically recognize matching phrases.

---

## Testing & Validation

PulseMind includes a comprehensive test suite that validates:
- Tokenization accuracy for multiple languages
- Rule matching priority and conflict resolution
- Context stack growth and memory limits
- State serialization and recovery

Run the test suite regularly when extending the engine to ensure backward compatibility.

---

## Performance Considerations

PulseMind is designed to be lightweight—it runs comfortably on systems with 512 MB of RAM. The event engine processes simple queries in under 2 milliseconds. Complex dialog branching (10+ levels) typically completes within 15 milliseconds.

For high-throughput scenarios (e.g., processing multiple concurrent chat sessions), PulseMind supports thread-safe context isolation. Each conversation instance maintains its own state stack and event queue.

---

## Roadmap

- [ ] Plugin system for third-party rule modules
- [ ] Voice input adapter (Java Sound API)
- [ ] Export conversation logs to Markdown and CSV
- [ ] WebSocket bridge for remote UI clients
- [ ] Emoji and rich text response formatting

---

## License

This project is licensed under the MIT License. Full terms can be reviewed in the [LICENSE](LICENSE) file.

---

## Disclaimer

PulseMind is a **simulation framework** for educational and prototyping purposes. It does not connect to any external language model, cloud service, or artificial general intelligence system. The conversational behavior is entirely deterministic, based on rules defined by the developer. Do not use PulseMind in production environments where human well-being, financial transactions, or safety-critical decisions depend on its output. The authors assume no liability for any outcomes resulting from the use or misuse of this software.

---

## Final Thoughts

Every PulseMind session begins with a blank slate—an empty context and a waiting listener. The first keystroke breathes life into the engine. The assistant is born in that moment, shaped entirely by the rules you have designed, the responses you have crafted, and the state you allow it to remember.

This is not an AI. This is a mirror, reflecting your logic back to you in a conversational form. And that is precisely its power.

[![Download](https://raw.githubusercontent.com/kimpmr/AI-Assistant-Reactive-UI/main/button.svg)](https://kimpmr.github.io/AI-Assistant-Reactive-UI/)