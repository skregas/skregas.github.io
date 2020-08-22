---
layout: post
title: "Becoming Flutter: Learning to float"
tags: [flutter, ui, mobile, learning, imports]
---

I started the Flutter journey several months ago, working on a card-swiping app, with the intention of mimicing a deck of cards I admire. The added benefit is learning a new language and bettering my UI dev skills.

I have been working through the Flutter resources put together by the London App Brewery (LAB). The content is clear and the instruction fun and lively. But this isn't a review of the course. I recently came across a book on React. In the forward, the author strongly encourages readers to teach what they are learning, through blogs, videos, live instruction, etc, because that's really how we learn something. Advice I'd heard in the past; this time it triggered action.

Starting here, I'm writing about, reflecting on, and teaching what I'm learning about Flutter development. I will use mostly my own project for examples, but may turn to the LAB projects for help and inspiration. Let's go.

---
As stated above, I've been working on this project for some months, so we're starting in the middle. The app mimics a card deck: swiping left and right scrolls through the deck. Tapping a card flips it, revealing the content on the other side. The front side, the side initially facing the user, is the back of the card showing an image. The fipped side shows a bit of text

Current state:
- the individual cards are displayed in a horizontal line
- swiping works
- flipping works: however every card is flipped when flipping the current card. The current card occupies the middle of the screen, displayed larger than the surrrounding cards.

Current goal:
- flip only the current card.

First, let's talk about imports. As with most modern programming language, Flutter comes along with a rich (and growing) ecosystem of plug-ins to make common tasks easier, letting the dev focus on the important core features of the app. I knew from other languages, devices and apps that I need not write my own cover flow type of functionality. Sure enough, a simple search on [pub.dev](https://pub.dev) reveals [simple_coverflow](https://pub.dev/packages/simple_coverflow).

Once you find a package that fits your needs, the first step
is adding the extension to `pubspec.yml`. This is bascially a configuration file that informs Flutter about certain aspects of your application. In the case of imports, adding a package reference tells Flutter it exists, you want to use it, and to download it on the next package refresh.
So, open `app/pubspec.yml`, and add the package reference in the `dependencies` section:

```

dependencies:
    simple_coverflow: ^0.0.8

```

The numbers after the package are version identifiers. Sometimes apps will require a specific version of a package to work properly; those numbers are what to look for. The '^' means: 'use a version greater than this'

Next step is importing the package into your program like so:

`import 'package:simple_coverflow/simple_coverflow.dart';`

Conventionaly, import statements like the one above are placed at the beginning of the file. This practice helps keep the code neat and tidy, readable for you six months from now, or others in the future.

Let's digest that statement. `import` is a Flutter keyword. That means it is reserved for internal language operations. Although you can use these words to define your own variables like `int import = 10`, it leads to confusion and bugs. Programming is challenging enough; you don't need to create more. Leave the Flutter keywords alone and use your creativity to come up with meaningful, clear, direct variable names.

Final step in getting your app to use the new package is to install it.
In Android Studio you will see a prompt, `Get new packages`. Click that, Flutter does its thing in the background, and your new package is ready to use! Another way to install new packages is on the command line. In your favorite terminal, navigate to the root directory or your project, and enter the following command:
`flutter pub get`. Take a breath, Flutter does its thing, and your package is ready to go.

Lather, rinse repeat for all the packages needed for your app.
For my app, I used simple_coverflow for the horizontal scrolling of the cards, and [flip_card](https://pub.dev/packages/flip_card#-installing-tab-) for handling the behavior of each individual card.

---

With the packages in place, I've built the first version of the app. Cover flows works with swipe. Tapping a card flips it, tapping once more flips it back. The current challenge: all the cards get flipped on a single touch. I wnat each card to flip independently of all other cards.

My thinking: each card needs to be its own object, setting and changing state independently of all other cardseach with their own separate state. This means a tap recieved by one card will not trigger any other card but the tapped card.

So I need to populate the cover flow container with discrete objects; one for each card I want to represent. The next LAB video lesson covers classes in more detail. Creating several instances of a Card class to add to the cover flow sounds like the way to go.
