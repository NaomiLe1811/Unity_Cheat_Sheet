# Unity_Cheat_Sheet
## Table of Contents
- [Fundamentals](#fundamentals)
  - [MonoBehaviour](#monobehaviour)
  - [Game Recycle](#gamerecycle)
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
| **If you're using Visual Studio Code, here are some handy keyboard shortcuts.** |
| -------------------------------- | ------------------------------------------------------- |
| **Action**                       | **Key Binding**                                         |
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
