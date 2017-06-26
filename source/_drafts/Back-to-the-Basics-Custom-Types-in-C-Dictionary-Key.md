---
title: 'Back to the Basics: Custom Types in C# Dictionary Key'
date: 2017-06-21 18:06:43
tags: csharp dotnet dictionary perf
---

## The Performance Problem

I recently bumped into a performance problem that I haven't thought about in quite a while.  

```
public struct CatTrackingId
    {
        public CatTrackingId(string table, string localId)
            : this()
        {
            Table = table;
            LocalId = localId;
        }

        public string Table { get; private set; }

        public string LocalId { get; private set; }

```

```
   private readonly Dictionary<CatTrackingId, CatTracking> _catTracking;
```