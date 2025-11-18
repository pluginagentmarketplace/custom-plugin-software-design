---
name: mobile-platforms
description: Mobile development for iOS, Android, Flutter, React Native, and cross-platform solutions. Master native and cross-platform development, app distribution, and mobile best practices.
---

# Mobile Development Platforms

## Quick Start

Mobile development spans native platforms (iOS, Android) and cross-platform frameworks. Each approach has tradeoffs:

- **Native iOS** - Best performance, full platform access, Swift
- **Native Android** - Largest market, Kotlin, open ecosystem
- **Flutter** - Single codebase, excellent performance, Dart
- **React Native** - JavaScript code sharing, large community

## iOS Development (Swift)

```swift
import SwiftUI

// View Model (MVVM)
class UserViewModel: ObservableObject {
    @Published var users: [User] = []
    @Published var isLoading = false

    func fetchUsers() {
        isLoading = true
        Task {
            let url = URL(string: "https://api.example.com/users")!
            let (data, _) = try await URLSession.shared.data(from: url)
            let decoded = try JSONDecoder().decode([User].self, from: data)
            DispatchQueue.main.async {
                self.users = decoded
                self.isLoading = false
            }
        }
    }
}

// SwiftUI View
struct ContentView: View {
    @StateObject var viewModel = UserViewModel()

    var body: some View {
        NavigationView {
            ZStack {
                if viewModel.isLoading {
                    ProgressView()
                } else {
                    List(viewModel.users) { user in
                        NavigationLink(destination: UserDetailView(user: user)) {
                            VStack(alignment: .leading) {
                                Text(user.name)
                                    .font(.headline)
                                Text(user.email)
                                    .font(.caption)
                                    .foregroundColor(.gray)
                            }
                        }
                    }
                }
            }
            .navigationTitle("Users")
            .onAppear {
                viewModel.fetchUsers()
            }
        }
    }
}

// Model
struct User: Codable, Identifiable {
    let id: Int
    let name: String
    let email: String
}
```

## Android Development (Kotlin)

```kotlin
// ViewModel
class UserViewModel : ViewModel() {
    private val _users = MutableLiveData<List<User>>()
    val users: LiveData<List<User>> = _users

    fun fetchUsers() {
        viewModelScope.launch {
            try {
                val apiService = RetrofitClient.apiService
                val response = apiService.getUsers()
                _users.value = response
            } catch (e: Exception) {
                Log.e("UserViewModel", "Error fetching users", e)
            }
        }
    }
}

// Composable (Jetpack Compose)
@Composable
fun UserListScreen(viewModel: UserViewModel = viewModel()) {
    val users by viewModel.users.observeAsState(emptyList())

    LaunchedEffect(Unit) {
        viewModel.fetchUsers()
    }

    LazyColumn {
        items(users) { user ->
            UserItem(user)
        }
    }
}

@Composable
fun UserItem(user: User) {
    Surface(
        modifier = Modifier
            .fillMaxWidth()
            .padding(8.dp),
        color = Color.White
    ) {
        Column(modifier = Modifier.padding(16.dp)) {
            Text(user.name, style = MaterialTheme.typography.headlineSmall)
            Text(user.email, style = MaterialTheme.typography.bodySmall)
        }
    }
}
```

## Flutter Development

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

// ViewModel
class UserProvider with ChangeNotifier {
    List<User> _users = [];
    bool _isLoading = false;

    List<User> get users => _users;
    bool get isLoading => _isLoading;

    Future<void> fetchUsers() async {
        _isLoading = true;
        notifyListeners();

        try {
            final response = await http.get(
                Uri.parse('https://api.example.com/users')
            );

            if (response.statusCode == 200) {
                final jsonData = jsonDecode(response.body) as List;
                _users = jsonData
                    .map((item) => User.fromJson(item))
                    .toList();
            }
        } catch (e) {
            print('Error: $e');
        } finally {
            _isLoading = false;
            notifyListeners();
        }
    }
}

// UI Widget
class UserListScreen extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return ChangeNotifierProvider(
            create: (_) => UserProvider()..fetchUsers(),
            child: Scaffold(
                appBar: AppBar(title: const Text('Users')),
                body: Consumer<UserProvider>(
                    builder: (context, userProvider, _) {
                        if (userProvider.isLoading) {
                            return const Center(
                                child: CircularProgressIndicator()
                            );
                        }

                        return ListView.builder(
                            itemCount: userProvider.users.length,
                            itemBuilder: (context, index) {
                                final user = userProvider.users[index];
                                return ListTile(
                                    title: Text(user.name),
                                    subtitle: Text(user.email),
                                );
                            },
                        );
                    },
                ),
            ),
        );
    }
}
```

## React Native

```javascript
import React, { useState, useEffect } from 'react';
import { View, Text, FlatList, ActivityIndicator, StyleSheet } from 'react-native';

const UserListScreen = () => {
    const [users, setUsers] = useState([]);
    const [loading, setLoading] = useState(true);

    useEffect(() => {
        fetchUsers();
    }, []);

    const fetchUsers = async () => {
        try {
            const response = await fetch('https://api.example.com/users');
            const data = await response.json();
            setUsers(data);
        } catch (error) {
            console.error(error);
        } finally {
            setLoading(false);
        }
    };

    if (loading) {
        return (
            <View style={styles.container}>
                <ActivityIndicator size="large" color="#0000ff" />
            </View>
        );
    }

    return (
        <View style={styles.container}>
            <FlatList
                data={users}
                keyExtractor={(item) => item.id.toString()}
                renderItem={({ item }) => (
                    <View style={styles.userCard}>
                        <Text style={styles.name}>{item.name}</Text>
                        <Text style={styles.email}>{item.email}</Text>
                    </View>
                )}
            />
        </View>
    );
};

const styles = StyleSheet.create({
    container: {
        flex: 1,
        backgroundColor: '#f5f5f5',
    },
    userCard: {
        backgroundColor: 'white',
        padding: 16,
        marginHorizontal: 8,
        marginVertical: 4,
        borderRadius: 8,
    },
    name: {
        fontSize: 16,
        fontWeight: 'bold',
    },
    email: {
        fontSize: 14,
        color: '#666',
        marginTop: 4,
    },
});

export default UserListScreen;
```

## Mobile Best Practices

### Performance
- Lazy load images and data
- Use view recycling (ListView, LazyColumn)
- Minimize memory footprint
- Implement pagination for large lists
- Optimize database queries

### User Experience
- Responsive touch targets (48x48 dp minimum)
- Intuitive navigation
- Fast loading indicators
- Proper error handling and messaging
- Offline capability

### Security
- Encrypt sensitive data
- Use HTTPS for APIs
- Secure token storage
- Implement biometric authentication
- Validate user input

### Testing
```dart
// Flutter Testing
testWidgets('User list loads correctly', (WidgetTester tester) async {
    await tester.pumpWidget(MyApp());
    expect(find.text('Users'), findsOneWidget);
    await tester.pumpAndSettle();
    expect(find.byType(ListTile), findsWidgets);
});
```

## Platform Comparison

| Aspect | Native iOS | Native Android | Flutter | React Native |
|--------|-----------|----------------|---------|--------------|
| Language | Swift | Kotlin | Dart | JavaScript |
| Performance | Excellent | Excellent | Excellent | Good |
| Learning Curve | High | High | Medium | Medium |
| Code Sharing | No | No | Yes | Partial |
| Ecosystem | Mature | Mature | Growing | Large |
| Time to Market | Medium | Medium | Fast | Fast |

## Resources

- [Swift Official Docs](https://developer.apple.com/swift)
- [Android Official Docs](https://developer.android.com)
- [Flutter Official Docs](https://flutter.dev)
- [React Native Docs](https://reactnative.dev)

## Related Skills

- **Backend APIs** - Server integration
- **Databases** - Local and remote data
- **Testing** - Unit and UI testing
- **DevOps** - CI/CD for mobile
