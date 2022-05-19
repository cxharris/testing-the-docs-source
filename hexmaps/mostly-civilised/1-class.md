# Lecture 1
https://www.youtube.com/watch?v=j-rCuN7uMR8&list=PLbghT7MmckI7JHf0pdEQ8fbPb-LoDXEno


Download the hex model (`hex.blend`) from https://github.com/quill18/MostlyCivilizedHexEngine.

Intend to generate hex procedurally later, but just choose *Assets > Import New Asset* for now.

1. Create an empty gameobject and ensure its transform is 0,0,0. Call it *HexMap*. This is the thing that represents the entirety of the map. There are nuances relating to having one giant object versus multiple smaller objects. 

For this pass, we *are* going to have each hex being its own separate game object. There's going to be a few different reasons for choosing this route, but we're also going to be looking at how to optimise this behaviour.

The subtext of course, is that this isn't the most performant way to organise things. Because the biggest overhead for rendering an object is the overhead of it being an object itself, as opposed to the number of triangles. So it's generally better to have fewer objects even if they're bigger. Note that Unity no longer has a 65000 vertex limit to a mesh - you can set a parameter that allows up to 4 billion.

2. Create a component on the HexMap GameObject called HexMap as well - this will be responsible for creating and managing the map. To start off, it's just going to help us generate flat untextured hexes.
3. In the new script, just create a `GenerateMap()` method on `HexMap` and call it from `Start()`:

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class HexMap : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        GenerateMap();
    }

    public void GenerateMap()
    {

    }
}
```

4. `GenerateMap`'s job is going to be to generate our hexes, OK? So let's say, our first map is going to be a 10x10 map - 100 hexes. We're going to have to loop around both dimensions to place each instantiated hex. To help us, to be sure, we'll have some kind of hex prefab - a public hex prefab.

When we instantiate our HexPRefab, and it needs a location, so in world space, a suitable co-ordiniate might be (column, 0, row) - it's got a 0 middle dimension because we want all hexes to be on the same plane, and the way we are crea ting this world means that y=0 is this plane. It also needs a rotation, and usually, our first attempt at providing a rotation is by providing the identity rotaiton. So here's the modified `GenerateMap()` so far - bear in mind that this is currently WRONG:

```C#
    public GameObject HexPrefab;

    public void GenerateMap()
    {
        for (int column = 0; column < 10; column++)
        {
            for (int row = 0; row < 10; row++)
            {
                // Instantiate a hex
                Instantiate(HexPrefab, new Vector3(column, 0, row), Quaternion.identity, this.transform);
            }
        }

    }
```
The fourth (optional) parameter is the intended *parent* GameObject, which we are going to declare as *this*, recalling that it's the `HexMap` that is doing all this work so will adopt the `this` moniker for this purpose.

5. Our HexMap is expecting a HexPrefab. 

[9:30]

The low impedance approach is to simply create a prefab from the hexmodel we imported earlier. But several things will go wrong if we do this.

a. The individual hexes are standing on their edges - they need to be rotated into the XZ plane. As the model was brought in from Blender, it actually needs a -90degree reotation on th x axis to be properly flat. It is VERY common for your co-ordinates in your modeling program (e.g. Blender) to not be the same as those in Unity.

ALWAYS ALWAYS ALWAYS create an empty object and parent th emodel to it before you make it into a prefab. This will save a lot of unspecirfied pain later.

So create an empty called HexPrefab, and drag HexModel (... the one that you imported) so that it is a child. Ensure both are tranformed to 0,0,0. The model is going to have that -90degrees rotation. Not the prefab! Same thing if I needed to scale things. I might have modeled the wrong size - fix it at the model level, not the prefab level.

Then you can drag HexPRefab into the PRefabs folder and then delete it from the ierarchy.


b. OK they're now flat, but they're obviously no tpositioned correclty. The  reason is tha tevery other row is supposed to be offset by some amount. 

But even the spacing isn't quite right.

Let's talk about the dimensions of a hex - you can th ink about it a little bit like a circle with an inner and an outer radius.





5. 
