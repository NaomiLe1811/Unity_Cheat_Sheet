# Unity_Cheat_Sheet
## Table of Contents
- [Fundamentals](#fundamentals)
  - [Unity Shortcuts](#unity-shortcuts)
  - [MonoBehaviour](#monobehaviour)
  - [Serializing Variables](#serializing-variables)
  - [Instantiating](#instantiating)
  - [Finding Game Objects](#finding-game-objects)
  - [Destroying Games Objects](#destroying-game-objects)
  - [Components](#components)
  - [Constants](#constants)
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
```csharp
Instantiate(someGameObject);
Instantiate(someGameObject, new Vector3(0, 0, 10));
Instantiate(someGameObject, new Vector3(0, 0, 10), Quaternion.identity);
```
### Finding Game Objects
The GameObject class has a few methods for finding game objects within the hierarchy.
-	Find() - Searches for a game object based on its name.
-	FindGameObjectsWithTag() - Finds multiple game objects that are stored in an array and returned. Uses a game object's tag to find them.
-	FindWithTag() - Finds a game object based on its tag.
```csharp
GameObject myObj = GameObject.Find("NAME IN HIERARCHY");
GameObject myObj = GameObject.FindGameObjectsWithTag("TAG");
GameObject myObj = GameObject.FindWithTag("TAG");
```

### Destroying Game Objects
Game objects can be destroyed by calling the Destroy() function:
```csharp
Destroy(gameObject);
```
### Components
Game objects don't do much on their own. We need to add components for specific functions. If you're using custom components and need to choose others, Unity provides ways to grab them. The first method is using the GetComponent() function, typically by specifying the component class name.
```csharp
AudioSource audioSource = GetComponent<AudioSource>();
```
Alternatively, you can use the typeof keyword and assert the value like so:
```csharp
AudioSource audioSource = GetComponent(typeof(AudioSource)) as AudioSource;
```
Lastly, you can pass in the name of the component as a string like so:
```csharp
AudioSource audioSource = GetComponent("AudioSource") as AudioSource;
```

### Constants

In Unity, you can use constants to define values that remain the same throughout your script. Here's how you can use constants in Unity:

1. Declare a Constant:
Use the const keyword to declare a constant. Constants must be initialized with a value at the time of declaration and cannot be changed afterward. Here's an example:
```csharp
public class ExampleScript : MonoBehaviour
{
    // Define a constant for gravity
    private const float Gravity = 9.8f;

    void Start()
    {
        // Use the constant in your code
        float fallSpeed = Gravity * Time.deltaTime;
    }
}
```
2. Benefits of Constants:
Constants are helpful for defining values that are used in multiple places within your script and should not be modified during runtime. They make your code more readable and maintainable.

3. Usage in Unity:
You can use constants in various Unity scripts, such as MonoBehaviour scripts attached to GameObjects or utility scripts. Constants are often used for values like default speeds, fixed dimensions, or other unchanging parameters.

4. Scope of Constants:
Constants have a scope limited to the class or method in which they are declared. If you need constants accessible from multiple scripts, consider using a public static class.

Here's a simple example:
```csharp
public static class GameConstants
{
    public const int MaxScore = 100;
}

public class ScoreManager : MonoBehaviour
{
    void Update()
    {
        // Access the constant from another script
        int currentScore = CalculateScore();
        if (currentScore >= GameConstants.MaxScore)
        {
            Debug.Log("You reached the maximum score!");
        }
    }

    int CalculateScore()
    {
        // Your score calculation logic here
        return 50;
    }
}
```
### Vectors
Vectors determine game object positions and aid in distance and movement calculations. Unity has two vector classes: Vector2 for 2D games with coordinates (x, y), and Vector3 for 3D games with coordinates (x, y, z). In these classes, X represents Left/Right, Y denotes Up/Down, and Z indicates Forward/Back. Unity provides constants accessible from the relevant vector class.
#### Vector 3
```csharp
Vector3 V = new Vector3(0f; 0f; 0f);
```
```csharp
Vector3.right /* (1, 0, 0)  */
Vector3.left /* (-1, 0, 0)  */
Vector3.up /* (0, 1, 0)  */
Vector3.down /* (0, -1, 0)  */
Vector3.forward /* (0, 0, 1)  */
Vector3.back /* (0, 0, -1) */
Vector3.zero /* (0, 0, 0)  */
Vector3.one /* (1, 1, 1)  */
```
#### Vector 2

```csharp
Vector2.right /* (1, 0)  */
Vector2.left  /* (-1, 0) */
Vector2.up    /* (0, 1)  */
Vector2.down  /* (0, -1) */
Vector2.zero  /* (0, 0)  */
Vector2.one   /* (1, 1)  */
```
If you're just interested the direction of a specific vector, you can access its normalized property like so:
```csharp
myVector.normalized
```
The distance between two vectors can be calculated with the Vector3.Distance() method, which returns a float :
```csharp
float distance = Vector3.Distance(vectorOne, vectorTwo);
```
### Quaternion
Quaternions handle game object rotation. You can check or change the object's rotation using transform.rotation. Unity's Quaternion.LookRotation() function creates a rotation based on a target position.
```csharp
Quaternion.LookRotation(gameObjectPosition);
```
A rotation 30 degrees around the y-axis

```csharp
Quaternion rotation = Quaternion.Euler(0, 30, 0);
```
### Euler Angles
Euler angles are "degree angles" like 90, 180, 45, 30 degrees. Quaternions differ from Euler angles in that they represent a point on a Unit Sphere (the radius is 1 unit).

Create a quaternion that represents 30 degrees about X, 10 degrees about Y
```csharp
Quaternion rotation = Quaternion.Euler(30, 10, 0);
```
Using a Vector
```csharp
Vector3 EulerRotation = new Vector3(30, 10, 0);
Quaternion rotation = Quaternion.Euler(EulerRotation);
```
Convert a transform's Quaternion angles to Euler angles
```csharp
Quaternion quaternionAngles = transform.rotation;
Vector3 eulerAngles = quaternionAngles.eulerAngles;
```
