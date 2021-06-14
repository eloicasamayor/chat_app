# chat_app
> *Learning Flutter: chapter VI*

This project was build following a [Flutter & Dart Course by Maximilian Schwarzmüller](https://www.udemy.com/course/learn-flutter-dart-to-build-ios-android-apps/). The main learning focus in this section is the integration with main **Firebase** services.

I've been writing some notes while building the app. Here they are.

# Setting Up Firebase Firestore
We use the cloud_firestore package to work with the Firestore Database and import it on the file:
```dart
import 'package:cloud_firestore/cloud_firestore.dart';
```
## Initialize the firestore instance
We must call Firebase.initializeApp() when app starts.
```dart
import 'package:firebase_core/firebase_core.dart';
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}
```
## Accessing firestore data
To reach a collection, access the firebase instance and run .collection() passing the path to the collection:
```dart
Firestore.instance.collection('collection_name/document_id/subcollection');
```
- To add a document we run .add() after the .collection()
- To get a specific document -> .document()
## Using Snapshots() stream
We can call **.snapshots()** to stablish the realtime connection with the firestore db.
It returns a stream, it means that it will emit new values whenever the data changes.
Then, with the **.listen()** we pass a function that gets every peace of data of the stream and will will be triggered on every change on the data.
```dart
Firestore.instance
    .collection('chats/9BZnekYwCzB30jDmpUVR/messages')
    .snapshots()
    .listen((data) {
        print(data.documents[0]['text']); 
        // we access the value for the 'text' key of the first document in messages collection.
    })
```
### Solving the DexArchiveMergeException bug
- We go to the build.gradle in the android/app folder 
- in defaultconfig we add "multiDexEnabled true"
- in dependencies we add "implementation 'com.android.support:multidex:1.0.3

## Using StreamBuilder()

> git push origin main