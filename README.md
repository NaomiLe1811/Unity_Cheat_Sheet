# Unity_Cheat_Sheet
## Table of Contents
- [Fundamentals](#fundamentals)
  - [Unity Shortcuts](#unity-shortcuts)
  - [MonoBehaviour](#monobehaviour)
  - [Serializing Variables](#serializing-variable)
  - [Instantiating](#instantiating)
  - [Finding Game Objects](#finding-game-objects)
  - [Destroying Games Objects](#destroying-game-objects)
  - [Components](#components)
  - [Constant](#constant)
  - [Vectors](#vectors)
  - [Transform](#transform)
  - [Quaternion](#quaternion)
  - [Euler Angles](#euler-angles)
- [Movement & Rotation](#movement--rotation)
  - [Move Object](#move-object)
    - [Transform.Translate()](#transformtranslate)
    - [Vector3.MoveTowards()](#vector3movetowards)
    - [Vector3.Lerp()](#vector3lerp)
    - [Vector3.SmoothDamp()](#vector3smoothdamp)
  - [Rotate Object](#rotate-object)
    - [Transform.rotation](#transformrotation)
    - [Transform.eulerAngles](#transformeulerangles)
    - [Transform.Rotate()](#transformrotate)
    - [Transform.RotateAround()](#transformrotatearound)
    - [Transform.LookAt()](#transformlookat)
    - [Quaternion.LookRotation()](#quaternionlookrotation)
    - [Quaternion.FromToRotation()](#quaternionfromtorotation)
    - [Quaternion.ToAngleAxis()](#quaterniontoangleaxis)
- [Input](#input)
  - [Keyboard](#keyboard)
  - [Mouse](#mouse)
  - [Touch](#touch)
- [UI](#ui)
  - [Keep Screen's Ratio](#keep-screens-ratio)
  - [Button](#button)
  - [Slider](#slider)
- [Audio](#audio)
  - [Basic Audio Play](#basic-audio-play)
- [Design Patterns](#design-patterns)
  - [Singleton](#singleton)
- [Practical Use Cases](#practical-use-cases)

 ## Fundamentals

### Unity shortcuts 
  
  | Action                           | Key Binding                                             |
| -------------------------------- | ------------------------------------------------------- |
| View Tool                        |                                                        |
| Move Tool                        |                                                        |
| Rotate Tool                      |                                                        |
| Scale Tool                       |                                                        |
| Rect Tool                        |                                                        |
| Transform Tool                   |                                                        |
| New Game Object                  |                                                        |
| New Child Game Object            | Toggle Window Size                                      |
| Duplicate                        |                                                        |
| Play/Pause                       |                                                        |
| Focus Game Object                |                                                        |
| Key Binding                      |                                                        |
| Q                                |                                                        |
| W                                |                                                        |
| E                                |                                                        |
| R                                |                                                        |
| T                                |                                                        |
| Y                                |                                                        |
| Windows: CTRL + SHIFT + N        | Mac: CMD + SHIFT + N ALT + SHIFT + N                      |
| SHIFT + SPACE                    |                                                        |
| Windows: CTRL + D                | Mac: CMD + D Windows: CTRL + P Mac: CMD + P F              |
|                                |                                                        |
### Visual Studio Code

  | Action                           | Key Binding                                             |
| -------------------------------- | ------------------------------------------------------- |
| Command Palette                  | Windows: CTRL + SHIFT + P Mac: CMD + SHIFT + P            |
| Quick File Open                   | Windows: CTRL + P Mac: CMD + P                           |
| Toggle Sidebar                    | Windows: CTRL + B Mac: CMD + B                           |
| Multi-Select Cursor               | Windows: CTRL + D Mac: CMD + D                           |
| Copy Line                         | Windows: SHIFT + ALT + UP or SHIFT + ALT + DOWN Mac: OPT + SHIFT + UP or OPT + SHIFT + DOWN |
| Comment Code Block                | Windows: SHIFT + ALT + A (Multi-line comment), CTRL + K + C (Single-line comment) Mac: SHIFT + OPT + A |
| Show All Symbols                  | Windows: CTRL + T Mac: CMD + T                           |
| Trigger suggestion and parameter hints | Windows: Ctrl + Space, Ctrl + Shift + Space Mac: CMD + Space, CMD + Shift + Space |
| Show References                   | Windows: Shift + F12 Mac: Shift + F12                    |
| Global Find                       | Windows: CTRL + SHIFT + F Mac: CMD + SHIFT + F            |


### [MonoBehaviour](https://docs.unity3d.com/ScriptReference/MonoBehaviour.html)
[MonoBehaviour Life Cycle Flow Chart](https://docs.unity3d.com/uploads/Main/monobehaviour_flowchart.svg)

All components derived from the MonoBehaviour class execute a series of event functions in a predetermined order. These functions include:
```csharp
Awake(): Called after a game object has been instantiated.
OnEnable(): Called when a game object is enabled.
Start(): Called before the first frame update.
Update(): Invoked on every frame.
LateUpdate(): Triggered on every frame after the Update() function.
OnBecameVisible(): Called when the current game object becomes visible via any camera.
OnBecameInvisible(): Called when the current game object no longer becomes visible via any camera.
OnDrawGizmos(): Called for drawing gizmos in the scene window.
OnGUI(): Invoked multiple times for GUI events.
OnApplicationPause(): Called when the game is paused via the Unity editor.
OnDisable(): Executed when the game object is disabled.
OnDestroy(): Triggered when the game object is destroyed.
```

There's a lifecycle function called `FixedUpdate`, which is called a fixed number of times per second. You can configure the frequency in the Edit ▸ Project Settings ▸ Time ▸ Fixed Timestep.

### Serializing Variables
Unity can serialize variables, converting data into a format editable from the Unity editor. Serialization depends on attributes or access modifiers applied to the variable.

If a variable is public , it'll be automatically serialized:

```csharp
public int age = 10;
```

If you don't want public variables to be serialized, you can use the NonSerialized attribute from the System namespace like so:

```csharp
[NonSerialized] public int age = 10;
```
Private variables not serialized. However, if you want them to be serialized, Unity has an attribute called SerializeField that can be found from the Unity namespace. It can be applied like so:

```csharp
[SerializeField] private int age = 10;
```

### Instantiating
New game objects can be inserted into the scene programmatically by calling the function. This function has three arguments.
- The Game Object
- *(Optional)* Global Position
- *(Optional)* Rotation
