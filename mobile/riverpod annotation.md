

family
```dart
@riverpod 
Future<TMDBMovie> movie( MovieRef ref, { required int movieId, }) {
	return ref
		 .watch(moviesRepositoryProvider) 
		 .movie(movieId: movieId); 
}
```

notifiyprovider
https://codewithandrea.com/articles/flutter-riverpod-async-notifier/

notifiyprovider and test
https://q.agency/blog/migrating-from-statenotifier-to-notifier-in-riverpod-2-0-with-unit-tests/