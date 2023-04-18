---
title: "UnityとUe5のMethod整理"
author:
  name: lee
date: 2023-04-19 19:25:00 +0900
categories: [Programming]
tags: [C#, C++, Unity, Ue5]
---

# DebugLog

```cpp
  UE_LOG(LogTemp, Log, TEXT("My Name: %f"), 100f);
  UE_LOG(LogTemp, Waring, TEXT("My Name: %f"), 100f); //黄色でDebugLog出力
```

```cs
  float test = 100f;
  Debug.Log($"My Name: {test}");
```

# Remap

## cpp

```cpp
  // map pitch from [270.f, 360.f] to [-90, 0]
  FVector2D InRange(270.f, 360.f);
  FVector2D OutRange(-90.f, 0.f);
  float val = 360f;
  float test = FMath::GetMappedRangeValueClamped(InRange, OutRange, val);
  //test = 0.f
```

## cs

```cs
  public static float Remap (this float value, float from1, float to1, float from2, float to2) 
  {
      return (value - from1) / (to1 - from1) * (to2 - from2) + from2;
  }

  float val = 0f;
  Remap(val, 270f, -90f, 360f, 0);
```