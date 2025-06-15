# Enum Patching

Little explanation
------ 

Now, what are ids? Id stands for identifier, the most used enum type would be `Identifiable.Id`. Why do we need that? Now, very much simplifeid, as the name already implies it itself, think of ids as a way to distinguish things from each other, for example, an hen would have a different `Identifiable.Id` than a Pink Slime, it's like the object's "family names" basically.

Now, of course, the ids for our future custom objects don't exist yet, hence why this tutorial in first place!


Manual
-------

Now, there are two ways at registering our enums, the first one is what I call "manual" and the second "automatic", we're starting with what I refer to "manual". To add new values to enums (for example, our popular `Identifiable.Id` one, we can use a static class called `EnumPatcher` inside the main `SRML` namespace. However, be aware, there are some enums that can only be registered using some Registry classes instead of the `EnumPatcher`. To add a new value to an enum with `EnumPatcher`, we use `EnumPatcher.AddEnumValue(Type enumType, object value, string name)`.



Automatic
-------

In this method,SRML provides us with an easy method for this, it's an attribute called EnumHolder in the `SRML.Utils.Enum` namespace. Simply attach this attribute to a static class and when your mod is loaded, SRML will then proceed to register and assign all readonly static fields with the first available free value in that enum. Basically:

```csharp
[EnumHolder]
public static class ModdedIds
{
    public static readonly Identifiable.Id CUSTOM_IDENTIFIABLE; // Creating a new Identifiable.id, the first value in Identifiable.Id has the name CUSTOM_IDENTIFIABLE
    public static readonly Gadget.Id TEST_GADGET; // Even tho it's another type of id, in this case for gadgets, it works the same way as the example above!
}
```


Conclusion
----------

When should we use the one method and the other, what are the differences of between? Basically, this takes some setup, but it's going to pay off in the long ride. It's way easier and comfortable than the manual method. However, since the manual method doesn't requires classes and etc, it's way more flexible (you can create codes in between the lines incase you're counting to use them just once), however requires more work. For the beginning, just consider the automatic!