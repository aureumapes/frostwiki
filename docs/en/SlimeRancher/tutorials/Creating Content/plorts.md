# Adding Plorts

Creating an ID for your Plort
------------------------------

Just like when creating a Slime, you have to add this line to your EnumHolder:
```cs title="EnumHolder" linenums="1"
public static readonly Identifiable.Id YOUR_PLORT;
```

Adding the Plort and its behaviours
-----------------------------------
Create a new File containing this code:
```cs title="CreatePlort" linenums="1"
namespace YourMod
{
    public class CreatePlort
    {
        public static void CreateYourPlort()
        {
            var b = PrefabUtils.CopyPrefab(
                SRSingleton<GameContext>.Instance.LookupDirector.GetPrefab(Identifiable.Id.PINK_PLORT));
            b.GetComponent<Identifiable>().id = ModdedIds.YOUR_PLORT;
            b.name = "Your Plort";
            LookupRegistry.RegisterIdentifiablePrefab(b);
            b.GetComponent<MeshRenderer>().material = Object.Instantiate(b.GetComponent<MeshRenderer>().material);
            b.GetComponent<MeshRenderer>().material.SetColor("_TopColor", new Color(0,0,0,0));
            b.GetComponent<MeshRenderer>().material.SetColor("_MiddleColor", new Color(0,0,0,0));
            b.GetComponent<MeshRenderer>().material.SetColor("_BottomColor", new Color(0,0,0,0));
            SlimeEat.FoodGroup.PLORTS.UnregisterId(ModdedIds.YOUR_PLORT);
            b.GetComponent<MeshRenderer>().material.SetColor("_CrackColor", new Color(0,0,0,0));
            AmmoRegistry.RegisterAmmoPrefab(PlayerState.AmmoMode.DEFAULT,
                SRSingleton<GameContext>.Instance.LookupDirector.GetPrefab(ModdedIds.YOUR_PLORT));
            SRSingleton<GameContext>.Instance.LookupDirector.GetPrefab(ModdedIds.YOUR_PLORT).GetComponent<Vacuumable>()
                .size = Vacuumable.Size.NORMAL;
            TranslationPatcher.AddActorTranslation("l.your_plort", "Your Plort");
            var icon = Texture.LoadTextureFromAssembly("yourPlortIcon").AsSprite();
            LookupRegistry.RegisterVacEntry(ModdedIds.YOUR_PLORT, Main.color1, icon);
            PlortRegistry.RegisterPlort(ModdedIds.YOUR_PLORT, 100f, 10f);
            DroneRegistry.RegisterBasicTarget(ModdedIds.YOUR_PLORT);
        }
    }
}
```
To make your Slimes actually producing their plorts, you have to add the Plort to the 