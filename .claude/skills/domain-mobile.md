---
name: Mobile Development
domain: mobile
description: Patterns and best practices for cross-platform mobile development (Flutter, React Native, iOS/Swift, Android/Kotlin)
file_detection: ["*.dart", "*.swift", "*.kt", "*/android/*", "*/ios/*", "*/lib/*"]
---

## Patterns to Apply

### Navigation
- **Flutter**: Use named routes + `GoRouter` for type-safe navigation
- **React Native**: Stack/Tab navigators with deep linking support
- **iOS**: SwiftUI `NavigationStack` or UINavigationController delegation
- **Android**: Navigation Component with safe-args

### State Management
- **Flutter**: BLoC pattern with streams or Provider package for simplicity
- **React Native**: Redux or Context API with hooks
- **iOS**: Combine framework with @Published properties
- **Android**: ViewModel + LiveData or StateFlow with coroutines

### Offline-First
- Store critical data locally (SQLite/Realm for Flutter, AsyncStorage for React Native)
- Sync queue for pending operations
- Conflict resolution: last-write-wins or merge strategies
- Network status monitoring before operations

### Performance Optimization
- **Lists**: Use lazy loading, pagination, and virtualization (ListView.builder, FlatList with removeClippedSubviews)
- **Images**: Cache aggressively, downsample, use CDN with device-appropriate sizes
- **Animations**: Prefer GPU-accelerated transforms over layout changes
- **Startup**: Defer initialization, lazy-load plugins, measure app startup time

### Platform-Specific Patterns
- Handle safe areas and notches consistently
- Respect OS conventions: iOS back gesture, Android back button
- Use native dialogs and haptic feedback appropriately
- Test on actual devices for platform-specific quirks

### Native Integration
- Bridge native code carefully with error handling
- Version native libraries independently
- Use platform channels (Flutter) or modules (React Native) consistently
- Test native crashes don't crash the app layer

## Pitfalls to Avoid

- Memory leaks from unclosed streams/listeners (dispose pattern critical)
- Blocking main thread with sync operations or heavy computation
- Improper state restoration after app backgrounding/resuming
- Ignoring platform permissions—always check before accessing sensors/camera/files
- Over-engineering state management for simple apps
- Hardcoding colors/strings instead of using design tokens
- Skipping keyboard handling—test with various input scenarios
- Missing error boundaries and graceful degradation
- Shipping without performance profiling (use Android Profiler, Instruments, DevTools)

## Quality Checks

- [ ] Navigation handles deep links and app restoration after background
- [ ] All network operations have timeout, retry, and error handling
- [ ] Stream/listener disposal on dispose() or equivalent lifecycle
- [ ] Offline mode tested: app functions without network
- [ ] Build size optimized: no unnecessary assets, tree-shaken dependencies
- [ ] Performance: list scroll smooth, animations 60fps (90fps for high-refresh displays)
- [ ] Permissions requested before use, with fallback UX
- [ ] Image loading shows progress/skeleton, not blank white space
- [ ] Keyboard dismissal works predictably across all screens
- [ ] Platform-specific navigation gestures work (iOS back, Android back)
