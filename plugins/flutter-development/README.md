# Flutter Development Plugin

Specialized agents for Flutter and Dart development, covering mobile app development and code review workflows.

## Available Agents

### Code Review Agents

#### reviewer-flutter-app.md
Comprehensive code reviewer for Flutter application PRs. Analyzes Flutter/Dart code for best practices, performance, state management, and mobile-specific concerns.

**Use cases**:
- Automated Flutter PR reviews in CI/CD
- Widget architecture validation
- State management pattern enforcement
- Performance optimization analysis
- Flutter best practices compliance

**Review focus areas**:
- Widget composition and reusability
- State management (Provider, Riverpod, Bloc, etc.)
- Navigation and routing
- Performance and optimization
- Platform-specific considerations
- Accessibility
- Testing coverage

## Usage

### Installing Agents

```bash
# Install Flutter reviewer agent
./scripts/sync-agents.sh
# Select: reviewer-flutter-app
```

## Flutter Best Practices

The Flutter reviewer agent evaluates code based on:

### 1. Widget Architecture
- Proper widget composition
- StatelessWidget vs StatefulWidget usage
- Widget tree optimization
- Const constructors for performance

### 2. State Management
- Appropriate state management solution
- State scope and lifecycle
- Avoiding unnecessary rebuilds
- Proper use of keys

### 3. Code Quality
- Dart best practices and conventions
- Null safety
- Immutability where appropriate
- Error handling

### 4. Performance
- Build method optimization
- Lazy loading and pagination
- Image optimization
- Memory leak prevention

### 5. Testing
- Widget tests
- Integration tests
- Golden tests (screenshot testing)
- Test coverage

### 6. Platform Integration
- Native platform channels (if applicable)
- Platform-specific UI considerations
- Permissions handling
- Responsive design

## Code Review Criteria

Flutter reviewers evaluate PRs on:

1. **Architecture** (30%):
   - Widget organization
   - Separation of concerns
   - State management patterns

2. **Code Quality** (30%):
   - Dart conventions
   - Readability
   - Error handling
   - Null safety

3. **Performance** (20%):
   - Build efficiency
   - Resource management
   - Optimization techniques

4. **Testing** (20%):
   - Test coverage
   - Widget test quality
   - Integration tests

## Integration with Git Workflows

Flutter reviewer agents integrate with GitHub Actions:

```yaml
# .github/workflows/flutter-code-review.yml
- name: Review Flutter App PR
  uses: ./.github/actions/code-review
  with:
    agent: reviewer-flutter-app
```

See `git-workflows/flutter/` for complete workflow configurations.

## Future Agents

The Flutter plugin will expand to include:

- **flutter-dev**: Flutter development agent for building features
- **flutter-qa**: QA agent for Flutter testing strategies
- **flutter-performance**: Performance optimization specialist

## Organization

Flutter agents follow mobile development best practices:
- Widget-based architecture
- Responsive and adaptive design
- Platform-specific considerations
- Performance-first approach
- Comprehensive testing strategies
