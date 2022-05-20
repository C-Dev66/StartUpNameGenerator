<img src="https://github.com/C-Dev66/StartUpNameGenerator/blob/main/screenshots/StartUpNameGeneratorReview.png" alt="HomePage"/>

# StartUpNameGenerator
> This multi-platform application(Andoird, iOS, Web) creates a simple app that generates proposed names for a startup company. The user can select and unselect names, saving the best ones. The code lazily generates 10 names at a time. As the user scrolls, more names are generated. There is no limit to how far a user can scroll.
---

### Table of Contents:

- [Description](#description)
- [Code Snippets](#code-snippets)
- [Summary](#summary)
- [Demo](#demo)

---

## Description

Application is built with Google's Flutter framework.

Flutter is Google's UI toolkit for building beautiful, natively compiled applications for mobile, web, and desktop from a single codebase. Flutter works with existing code, is used by developers and organizations around the world, and is free and open source



## What we will be covering
- **Part 1**
	- Structure of a Flutter app
	- Finding and using packages to extend functionality
	- Practice using hot reload for quicker development cycle
	- How to implement a stateful widget
	- how to create an infinate, lazily loaded list
- **Part 2**
	- How to add interactivity to a stateful widget
	- How to create and navigate to a second screen
	- How to change the look of an app using themes

---

## Code Snippets

> Setting up the application
```
// Creating the project

flutter create startup_namer
cd startup_namer

// Set up dependencies

flutter pub add english_words
```

> Configure the start of the application 
```dart
import 'package:english_words/english_words.dart';
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Startup Name Generator'
...
class RandomWords extends StatefulWidget {
  const RandomWords({Key? key}) : super(key: key);

  @override
  State<RandomWords> createState() => _RandomWordsState();
}
...
class _RandomWordsState extends State<RandomWords> {
  final _suggestions = <WordPair>[];
  final _biggerFont = const TextStyle(fontSize: 18.0);
  final _saved = <WordPair>{}; //NEW

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: const Text('Startup Name Generator')
...
```

> Create an infinate scrolling ListView
```dart
        body: ListView.builder(
            padding: const EdgeInsets.all(16.0),
            itemBuilder: /*1*/ (context, i) {
              if (i.isOdd) return const Divider(); /*2*/

              final index = i ~/ 2; /*3*/
              if (index >= _suggestions.length) {
                _suggestions.addAll(generateWordPairs().take(10)); /*4*/
              }
...

```

> Add interactivity & navigating to the new screen
```dart
                  trailing: Icon(
                    alreadySaved ? Icons.favorite : Icons.favorite_border,
                    color: alreadySaved ? Colors.red : null,
                    semanticLabel: alreadySaved ? 'Remove from saved' : 'Save',
                  ),
                  onTap: () {
                    setState(() {
                      if (alreadySaved) {
                        _saved.remove(_suggestions[index]);
                      } else {
                        _saved.add(_suggestions[index]);
                      }
...
    void _pushSaved(){
      Navigator.of(context).push(
        MaterialPageRoute<void>(
          builder: (context) {
            final tiles = _saved.map(
              (pair) {
                return ListTile(
                  title: Text(
                    pair.asPascalCase,
                    style: _biggerFont,
...
            return Scaffold(
              appBar: AppBar(
                title: const Text('Saved Suggestions'),
...
```

>Adding a theme
```dart
      theme: ThemeData(
        appBarTheme: const AppBarTheme(
          backgroundColor: Colors.white,
          foregroundColor: Colors.black,
```

---

## Summary
Building this application introduced me to the powerful idea of interactivity. An static application can feel out of grasp to the standard user. However, applying ways to touch and play with the different flow allows for a more immersed experience. Giving the user a whole new way of navigating the app. A powerful tool to keep in someones arsenal. This project serves as a baseline to think how we can make the user feel at home. Not too diffucult but simple enough to grasp at a quick pace.

For more information refer to the official documentation.

- [Flutter Documentation](https://docs.flutter.dev/)
- [Firebase Documentation](https://firebase.google.com/docs)
- [Flutterfire](https://firebase.google.com/docs/flutter/setup?platform=ios)
- [Google's awesome Flutter Youtube channel, Lots of great content here](https://www.youtube.com/channel/UCwXdFgeE9KYzlDdR7TG9cMw)

---

## Demo
![HomePage Gif](https://github.com/C-Dev66/StartUpNameGenerator/blob/main/screenshots/StartUpNameGeneratorGIF.gif)

