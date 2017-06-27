---
title: 'Back to the Basics: Custom Types in C# Dictionary Key'
tags: 
  - csharp 
  - dotnet 
  - dictionary 
  - perf
date: 2017-06-21 18:06:43
---


## The Usual Profiling, Refactoring, & Reimagining Exercises

I recently bumped into a performance problem while reworking some C# code that I haven't thought about in quite a while. I switched the code around to use the standard BCL containers instead of a hodgepodge of custom container logic and manual hashing.  As part of this work I introduced a struct to hold the Key info for a dictionary.

Below is the general idea of the struct used for the Dictionary key.  The domain has been changed to cats to protect the innocent. If you think it strange that I'm using a couple of strings here, you're probably right, but I haven't finished [profiling](https://www.jetbrains.com/profiler/) or refactoring yet.

![Coding cat](http://68.media.tumblr.com/9d435c4983e87521328423a4d0941d9e/tumblr_inline_nh05dqymmX1ro2d0d.jpg)

```
public struct CatTrackingId
{
    public CatTrackingId(string breed, string localId)
        : this()
    {
        Breed = breed;
        LocalId = localId;
    }

    public string Breed { get; private set; }

    public string LocalId { get; private set; }
}
```

This is representative of how it is used:
```
   private readonly Dictionary<CatTrackingId, CatTracking> _catTracking;
```

I know your 'spidey sense' is already tingling, but I didn't catch my rookie mistake until I re-ran the profiler, realized it was going way too slow, and noticed a lot of reflection time being taken.  I had a pretty good idea of what I'd forgotten, but did some Googling anyway, because that's what we do.  

For shame, I had forgotten my `Equals()` and `GetHashCode()`.  Turns out, after all these years we still need them.  When defining a struct containing reference types as I have here (good/bad idea? I'm open to input), the default [Equals()](https://msdn.microsoft.com/en-us/library/2dts52z7(v=vs.110).aspx) comparison uses reflection to compare the fields of the struct which can be quite costly.  

Instead of adding the methods to the class I opted to let ReSharper generate an `IEqualityComparer<CatTrackingId>` for me.  Feels good.

```
public struct CatTrackingId
{
    private static readonly IEqualityComparer<CatTrackingId> BreedLocalIdComparerInstance =
        new BreedLocalIdEqualityComparer();

    public CatTrackingId(string table, string localId)
        : this()
    {
        Breed = table;
        LocalId = localId;
    }

    public static IEqualityComparer<CatTrackingId> BreedLocalIdComparer
    {
        get
        {
            return BreedLocalIdComparerInstance;
        }
    }

    public string Breed { get; private set; }

    public string LocalId { get; private set; }

    private sealed class BreedLocalIdEqualityComparer : IEqualityComparer<CatTrackingId>
    {
        public bool Equals(CatTrackingId x, CatTrackingId y)
        {
            return string.Equals(x.Breed, y.Breed) && string.Equals(x.LocalId, y.LocalId);
        }

        public int GetHashCode(CatTrackingId obj)
        {
            unchecked
            {
                return ((obj.Breed != null ? obj.Breed.GetHashCode() : 0) * 397)
                       ^ (obj.LocalId != null ? obj.LocalId.GetHashCode() : 0);
            }
        }
    }
 ```

Next may be working out how to use something more efficient than strings to hold the `Key`, but as usual with performance, let the profiler be your guide.
