# Loading Images

Adding Images to your project
-----------------------------
Simply add the image files to your project files and configure them as EmbededResource, just as the modinfo.json.<br>
Make sure, that your file is a png, you may have to change the upcoming function if you use a jpeg or bitmap.

Loading said Images
-------------------
You can easily write a Utility Class, with a method to load Sprites from your Assemblies Resources:
```cs title="Utility Class" linenums="1"
namespace YourMod
{
    public static class Utility
    {
        public static Texture2D LoadTextureFromAssembly(string filename)
        {
            var executingAssembly = Assembly.GetExecutingAssembly();
            var manifestResourceStream = executingAssembly.GetManifestResourceStream(executingAssembly.GetName().Name + "." + filename + ".png");
            var numArray = new byte[manifestResourceStream.Length];
            manifestResourceStream.Read(numArray, 0, numArray.Length);
            var tex = new Texture2D(1, 1);
            tex.LoadImage(numArray);
            tex.filterMode = FilterMode.Bilinear;
            return tex;
        }

        public static Sprite ConvertToSprite(this Texture2D texture)
        {
            return Sprite.Create(texture, new Rect(0.0f, 0.0f, texture.width, texture.height), new Vector2(0.5f, 0.5f), 1f);
        }
    }
}
```
