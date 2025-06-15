# Getting Started

Requisites
----------

*   Visual Studio
*   Basic knowledge of C#
*   Having SRML already installed

In the case you havent downloaded Visual Studio, you should follow this [wonderful tutorial](https://www.guru99.com/download-install-visual-studio.html) (choose the community option, that‘s the free one)

  

For learning basic knowledge of C#, you can look at this excellent playlist from [Brackeys](https://youtube.com/playlist?list=PLPV2KyIb3jR4CtEelGPsmPzlvP7ISPYzR).

If you won‘t have the requisites, don‘t expect me explaining it to you.

  

To get SRML, go on it‘s [NexusMods‘ page](https://www.nexusmods.com/slimerancher/mods/2) and follow the instructions there. You can also follow some tutorials on youtube about it.

  

  

**Honorable Mentions**
------------------

*   mikel veesus heir: many images that I don‘t write below „credited by X“ are from mikel‘s own wiki. Also of course his SRML, without it, we would need other ways to mod.
*   MrPurple/CabbageCrow: for the assembly publicizer (I think I should mention the creator of the program)

  

**Introduction**
------------

Now, let‘s gather up some energy, because this first tutorial will be a long and a bit complicated one. We‘re going to install a lot of stuff, so no codding at this point. Also, because I only have Windows, this is a tutorial for Windows users (yet). Because First step: Let‘s start a project!

  

  

**Setting up the project**
----------------------

I assume you‘ve already installed Visual Studio (read the requisites) then set up a project in there. Now, you can use any other IDE if you have one, like JetBrain‘s Rider IDE, but VisualStudio is the only one I know that‘s free and can do what we need for modding. (So yea, this whole tutorial is basically about visual studio).

  

  

**How to set up a new project in Visual Studio**
--------------------------------------------

After finally installing VisualStudio, together with C#, we now need to start a project! Select a **.NET Framework Class Library for C#** Project.

  

![](https://t24465758.p.clickup-attachments.com/t24465758/60fa5fd8-e7cf-4c25-b1e2-ea1a3644d5cf/IMG_0607.png)

_(Credits to_ [_veesus mikel heir_](https://github.com/veesusmikelheir) _for the image__)_

  

After clicking to `Next`, we‘ll land to the `Configure your new Project`, page.

  

![](https://t24465758.p.clickup-attachments.com/t24465758/56df5ed5-ba36-4809-922c-17d66be3b8ed/308053E7-5689-401D-8A4A-4A1688EADA1A.png)

_(Credits to_ [_veesus mikel heir_](https://github.com/veesusmikelheir) _for the image__)_

  

Here, we can set our:

*   project‘s name (pretty self-explanatory)
*   the location (only touch it if you want to have the project on a special folder, else leave this setting)
*   the solution‘s name (the \[NAME\_OF\_MOD\].dll file you download and use for playing the mods, here it‘s the name of that .dll file)

You can change the project‘s name and the solution‘s name, but I suggest you to only use this first mod to follow the content of this tutorial series. I‘m saying this so that you can concentrate about knowing the structure of a mod, before starting your private one, but feel free to do what you want, it‘s only a suggestion.

  

Anyways for this tutorial we‘re using the name „MyFirstMod“ for the Project and Solution.

  

  

**Adding the needed references**
----------------------------

Mentions: Because I can‘t take screenshots on my laptop, I‘m going to instead use the pictures of veesus (this is all WIP so I dont think I‘m actually going to show this to anyone, but if anyone sees this, atleast you‘re warned about screenshots not matching what I wrote until now).

  

After that, we need to setup the references we need in order to allow us to even start modding (and we make sure to use the publicized assemblies of SRML and Assembly-C).

In the solution explorer on the right side of the screen there‘s an option called References.

![](https://t24465758.p.clickup-attachments.com/t24465758/6a42ea7a-0977-46de-87af-7ceb7b7cacaa/77946113-0994-433D-9A18-7989ADBC5B9D.png)

  

After right clicking on this option, click the **Add Reference...** button

![](https://t24465758.p.clickup-attachments.com/t24465758/1a146bf8-de63-4d9a-8e50-f337f6afa9e8/FA671A47-A5C7-43FF-9A95-7195AA884A71.png)

  

Once getting on this menu, select the **Browse...** option in the bottom right corner

![](https://t24465758.p.clickup-attachments.com/t24465758/fbd1e84b-3ff3-4d78-b29a-3d416ac3ac6a/5BDE029F-B741-4CC0-942A-13CA04BE1E8C.png)

_(Credits to_ [_veesus mikel heir_](https://github.com/veesusmikelheir) _for the images__)_

The .dll references needed are located in the `<slime rancher game folder>/SlimeRancher_Data/Managed` folders as well as in `<slime rancher game folder>/SRML/Libs`, those include the: **Assembly-CSharp\_old.dll (NOT Assembly-CSharp-firstpass.dll or Assembly-CSharp.dll), SRML.dll, 0Harmony.dll** and any UnityEngine .dll files you'll need for your mod (We'll start with **UnityEngine.CoreModule.dll** for now).

  

  

![](https://t24465758.p.clickup-attachments.com/t24465758/dba6ab2b-2ad2-4194-8327-dd9f71e35a38/EA73E580-A8F3-459E-8611-1F3C3A958EE4.png)

  

![](https://t24465758.p.clickup-attachments.com/t24465758/f2cd26b6-39dc-4089-9eb9-0cf623fdfcec/F97FA33A-2179-48F1-B526-66626D6AA09B.png)

_(Credits to_ [_veesus mikel heir_](https://github.com/veesusmikelheir) _for the images__)_

  

See those .dll files? Those are the ones you want to use `MrPurple‘s AssemblyPublicizer` on. Use the AssemblyPublicizer and select the new .dll files, once done that click the `Add` button near the under right corner and you have your references!

  

  

**The `Main.cs`, `modinfo.json` files and Build events**
----------------------------------------------------

Time to set up the `Main.cs`, `modinfo.json` files and to add the build events. The `Main.cs` is going to be the mod‘s entry point, the `modinfo.json` is going to be the file that allows SRML to recognize your mod as a mod and we can use build events to speed up our working. More in details later on.

  

  

### **Building the .dll**

Lets start by build events. Everytime we‘re done codding our mod, we usually need to manually take the `MyFirstMod.dll` generated in `[YourRepository]/bin/Debug` (the name depends of what you‘ve chosen at the beginning, you‘ll find the SolutionsName.dll file there, in our case we‘ve written `MyFirstMod`).

  

First, we need to know 2 different paths: the path of your `MyFirstMod.dll` and the path of your **Mods** folder.

  

To get the first path, first you should build your project (do that every time you want to update your builded .dll file).

  

To do that, click on the **Build** tab at the top of the screen, then select **Build Solution**.

![](https://t24465758.p.clickup-attachments.com/t24465758/4467ce89-c0a6-47c1-8328-c9a0795f9d35/672CC595-1434-4236-8331-1171EB9B58C2.png)

If done correctly, and your code generates no error at building time, you should see **Build Succeeded** at the bottom of your screen.

  

![](https://t24465758.p.clickup-attachments.com/t24465758/c80d607a-42fa-4a92-b1a6-45e7f9547af8/349D9E13-2624-4064-9164-B324EDA3AAAF.png)

  

Finally, we can access the created `MyFirstMod.dll` file, by right clicking on the project, then selecting **Open Folder in File Explorer**.

![](https://t24465758.p.clickup-attachments.com/t24465758/fa8ecd8e-5818-4d37-8c5d-0483e060f118/22AE5959-F619-4DCF-B755-3045FE92BD7B.png)

  

Now naviguate to `/bin/Debug`. And there you should find your `MyFirstMod.dll` file. Now, you can just drag it to your **Mods** folder.

  

  

### **Main.cs**

Our first mod is almost ready to run! But there are still some steps to do. First we need to create an entry point for the mod to start execution at. SRML provides an abstract class to help us achieve this, it‘s called **ModEntryPoint** in the SRML namespace. Thanks to it, SRML will auto-detect a class extending ModEntryPoint and run the code found in certain methods inside it, those methods are **PreLoad, Load, and PostLoad**.

  

Important note: You usually should have a class called `Class1.cs`, we‘re going to rename it (F2) to our `Main.cs`.

#### **PreLoad**

![](https://t24465758.p.clickup-attachments.com/t24465758/c76890d3-d996-4dbd-8dd7-20843d654ec3/33DF3989-A3FA-49FA-8548-B3C300F3FFBF.jpeg)

Everything inside Preload will be executed before you enter your game (more about GameContext and SceneContext on a later chapter).

What you need to know for now is that the `HarmonyInstance.PatchAll();` is needed, if that isn‘t present in PreLoad (and it can only be present in Preload), then your whole mod wont probably work. More about HarmonyPatching in later chapters.

  

Also, if we want to register (aka make so that the game can recognise it) an object to the game, or add manually new enum values (the id of your object), then it‘s here that happens. If you don‘t get it, no worries, everything‘s going to be explained with some examples later on.

  

#### **Load**

![](https://t24465758.p.clickup-attachments.com/t24465758/3229c842-6589-4727-be76-16d22ab53d07/0043B34D-1E1D-4197-B7AD-D99105DEE82C.png)

Everything inside Load will be executed when the game starts. Here it‘s where most of registering stuff happen. For example, we write here when we‘re registering a slime, food, or etc.

  

#### **PostLoad**

![](https://t24465758.p.clickup-attachments.com/t24465758/2471b019-0480-419b-a2b1-8329d734172b/3DE68B67-DCF6-47FB-8060-4801994C5885.png)

Everything inside here will be executed after the game has already loaded. It‘s perfect to modify things that already exist in game, like a texture, color, and etc. But it‘s not a place to register new things, because at this point, the game has already loaded, and you can‘t add new things to the game if it‘s already loaded.

  

#### **The ModEntryPoint**

So, after having explored the 3 functions, now it‘s time to see how to use the ModEntryPoint abstract class.

  

```cs
using SRML;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

// Feel free to change the namespace to another name
namespace MyFirstMod
{
    public class Main : ModEntryPoint
    {
        // Called before GameContext.Awake
        // You want to register new things and enum values here, as well as do all your harmony patching
        public override void PreLoad()
        {
            HarmonyInstance.PatchAll();
        }


        // Called before GameContext.Start
        // Used for registering things that require a loaded gamecontext
        public override void Load()
        {

        }

        // Called after all mods Load's have been called
        // Used for editing existing assets in the game, not a registry step
        public override void PostLoad()
        {

        }

    }
}
```

  

### **modinfo.json**

Now, the last thing to set up is the modinfo.json file. It‘s needed to SRML to recognise the mod at all.

  

First, start by creating an text file, and rename it to `modinfo.json`.

![](https://t24465758.p.clickup-attachments.com/t24465758/fff6d45d-a165-414d-bac0-f8a6571408fc/4BABD600-B2E7-46A3-A8E3-D3CAA91A7D48.png)

  

![](https://t24465758.p.clickup-attachments.com/t24465758/42c4a881-4471-4953-86ae-8fc18be41537/52DB675F-6057-475C-AF4F-A02C5967C992.png)

  

Now, write this in the file (it‘s a template, so feel free to copy it):

```json
{
  "id": "myfirstmod",
  "name": "My First Mod", 
  "author": "frostdracony", 
  "description": "This is the first mod I have ever made!", 
  "version":  "1.0" 
}
```

  

Now, after saving it, select the file in your solution explorer. We can find lots of information about the file at the bottom of the solution explorer, included an option that reads, **Build Action**. By clicking on it and selecting **Embedded Resource**. This will make the C# compiler include your modinfo.json in your mods final .dll, thus allowing it to be recognized by SRML.

![](https://t24465758.p.clickup-attachments.com/t24465758/a9fde4d5-5558-41e5-bce2-bbc97130ee7a/3FA60380-A785-4670-8058-694879C58E82.png)

**Building and testing**
--------------------

Now that we have our Main.cs and modinfo.json files, it's time to build and test your mod! To build a project in visual studio, click on the **Build** tab at the top of the screen and select **Build Solution.**

  

![](https://t24465758.p.clickup-attachments.com/t24465758/4467ce89-c0a6-47c1-8328-c9a0795f9d35/672CC595-1434-4236-8331-1171EB9B58C2.png)

  

If done correctly, and your code generates no error at building time, you should see **Build Succeeded** at the bottom of your screen.

  

![](https://t24465758.p.clickup-attachments.com/t24465758/c80d607a-42fa-4a92-b1a6-45e7f9547af8/349D9E13-2624-4064-9164-B324EDA3AAAF.png)

  

Finally, we can access the created `MyFirstMod.dll` file, by right clicking on the project, then selecting **Open Folder in File Explorer**.

![](https://t24465758.p.clickup-attachments.com/t24465758/fa8ecd8e-5818-4d37-8c5d-0483e060f118/22AE5959-F619-4DCF-B755-3045FE92BD7B.png)

  

Now navigate to `/bin/Debug`. And there you should find your `MyFirstMod.dll` file. Now, you can just copy-paste it to your **Mods** folder.

  

Now just start slime rancher and you should see, after clicking the **Mods tab**, your mod information. If it‘s there, then your first mod is ready!

  

![](https://t24465758.p.clickup-attachments.com/t24465758/cbc146c0-b4cb-4242-9d08-35dc3dbf2c34/2675517C-9194-4DCB-A3E4-B012B63D0CA1.png)

  

Now, for now, your mod isn‘t doing anything. Now, after all that setup, we can finally start the fun part about modding in the next tutorials. There are some optional things we can do, but you‘re not forced to. Else:

  

I wish you good luck with your modding adventure!

  

**Optional**
--------

### **Build events (RECOMMENDED)**

Now, to be honnest, after a while, having to drag your mod DLL everytime to the Mods folder can become tiring. For this, we can automize the proccess of it.

  

Now, instead of dragging the build (aka `MyFirstMod.dll`) to the Mods folder, copy it‘s path (right click on your `MyFirstMod.dll` and select **Copy as path**)

![](https://t24465758.p.clickup-attachments.com/t24465758/9ddc82cb-7ee9-4025-abe5-1d73c10242a6/9F949DDA-DE1A-44E1-BB49-5D4A38BCF339.png)

_(Example image, credits to the_ [_How-To Geek_](https://www.howtogeek.com/670447/how-to-copy-the-full-path-of-a-file-on-windows-10/) _website)._

  

After doing this, you can go to the **Build Event tab** on your **Settings**

![](https://t24465758.p.clickup-attachments.com/t24465758/bbd91979-f583-4abd-94ba-fe2b1500d3f8/F7B9DDAE-1E0A-4901-AE28-AC92A5043906.png)

_(Image from_ [_Mitesh Sureja‘s Blog_](http://miteshsureja.blogspot.com/2012/04/how-to-use-pre-build-and-post-build.html)_)_

  

Now in theh **Post-build event command line**, add this: `xcopy "(PathToCopyFrom)" "(TargetPath)"`

  

Now, replace the `"(PathToCopyFrom)"` with the copy I asked you to copy before, the path to `MyFirstMod.dll`. You should now add the `MyFirstMod.dll` at the end of your copied path, so the first half looks like `xcopy "YourPath\MyFirstMod.dll" "(TargetPath)""`.

  

Now lets focus on the `"(TargetPath)"`, you just need to locate your **Mods** folder (the one where you usually add your mods to play modded SlimeRancher), and same as for the `MyFirstMod.dll`, right click and press **Copy as path**.

  

Now finally replace the with your copied path, and the first half is done!
  

The command we‘ve written in the **Post-build event command line** will make it easier for us to copy that **.dll** file into the **Mods** folder.

  

Now, to make it work, just build the mod and the game should start all by itself!

  

### **MrPurple‘s AssemblyPublicizer**

> Now, I would like to mention that this is a upgraded version of [CabbageCrow‘s AssemblyPublicizer](https://github.com/CabbageCrow/AssemblyPublicizer), but considering it has some issues that will become visible later on, we‘re using this upgraded one. Shout to [CabbageCrow](https://github.com/CabbageCrow)!

  

We will have to use `MrPurple‘s AssemblyPublicizer` to allow us to access every property we‘re going to need in our modding journey. It allows us to convert a .dll file with lots of `private` elements (aka properties, variables, functions, etc…) to a copy of it, containing only `public` elements. In other words: “Things we can‘t access become accessible for our code“.

  

It‘s like a big house where every door is closed, you have no way to open them by yourself. Now the AssemblyPublicizer comes in game and opens magically for you all the doors! ~~(It actually recreates the house and keeps the doors open, creating a copy of the closed house, but let‘s pretend it just opens them by magic)~~

  

You can download it [here](https://github.com/MrPurple6411/AssemblyPublicizer).

Now, how to use it? It‘s written on the github page (so I won‘t explain it here)
Now, where we use it? Wait for the **“Adding the needed references“** section
  


 

#### **Setting „Allow unsafe code“**

Now, talking for experience (painful hours wasted for this 1 single thing), we‘re going to need to set a compiler option, else every time we‘re going to build the project it‘s going to result into an error. For this we need to set the „allow unsafe code“ option to true. There are 2 ways to achieve this, one via the IDE, one via editing the .csproj of the project.

  

1\. For the first way, proceed to open the project's Properties page in your Visual Studio development environment (aka IDE). Click the Build property page, then select the Allow Unsafe Code check box.

  

2\. For the second way, open your .csproj file and add this snippet below:

```plain
  <PropertyGroup>
    <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
  </PropertyGroup>
```

  

  

![](https://t24465758.p.clickup-attachments.com/t24465758/e49e5070-389a-4cf8-a5db-4fae8e765b0b/91CDC5A8-4E81-4FDB-99B0-F4EC118286AB.png)

_(Credit to this_ [_StackOverflow post_](https://stackoverflow.com/a/6771861)_, a bit outdated, but it still works with modern Visual Studio versions)_

  

#### Adding the new references

Just remove the old references and add the publicized ones. After all what we‘ve done yet, you should be able to access codes you first weren‘t able to touch!