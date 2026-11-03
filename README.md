# Mobile Architecture Playbook

A short read on how I approach mobile architecture, plus links to reference implementations in this profile.

## Principles

1. **One-way dependency rule, not just layer names.** Domain depends on nothing. Everything else depends on Domain. This is what actually makes business logic testable and portable — not whether you call it "Clean Architecture" or "MVVM."
2. **Match DI to the platform, not to a textbook.** Hilt is right for an Android app with ten+ ViewModels and framework-heavy dependencies (see android-clean-architecture-sample); manual, protocol-based DI is right for a smaller iOS app (see ios-clean-architecture-sample). Consistency for its own sake is a trap.
3. **Feature-based modularity over layer-based.** Package by feature (auth/, menu/, cart/...) so a feature can be owned end-to-end by one team, and keep shared code in a deliberately small core.
4. **Testability is a design decision, not an afterthought.** Repository interfaces live in Domain; fakes replace Room DAOs/network clients in tests without Robolectric or instrumentation.
5. **State flows one way, UI effects are explicit.** `StateFlow` for continuous UI state, a `Channel`-based one-shot event type for navigation/snackbars — never mix the two, or a config change replays an event that already fired.
6. **Decide what's out of scope on purpose.** Every reference repo below has a "Decisions & trade-offs" section stating what I left out and why — usually real networking, auth, and persistence, so the sample stays about architecture, not infrastructure.

## Selected work

- **android-clean-architecture-sample** — Clean Architecture on Android: Kotlin, Jetpack Compose, Hilt, Room, tested `CartRepository` via a fake DAO.
- **ios-clean-architecture-sample** — same architecture on iOS: Swift, SwiftUI, manual DI, Swift Testing.
- **flutter-modular-architecture** — feature-modular Flutter with flutter_bloc + get_it.
- **react-native-scalable-architecture** — scalable RN structure with TypeScript + Zustand.
- **mobile-bff-reference** — the backend-for-frontend these clients talk to, Kotlin + Spring Boot.
- **ml_kit** — on-device ML on Android (text/face/pose/barcode detection) via ML Kit + CameraX.
- **llm-agent-tutorials** — hands-on LangChain/LangGraph agent-building, a different kind of system design.

## Currently exploring

Kotlin Multiplatform for sharing business logic across iOS/Android.
