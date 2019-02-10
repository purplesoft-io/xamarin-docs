---
title: "Xamarin.Essentials Map"
description: "The Map class in Xamarin.Essentials enables an application to open the installed map application to a specific location or placemark."
ms.assetid: BABF40CC-8BEE-43FD-BE12-6301DF27DD33
author: jamesmontemagno
ms.author: jamont
ms.date: 11/04/2018
---

# Xamarin.Essentials: Map

The **Map** class enables an application to open the installed map application to a specific location or placemark.

## Get started

[!include[](~/essentials/includes/get-started.md)]

## Using Map

Add a reference to Xamarin.Essentials in your class:

```csharp
using Xamarin.Essentials;
```

The Map functionality works by calling the `OpenAsync` method with the `Location` or `Placemark` to open with optional `MapLaunchOptions`.

```csharp
public class MapTest
{
    public async Task NavigateToBuilding25()
    {
        var location = new Location(47.645160, -122.1306032);
        var options =  new MapLaunchOptions { Name = "Microsoft Building 25" };

        await Map.OpenAsync(location, options);
    }
}
```

When opening with a `Placemark`, the following information is required:

- `CountryName`
- `AdminArea`
- `Thoroughfare`
- `Locality`

```csharp
public class MapTest
{
    public async Task NavigateToBuilding25()
    {
        var placemark = new Placemark
            {
                CountryName = "United States",
                AdminArea = "WA",
                Thoroughfare = "Microsoft Building 25",
                Locality = "Redmond"
            };
        var options =  new MapLaunchOptions { Name = "Microsoft Building 25" };

        await Map.OpenAsync(placemark, options);
    }
}
```

## Extension Methods

If you already have a reference to a `Location` or `Placemark`, you can use the built-in extension method `OpenMapAsync` with optional `MapLaunchOptions`:

```csharp
public class MapTest
{
    public async Task OpenPlacemarkOnMap(Placemark placemark)
    {
        await placemark.OpenMapAsync();
    }
}
```

## Directions Mode

If you call `OpenMapAsync` without any `MapLaunchOptions`, the map will launch to the location specified. Optionally, you can have a navigation route calculated from the device's current position. This is accomplished by setting the `NavigationMode` on the `MapLaunchOptions`:

```csharp
public class MapTest
{
    public async Task NavigateToBuilding25()
    {
        var location = new Location(47.645160, -122.1306032);
        var options =  new MapLaunchOptions { NavigationMode = NavigationMode.Driving };

        await Map.OpenAsync(location, options);
    }
}
```

## Platform Differences

# [Android](#tab/android)

- `NavigationMode` supports Bicycling, Driving, and Walking.

# [iOS](#tab/ios)

- `NavigationMode` supports Driving, Transit, and Walking.

# [UWP](#tab/uwp)

- `NavigationMode` supports Driving, Transit, and Walking.

--------------

## Platform Implementation Specifics

# [Android](#tab/android)

Android uses the `geo:` Uri scheme to launch the maps application on the device. This may prompt the user to select from an existing app that supports this Uri scheme.  Xamarin.Essentials is tested with Google Maps, which supports this scheme.

# [iOS](#tab/ios)

No platform-specific implementation details.

# [UWP](#tab/uwp)

No platform-specific implementation details.

--------------

## API

- [Map source code](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Map)
- [Map API documentation](xref:Xamarin.Essentials.Map)
