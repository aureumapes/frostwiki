# Adding Slimes

Adding an ID for your Slime
---------------------------
Its important, that your Slime has an ID, to refer to it via code and when in game.
You can add one by creating an Enum that you add to your Enum Holder:
```c-sharp
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
Now create a new static class and a new static void inside that class:
