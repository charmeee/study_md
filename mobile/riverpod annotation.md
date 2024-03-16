

family
```dart
@riverpod 
Future<TMDBMovie> movie( MovieRef ref, { required int movieId, }) {
	return ref
		 .watch(moviesRepositoryProvider) 
		 .movie(movieId: movieId); 
}
```