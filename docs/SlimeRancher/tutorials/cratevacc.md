# Planning
Slime Rancher is a really complicated game to mod, so we will start with something that's simple: We all know that we can't collect crates, they stick on the vacuum gun and you can shoot them... but what if we can vacuum them? And that's what we are going to do!

## Definitions

Here are the explanations of some words:

`Identifiable.Id` 
The creator explained it on the github of SRML.

`Ammo`
Ammo is the same as Inventory.

`Vaccumable/to vacuum`
Collectable/to collect

`LookupDirector`
The creator explained it on the github of SRML.

`PediaDirector`
The creator explained it on the github of SRML.


# How to start
Time to insert this code snippet in the Load or PostLoad function in our main class, you can choice where to put.

```csharp
AmmoRegistry.RegisterAmmoPrefab(PlayerState.AmmoMode.DEFAULT, SRSingleton<GameContext>.Instance.LookupDirector.GetPrefab(Identifiable.Id.CRATE_PARTY_01));
Sprite icon = SRSingleton<SceneContext>.Instance.PediaDirector.entries.First((PediaDirector.IdEntry x) => x.id == PediaDirector.Id.ORNAMENTS).icon;
LookupRegistry.RegisterVacEntry(Identifiable.Id.CRATE_PARTY_01, new Color32(138, 87, 40, 255), icon);
SRSingleton<GameContext>.Instance.LookupDirector.GetPrefab(Identifiable.Id.CRATE_PARTY_01).GetComponent<Vacuumable>().size = Vacuumable.Size.NORMAL;
```
Don‘t think I‘ll let you simply copy paste my code tho, it‘s time to explain what it does!

## First Line
```csharp
AmmoRegistry.RegisterAmmoPrefab(PlayerState.AmmoMode.DEFAULT, SRSingleton<GameContext>.Instance.LookupDirector.GetPrefab(Identifiable.Id.CRATE_PARTY_01));
```

Now, lets start with the method `AmmoRegistry.RegisterAmmoPrefab`:
We are making the crate vaccumable. This method accept 2 parameters:
An `AmmoMode` Enum
The target `GameObject`
There only exist 2 AmmoMode:

* `DEFAULT` (Normal)
* `NIMBLE_VALLEY` (Once you pass the gate of Mochi, the item will disappear)

For this tutorial we want the `DEFAULT` (Normal) Enum.

Then, we need a `GameObject`, that means just an object of the game. We want to get the party crate object for this example.

`SRSingleton<GameContext>.Instance.LookupDirector`
We are getting the `GameContext(SRSingleton<GameContext>.Instance)` to then get the `LookupDirector`. The `LookupDirector` contains a `GetPrefab` method, wich requires a `Identifiable.Id` and returns the desired `GameObject`.
TL;DR (the second parameter) We are getting the `GameObject` of our Crate.


## Second Line

```csharp
Sprite icon = SRSingleton<SceneContext>.Instance.PediaDirector.entries.First((PediaDirector.IdEntry x) => x.id == PediaDirector.Id.ORNAMENTS).icon;
```

All collectable objects of the game have their own picture, so why not our? And that's what we are doing!

```csharp
Sprite icon = SRSingleton<SceneContext>.Instance.PediaDirector
```
Like with the `LookupDirector`, we are getting the `PediaDirector` from the SceneContext.

`PediaDirector.entries` are all the icons/images of the game.

`entries.First((PediaDirector.IdEntry x) => x.id == PediaDirector.Id.ORNAMENTS).icon` means that we are targeting the Ornaments (These christmas-looking balls), getting an icon from some sort of object. You can change the `PediaDirector.Id` to the object that you want to have the image


## Third Line
```csharp
LookupRegistry.RegisterVacEntry(Identifiable.Id.CRATE_PARTY_01, new Color32(138, 87, 40, 255), icon);
```
Here we are assigning some background color and our icon to our crate.

`LookupRegistry.RegisterVacEntry` requires 3 parameters:
* The `Identifiable.Id` of the object that we want to give the colour and icon
* The Colour that we want to give
* The Icon that we want to give
  
We already have the Id and the Icon, but for the colour you will have to use a rgb sequence. You can go to this website; play around with the settings until you found your colour. Then just copy the number at the red (default 47), then green (default 50) and blue (default 159) slide and put them into the parameters of the `new Color32()`. So it would be `new Color32(47, 50, 159, 255)` (first red, then green and finally blue: This order has to be correct!). The last parameter, the 255, is needed for the transparency: You don't will need it.

## Fourth Line

```csharp
SRSingleton<GameContext>.Instance.LookupDirector.GetPrefab(Identifiable.Id.CRATE_PARTY_01).GetComponent<Vacuumable>().size = Vacuumable.Size.NORMAL;
```

Here we are making the crate actually vaccumable. Remember, in the first line we only made it "storagable", so that it can enter the inventory, but if you would run your mod then the crate still will stick on the gun and not enter.

`SRSingleton<GameContext>.Instance.LookupDirector.GetPrefab(Identifiable.Id.CRATE_PARTY_01)`, this has been already seen on the first line, we are getting the GameObject of our crate.

```csharp
.GetComponent<Vacuumable>().size = Vacuumable.Size.NORMAL;
```
Now we are getting the "Vacuumable Component" (Think this like a folder), then changing the size property to `Vacuumable.Size.NORMAL`. We have 3 type of sizes:
* NORMAL
* LARGE
* GIANT
  
Normal is the normal size. This means it can be collected.

Large means that it will stick on the vacuum gun (like a normal crate)

Giant means that it can't be collected at all, like a gordo.

## Fifth/Last Line

```csharp
TranslationPatcher.AddActorTranslation("l.crate_party_01", "Party Crate");
```
You can leave it, but this will add the little "Party Crate" name in your inventory when you are storing a party crate. We are doing this because crates aren't vacuumable, so there dosen't exist any name that should show up when you have one crate in your inventory. So we have to add one ourself!

## Conclusion

This is a long tutorial, but only because I tried to explain everything in details. This is really confusing at start, but you will get the point. Anyways, the next tutorial part is to add custom slimes (warning, it's a really long part), so enjoy your new crate!

P.S.

But FrostDracony, where can I find a party crate? I don't want to search the entire map for one! Ok, keep calm: Just spawn one! On Windwos, you can press `Ctrl + Tab` to access the command bar. Type in spawn `CRATE_PARTY_01` and a party crate should spawn where you were looking at! (If it doesn't spawn, then it probably spawned below the map.. Just find a flat place like the ranch and retry the command)

