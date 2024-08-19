# Debug Menu
[![Unity 2021.3+](https://img.shields.io/badge/unity-2021.3%2B-blue.svg)](https://unity3d.com/get-unity/download)
[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](LICENSE.md)

A simple and extensible debugging menu for Unity3D.
Right now the system works will parameterless methods, I plan to add simple parameters and watch values in the future.

## System Requirements
Unity 2021.3+. Will likely work on earlier versions but this is the version I tested with.

## Installation
Use the Package Manager and use Add package from git URL, using the following: 
```
https://github.com/qhenshaw/DebugMenu.git
```

> [!WARNING]  
> The menu is enabled/disabled by adding ```DEBUG_MENU``` to Unity's ```Project Settings > Player > Scripting Define Symbols```  
> This allows you to strip debug controls from release builds.

## Usage
Add the Demo Menu sample and drop the DebugSystemCanvas prefab into your scene.  
Import the DebugMenu namespace and register your object using ``RegisterObject`` and ``DeregisterObject.``  
Add the ``DebugCommand`` attribute to assign methods to the system. A simple example for moving the player:  
```cs
using UnityEngine;
using DebugMenu;

public class Player : MonoBehaviour
{
    private Vector3 _spawnPosition;

    private void Start()
    {
        _spawnPosition = transform.position;
    }

    private void OnEnable()
    {
        DebugMenuSystem.Instance.RegisterObject(this);
    }

    private void OnDisable()
    {
        DebugMenuSystem.Instance.DeregisterObject(this);
    }

    [DebugCommand("Reset Player Position")]
    public void ResetPosition()
    {
        transform.position = _spawnPosition;
    }

    [DebugCommand("Teleport Player")]
    public void TeleportForward()
    {
        transform.position += transform.forward * 5f;
    }
}
```
