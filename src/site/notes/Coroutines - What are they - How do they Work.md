---
{"dg-publish":true,"permalink":"/coroutines-what-are-they-how-do-they-work/","title":"Coroutines: What are they? How do they work?","created":"2025-11-01T12:15:21.862-04:00"}
---

I am super excited for today’s article because we are going to dive into one of my favorite topics in Unity: Coroutines! In this article, we won’t go too in depth as I want to keep this consumable for beginners, but I will _very likely_ dive deeper into Coroutines and how they work under the hood in a future article because I just find them so fun!

We’ll use Coroutines to spawn our enemies infinitely in our game!
![coroutine_basics_01.gif](/img/user/images/coroutine_basics_01.gif)

First, lets create a new GameObject that we’ll call **Spawn_Manager** and create a new script for it called `SpawnManager`. Be sure to add the newly created component to your **Spawn_Manager** game object:
![Pasted image 20251101121751.png](/img/user/images/Pasted%20image%2020251101121751.png)
Before we get into code, I want to explain a couple of basic concepts here. First of all, what is a Coroutine?
### Coroutine
A Coroutine is essentially a block of code that gets run over multiple frames in your game. Traditionally when you write code, it will run from top to bottom until it is finished executing and any other code after it will have to wait until it’s finished. Often times, we want code to run over the course of, say, a few seconds before we make something happen while also letting the next block of code run like normal. We achieve this by using Coroutines in Unity.

Let’s go to our `SpawnManager` script and I’ll show you what a basic Coroutine looks like:
![Pasted image 20251101121814.png](/img/user/images/Pasted%20image%2020251101121814.png)
So we have a method that we are calling `CO_SpawnRoutine()`, eventually we’ll use this method to spawn our enemies at a specific interval. Something to note is that I like to prefix my coroutines with `CO_`to denote that it’s a Coroutine. You’ll notice a few things about this special-looking method.

The first thing is this weird `IEnumerator` that we are adding to our method signature instead of `void` which we are used to. What this basically means is that our method returns an object of type `IEnumerator` but for our purposes and to keep things simple, assume that methods with `IEnumerator` as their return types are Coroutines. We need that so that Unity knows we want to use a Coroutine.

The next weird thing is this `yield return` line. The `yield` keyword is a C# keyword that you must use whenever you are writing a method that returns an `IEnumerator`. This tells the compiler to let code run after this method is called once it hits the `yield` part of the method’s execution. Its a little tricky to understand, so I wouldn’t let yourself get too caught up with it. For now, just know that the `yield return new WaitForSeconds(5);` line does just what you’d expect. It waits 5 seconds before going on to the next line which is our print statement that says “5 seconds have passed!”.

Finally in our Start method, we have the `StartCoroutine()` method, and in it we pass in our coroutine method. In Unity, you have to tell the engine when you want to run a Coroutine. In this case, we will run it at the start of the game. If we run this then “5 seconds have passed!” will get printed in the console after 5 seconds:
![coroutine_basics_02.gif](/img/user/images/coroutine_basics_02.gif)
Go ahead and give this a try on your project. Make sure that it works!

Now this is useful because we can use something like this to spawn enemies every 5 seconds in our game (or maybe every 3 seconds, or every 10 seconds). I’ll show you how to do this very simply.

Firstly I want a prefab in our `SpawnManager` script so that we can `Instantiate` the prefab as many times as we want within this script!
![Pasted image 20251101121929.png](/img/user/images/Pasted%20image%2020251101121929.png)

Make sure to drag and drop the prefab into the **SpawnManager’s** inspector panel:
![coroutine_basics_03.gif](/img/user/images/coroutine_basics_03.gif)

And now let’s write the logic we’ll need to spawn enemies infinitely:
![Pasted image 20251101122015.png](/img/user/images/Pasted%20image%2020251101122015.png)With this code, a new enemy will spawn every 5 seconds. We create a while loop and set the conditions to the while loop to be true by default, because we want this coroutine to run forever, and since we are Starting the Coroutine in our Start method, it will start from the beginning and go on until the game is over.

Once we have that done, we just write logic to Instantiate the `enemyPrefab` after 5 seconds that we wait in `yield return new WaitForSeconds(5);`. With that, we have a working **SpawnManager** in our game!
![coroutine_basics_04.gif](/img/user/images/coroutine_basics_04.gif)
There we go! We have a working Coroutine in our game! At some point, I’d like to dive deeper into coroutines as I did omit some details in the interest of keeping things simple for beginners. Coroutines are a bit more of an advanced topic, but they are so useful even for beginners I feel the need to explain at least the basic use case for them. At some point, I’ll dive deeper into this cool Unity feature in another article! Stay tuned for that! Good luck!