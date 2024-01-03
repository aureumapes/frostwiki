# Adding a Food Group
If you want to add an Food Group to the Game you'll need multiple patches don.

First things first, define the Food Class:
```cs
namespace YourMod
{
    public class FoodClass
    {
        internal static Identifiable.Id[] YOUR_FOOD_CLASS =
        {
            Identifiable.Id.WILD_HONEY_CRAFT,
            Identifiable.Id.ROYAL_JELLY_CRAFT,
            Identifiable.Id.HONEY_PLORT
        };
    }
}
```
you can, of course change the items contained in the class, feel free to play around with it

Add following entry to your ModdedIds:
```cs title="ModdedIds" linenums="1"
public static readonly SlimeEat.FoodGroup YOUR_FOODGROUP;
```

Now we'll come to the harder part: patch the existing SlimeEat and SlimeDiet class:

```cs title="FoodPatch Class" linenums="1"
using System.Linq;

namespace YourMod
{
    internal class FoodPatch
    {
        [HarmonyLib.HarmonyPatch(typeof(SlimeEat))]
        [HarmonyLib.HarmonyPatch("GetFoodGroupIds")]
        internal static class FoodGroupPatch
        {
            public static void Postfix(ref Identifiable.Id[] __result, SlimeEat.FoodGroup group)
            {
                if (!SlimeEat.foodGroupIds.ContainsKey(ModdedIds.YOUR_FOODGROUP))
                    SlimeEat.foodGroupIds.Add(ModdedIds.YOUR_FOODGROUP, FoodClass.YOUR_FOOD_CLASS);
                if (__result == null)
                    return;
                var list = __result.ToList();
                if (group == ModdedIds.YOUR_FOODGROUP)
                    foreach (var id in FoodClass.YOUR_FOOD_CLASS)
                        list.Add(id);
            }
        }
    }

    [HarmonyLib.HarmonyPatch(typeof(SlimeDiet))]
    [HarmonyLib.HarmonyPatch("GetFoodCategoryMsg")]
    internal static class FoodGroupPatchMsg
    {
        public static bool Prefix(ref string __result, Identifiable.Id id)
        {
            if (SlimeEat.GetFoodGroupIds(ModdedIds.YOUR_FOODGROUP).Contains(id))
                __result = "m.foodgroup." + ModdedIds.YOUR_FOODGROUP.ToString().ToLower();
            return false;
        }
    }
}
```
And your done.
Use the FoodGroup Id, as you want