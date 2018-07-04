# Unity-Managed-Update
Imporving performance by managing the Update() function in Unity.

I wrote a blog entry on performance optimization before. It focused on how code optimizations can enhance your performance by about 50 percent.You can check it out at www.itsKristin.me!

This tech demo goes a bit deeper and to do that you’ll first have to understand what Unity does under the hood. Unity utilizes a messaging system that lets you use a bunch of functions that will be called at specific events during runtime. Said functions are your basic Awake(),Start() and Update() for example.

The engine checks each MonoBehaviour for those functions and then adds them to lists according to the functions they entail. At runtime, Unity iterates through those lists and executes the methods from it one by one.

This does sound great, and obviously, it works – but there is room for improvement.

What are we aiming for?
We want to have some more options then what Unity gives us and more control over the functions we had to begin with.

How to do it?
First of all, we’ll have to extend MonoBehaviour with public virtual void functions for ManagedUpdate, ManagedFixedUpdate and ManagedLateUpdate (See the ManagedMonoBehaviour class on GitHub for reference.)  Next up we’ll need the UpdateManager.

The UpdateManager class holds an array for each type of Update call. It keeps track of all of them and sorts them into individual arrays for each kind of Update. At it’s own Update, FixedUpdate and LateUpdate it iterates through the arrays and calls their managed functions.

