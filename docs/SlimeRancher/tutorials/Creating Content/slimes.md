# Adding Slimes

Adding an ID for your Slime
---------------------------
Its important, that your Slime has an ID, to refer to it via code and when in game.
You can add one by creating an Enum that you add to your Enum Holder:
```cs title="ModdedIds EnumHolder" linenums="1"
namespace YourMod
{
    [EnumHolder]
    public class ModdedIds
    {
        public static readonly Identifiable.Id YOUR_SLIME;
    }
}
```

Making the Slime
----------------
Now create a new class and a new static void inside that class:
```cs title="CreateSlime Class" linenums="1"
using System;
using SRML.SR;
using SRML.Utils;
using UnityEngine;
using Object = UnityEngine.Object;

namespace DreamSlimes.Slimes
{
    public class CreateSlime
    {
        public static void CreateYourSlime()
        {
            // Copy the Prefab for the Pink Slime
            var slimeByIdentifiableId =
                SRSingleton<GameContext>.Instance.SlimeDefinitions.GetSlimeByIdentifiableId(Identifiable.Id.PINK_SLIME);
            var slimeDefinition = (SlimeDefinition)PrefabUtils.DeepCopyObject(slimeByIdentifiableId);
            slimeDefinition.AppearancesDefault = new SlimeAppearance[1];
            
            // Adding an eat map to the Slime, which allows it to eat something
            slimeDefinition.Diet.Produces = new[] { ModdedIds.YOUR_PLORT };
            slimeDefinition.Diet.MajorFoodGroups = new[] { SlimeEat.FoodGroup.PLORTS };
            slimeDefinition.Diet.Favorites = new[] { Identifiable.Id.SABER_PLORT };
            slimeDefinition.Diet.EatMap?.Clear();

            // Setting basic preferences for the Slime
            slimeDefinition.CanLargofy = false; // Slime can't become a largo
            slimeDefinition.FavoriteToys = Array.Empty<Identifiable.Id>(); // Clear the Favourite Toy lsit
            slimeDefinition.Name = "Your Slime"; // Change the name of the Slime
            slimeDefinition.IdentifiableId = ModdedIds.YOUR_SLIME; // Setting the ID of the SLime to be your previously made Enum
            
            // Creating and Modifying the Slimes GameObject
            var go =
                PrefabUtils.CopyPrefab(
                    SRSingleton<GameContext>.Instance.LookupDirector.GetPrefab(Identifiable.Id.PINK_SLIME)); // Copy the prefab GO
            go.name = "Dream_Slime"; // Setting the name of the GO in the Editor and in the Game
            // Setting the previously created SlimeDefinition to be the one for some of the GO-Components
            go.GetComponent<PlayWithToys>().slimeDefinition = slimeDefinition;
            go.GetComponent<SlimeAppearanceApplicator>().SlimeDefinition = slimeDefinition;
            go.GetComponent<SlimeEat>().slimeDefinition = slimeDefinition;
            go.GetComponent<Identifiable>().id = Id.DREAM_SLIME;
            go.GetComponent<Vacuumable>().size = Vacuumable.Size.LARGE;
            go.transform.localScale = new Vector3(0.75f, 0.75f, 0.75f); // Resizing the Slime
            Object.Destroy(go.GetComponent<PinkSlimeFoodTypeTracker>()); // Destroy the Tracker of the Pink SLime

            // Modifying the Slimes Appearance (Color etc.)
            var slimeAppearance =
                (SlimeAppearance)PrefabUtils.DeepCopyObject(slimeByIdentifiableId.AppearancesDefault[0]);
            slimeDefinition.AppearancesDefault[0] = slimeAppearance;
            var structures = slimeAppearance.Structures;
            var structures2 = structures;
            foreach (var structure in structures2)
            {
                var defaultMaterials = structure.DefaultMaterials;
                if (defaultMaterials != null && defaultMaterials.Length != 0)
                {
                    var val8 = Object.Instantiate(SRSingleton<GameContext>.Instance
                        .SlimeDefinitions.GetSlimeByIdentifiableId(Identifiable.Id.PINK_SLIME).AppearancesDefault[0]
                        .Structures[0]
                        .DefaultMaterials[0]);
                    val8.SetColor("_TopColor", new Color32(0,0,0,0)); // (1)
                    val8.SetColor("_MiddleColor", new Color32(0,0,0,0));
                    val8.SetColor("_BottomColor", new Color32(0,0,0,0));
                    val8.SetFloat("_Shininess", 1f);
                    val8.SetFloat("_Gloss", 0f);
                    structure.DefaultMaterials[0] = val8;
                }
            }

            var expressionFaces = slimeAppearance.Face.ExpressionFaces;
            foreach (var val9 in expressionFaces)
            {
                if (val9.Mouth)
                {
                    val9.Mouth.SetColor("_MouthBot",
                        new Color32(0x82, 0x82, 0xef, 0xff));
                    val9.Mouth.SetColor("_MouthMid",
                        new Color32(0xa0, 0xa0, 0xff, 0xff));
                    val9.Mouth.SetColor("_MouthTop",
                        new Color32(0xa0, 0xa0, 0xff, 0xff));
                }

                if (val9.Eyes)
                {
                    val9.Eyes.SetColor("_EyeRed", new Color(26, 45, 56, byte.MaxValue)); // (2)
                    val9.Eyes.SetColor("_EyeGreen", new Color32(94, 141, 160, byte.MaxValue));
                    val9.Eyes.SetColor("_EyeBlue", new Color32(40, 60, 68, byte.MaxValue));
                }
            }

            slimeAppearance.Face.OnEnable();
            var val10 = slimeAppearance;
            var colorPalette = default(SlimeAppearance.Palette);
            colorPalette.Top = new Color32(252, 254, byte.MaxValue, byte.MaxValue); // (1)
            colorPalette.Middle = new Color32(210, 236, 247, byte.MaxValue);
            colorPalette.Bottom = new Color32(124, 138, 163, byte.MaxValue);
            val10.ColorPalette = colorPalette;
            go.GetComponent<SlimeAppearanceApplicator>().Appearance = slimeAppearance;
            
            // Register the slimes to different registries
            LookupRegistry.RegisterIdentifiablePrefab(go);
            SlimeRegistry.RegisterSlimeDefinition(slimeDefinition);
            AmmoRegistry.RegisterAmmoPrefab(PlayerState.AmmoMode.DEFAULT,
                SRSingleton<GameContext>.Instance.LookupDirector.GetPrefab(ModdedIds.YOUR_SLIME));
            var icon = slimeAppearance.Icon = Utils.LoadTexture("yourSlimeIcon") // (3)
            slimeAppearance.ColorPalette.Ammo = new Color32(210, 236, 247, 225);
            SRSingleton<GameContext>.Instance.LookupDirector.GetPrefab(ModdedIds.YOUR_SLIME)
                .GetComponent<Vacuumable>()
                .size = Vacuumable.Size.LARGE;
            TranslationPatcher.AddActorTranslation("l.your_slime", "Your Slime"); // Make sure to use the Slimes ID with lower snake case (like_this)
        }
    }
}
```
Now load the function by calling `CreateSlime.CreateYourSlime()` in your Load() function ( 1 )

Creating a Pedia Entry (optional)
-------------------------
You may want to add a Pedia Entry for your Slime
First add this line into your EnumHolder
```cs title="EnumHolder" linenums="1"
public static readonly PediaDirector.Id YOUR_SLIME_ENTRY;
```
Add this to the bottom of your CreateYourSlime() function:
```cs title="Register Pedia" linenums="1"
PediaRegistry.RegisterIdEntry(ModdedIds.YOUR_SLIME_ENTRY, icon);
```
And last, add this to your PreLoad function, before patching all with the Harmony Instances:
```cs title="PreLoad" linenums="1"
RegisterIdentifiableMapping(PediaDirector.Id.PLORTS, ModdedIds.YOUR_SLIME/*(4)*/);
RegisterIdentifiableMapping(ModdedIds.YOUR_SLIME_ENTRY, );
SetPediaCategory(ModdedIds.YOUR_SLIME_ENTRY, PediaCategory.SLIMES);
new SlimePediaEntryTranslation(ModdedIds.YOUR_SLIME_ENTRY)
    .SetTitleTranslation("Your Slimes")
    .SetIntroTranslation("INTRO")
    .SetDietTranslation("FOOD")
    .SetFavoriteTranslation("FAVOURITE_FOOD")
    .SetSlimeologyTranslation("SLIMEOLOGY_SECTION")
    .SetRisksTranslation("RISK_SECTION")
    .SetPlortonomicsTranslation("PLORT_SECTION");
```

1. Make sure to change thy color
2. Thou shall alter the colours. I don't really know how to really bring this to practical use
3. See [Image Loading](../../images)
4. This is the Item you need to collect, to get the Entry