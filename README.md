# Unity_Cheat_Sheet
## Table of Contents
- [Fundamentals](#fundamentals)
  - [Unity Shortcuts](#unity-shortcuts)
  - [MonoBehaviour](#monobehaviour)
  - [Physics Events](#physics-events)
  - [Serializing Variables](#serializing-variables)
  - [Instantiating](#instantiating)
  - [Finding Game Objects](#finding-game-objects)
  - [Destroying Games Objects](#destroying-game-objects)
  - [Components](#components)
  - [Constants](#constants)
  - [Vectors](#vectors)
  - [Quaternion](#quaternion)
  - [Euler Angles](#euler-angles)
- [Movement & Rotation](#movement--rotation)
  - [Move Object](#move-object)
    - [Transform.Translate()](#transformtranslate)
    - [Vector3.MoveTowards()](#vector3movetowards)
    - [Vector3.Lerp()](#vector3lerp)
    - [Vector3.SmoothDamp()](#vector3smoothdamp)
  - [Move 3D Object](#move-3D-object)
    - [Transform.Position()](#transformtposition)
    - [Transform.Translate()](#transformtranslate)
    - [Rigidbody.Velocity()](#rigidbodyvelocity)
    - [Rigidbody.MovePosition()](#rigidbodymoveposition)
    - [Rigidbody.AddForce()](#rigidbodyaddforce)
    - [CharacterController.Move()](#charactercontrollermove)
    - [NavMeshAgent.Move()](#NavMeshAgentmove)
    - [CharacterJoint and Rigidbody.MoveRotation()](#characterjointandrigidbodymoverotation)
    - [SetPosition of Rigidbody2D](#setpositionofrigidbody2d)
    - [Lerp or Slerp](#lerporslerp)
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
  - [Button](#button)
  - [Slider](#slider)
- [Audio](#audio)
  - [Basic Audio Play](#basic-audio-play)
- [Design Patterns](#design-patterns)
  - [Singleton](#singleton)
- [Practical Use Cases](#practical-use-cases)
  - [Keep Screen's Ratio](#keep-screens-ratio)
- [Refernces](#refernces)

 ## Fundamentals

### Unity shortcuts 
  
  | Action                           | Key Binding                                             |
| -------------------------------- | ------------------------------------------------------- |
| View Tool                        |Q                                                        |
| Move Tool                        |W                                                        |
| Rotate Tool                      |E                                                        |
| Scale Tool                       |R                                                        |
| Rect Tool                        |T                                                        |
| Transform Tool                   |Y                                                        |
| New Game Object                  |Windows: CTRL + SHIFT + N <br> Mac: CMD + SHIFT + N      |
| New Child Game Object            |Toggle Window Size                                       |
| Duplicate                        |Windows: CTRL + D <br> Mac: CMD +D                       |
| Play/Pause                       |Windows: CTRL + P <br> Mac: CMD + P                      |
| Focus Game Object                |F                                                        |

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

### Physics Events
If you add a collider component to a game object, you can detect collision events from your components by defining a specific set of methods. The following methods are only called when you have a Collider or Rigid Body component on both game objects.
- OnCollisionEnter - This function is called once when another object has collided with the current game object.
- OnCollisionStay - This function is called on every frame when another object has collided with the current game object.
- OnCollisionExit - This function is called once when an object exits the collision zone of the current object.
```csharp
private void OnCollisionEnter(Collision hit) {
  Debug.Log($"{gameObject.name} hits {hit.gameObject.name}");
}
private void OnCollisionStay(Collision hit) {
  Debug.Log($"{gameObject.name} is hitting {hit.gameObject.name}");
}
private void OnCollisionExit(Collision hit) {
  Debug.Log($"{gameObject.name} stopped hitting {hit.gameObject.name}");
}
```
The following functions are only called when the On Trigger option is turned on from the respective collider component.
- OnTriggerEnter - This function is called when another object has collided with the current game object.
- OnTriggerStay - This function is called on every frame when another object has collided with the current game object.
- OnTriggerExit - This function is called once when an object exits the collision zone of the current object.
```csharp
private void OnTriggerEnter(Collider hit) {
  Debug.Log($"{gameObject.name} hits {hit.gameObject.name}");
}
private void OnTriggerStay(Collider hit) {
  Debug.Log($"{gameObject.name} is hitting {hit.gameObject.name}");
}
private void OnTriggerExit(Collider hit) {
  Debug.Log($"{gameObject.name} stopped hitting {hit.gameObject.name}");
}
```
Lastly, there are counterpart functions for 2D colliders. The functions share the same name as the 3D functions, but have the word 2D appended at the end. The same goes for the parameter's type. It's Collision2D instead of Collision .
- OnCollisionEnter2D
- OnCollisionStay2D
- OnCollisionExit2D
- OnTriggerEnter2D
- OnTriggerStay2D
- OnTriggerExit2D
```csharp
private void OnCollisionEnter2D(Collision2D hit) {
  Debug.Log($"{gameObject.name} hits {hit.gameObject.name}");
}
private void OnCollisionStay2D(Collision2D hit) {
  Debug.Log($"{gameObject.name} is hitting {hit.gameObject.name}");
}
private void OnCollisionExit2D(Collision2D hit) {
  Debug.Log($"{gameObject.name} stopped hitting {hit.gameObject.name}");
}
private void OnTriggerEnter2D(Collision2D hit) {
  Debug.Log($"{gameObject.name} hits {hit.gameObject.name}");
}
private void OnTriggerStay2D(Collision2D hit) {
  Debug.Log($"{gameObject.name} is hitting {hit.gameObject.name}");
}
private void OnTriggerExit2D(Collision2D hit) {
  Debug.Log($"{gameObject.name} stopped hitting {hit.gameObject.name}");
}
```

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
### Euler Angles
```csharp
// Euler angles are "degree angles" like 90, 180, 45, 30 degrees.
// Quaternions differ from Euler angles in that they represent a point on a Unit Sphere (the radius is 1 unit).

// Create a quaternion that represents 30 degrees about X, 10 degrees about Y
Quaternion rotation = Quaternion.Euler(30, 10, 0);

// Using a Vector
Vector3 EulerRotation = new Vector3(30, 10, 0);
Quaternion rotation = Quaternion.Euler(EulerRotation);

// Convert a transform's Quaternion angles to Euler angles
Quaternion quaternionAngles = transform.rotation;
Vector3 eulerAngles = quaternionAngles.eulerAngles;
```

## Movement & Rotation

### Move Object
#### Transform.Translate()
```csharp
// Moves the transform in the direction and distance of translation.
public void Translate(Vector3 translation);
public void Translate(Vector3 translation, Space relativeTo = Space.Self);

transform.Translate(Vector3.right * movementSpeed);
```

#### Vector3.MoveTowards()
```csharp
// Calculate a position between the points specified by current and target
// Moving no farther than the distance specified by maxDistanceDelta
public static Vector3 MoveTowards(Vector3 current, Vector3 target, float maxDistanceDelta);

Vector3 targetPosition;
transform.position = Vector3.MoveTowards(transform.position, targetPosition, Time.deltaTime);
```

#### Vector3.Lerp()
```csharp
// Linearly interpolates between two points. Results in a smooth transition.
public static Vector3 Lerp(Vector3 startValue, Vector3 endValue, float interpolationRatio);

Vector3 targetPosition;
float t = 0;
t += Time.deltaTime * speed;
transform.position = Vector3.Lerp(transform.position, targetPosition, t);
```

#### Vector3.SmoothDamp()
```csharp
// Gradually changes a vector towards a desired goal over time.
// The vector is smoothed by some spring-damper like function, which will never overshoot.
// The most common use is for smoothing a follow camera.
public static Vector3 SmoothDamp(Vector3 current, Vector3 target, ref Vector3 currentVelocity, float smoothTime, float maxSpeed = Mathf.Infinity, float deltaTime = Time.deltaTime);

float smoothTime = 1f;
Vector3 velocity;
Vector3 targetPosition = target.TransformPoint(new Vector3(0, 5, -10));
// Smoothly move the camera towards that target position
transform.position = Vector3.SmoothDamp(transform.position, targetPosition, ref velocity, smoothTime);
```

### Rotate Object
#### Transform.rotation
```csharp
// A Quaternion stores the rotation of the Transform in world space.
// Quaternions are based on complex numbers and don't suffer from gimbal lock.
// Unity internally uses Quaternions to represent all rotations.

transform.rotation = new Quaternion(rotx, roty, rotz, rotw);
```

#### Transform.eulerAngles
```csharp
// Transform.eulerAngles represents rotation in world space. 
// It is important to understand that although you are providing X, Y, and Z rotation values to describe your rotation
// those values are not stored in the rotation. Instead, the X, Y & Z values are converted to the Quaternion's internal format.

transform.eulerAngles = Vector3(rotx, roty, rotz);
```

#### Transform.Rotate()
```csharp
// Applies rotation around all the given axes.
public void Rotate(Vector3 eulers, Space relativeTo = Space.Self);
public void Rotate(float xAngle, float yAngle, float zAngle, Space relativeTo = Space.Self);

transform.Rotate(rotx, roty, rotz);
```

#### Transform.RotateAround()
```csharp
// Rotates the transform about axis passing through point in world coordinates by angle degrees.
public void RotateAround(Vector3 point, Vector3 axis, float angle);

// Spin the object around the target at 20 degrees/second.
Transform target;
transform.RotateAround(target.position, Vector3.up, 20 * Time.deltaTime);
```

#### Transform.LookAt()
```csharp
// Points the positive 'Z' (forward) side of an object at a position in world space.
public void LookAt(Transform target);
public void LookAt(Transform target, Vector3 worldUp = Vector3.up);

// Rotate the object's forward vector to point at the target Transform.
Transform target;
transform.LookAt(target);

// Same as above, but setting the worldUp parameter to Vector3.left in this example turns the object on its side.
transform.LookAt(target, Vector3.left);
```

#### Quaternion.LookRotation()
```csharp
// Creates a rotation with the specified forward and upwards directions.
public static Quaternion LookRotation(Vector3 forward, Vector3 upwards = Vector3.up);

// The following code rotates the object towards a target object.
Vector3 direction = target.position - transform.position;
Quaternion rotation = Quaternion.LookRotation(direction);
transform.rotation = rotation;
```

#### Quaternion.FromToRotation()
```csharp
// Creates a rotation (a Quaternion) which rotates from fromDirection to toDirection.
public static Quaternion FromToRotation(Vector3 fromDirection, Vector3 toDirection);

// Sets the rotation so that the transform's y-axis goes along the z-axis.
transform.rotation = Quaternion.FromToRotation(Vector3.up, transform.forward);
```

#### Quaternion.ToAngleAxis()
```csharp
// Converts a rotation to angle-axis representation (angles in degrees).
// In other words, extracts the angle as well as the axis that this quaternion represents.
public void ToAngleAxis(out float angle, out Vector3 axis);

// Extracts the angle - axis rotation from the transform rotation
float angle = 0.0f;
Vector3 axis = Vector3.zero;
transform.rotation.ToAngleAxis(out angle, out axis);
```
## Input

### Keyboard

```csharp
// Returns true during the frame the user starts pressing down the key
if (Input.GetKeyDown(KeyCode.Space)) {
    Debug.Log("Space key was pressed");
}

// Jump is also set to space in Input Manager
if (Input.GetButtonDown("Jump")) {
    Debug.Log("Do something");
}
```

### Mouse

```csharp
if (Input.GetAxis("Mouse X") < 0) {
    Debug.Log("Mouse moved left");
}

if (Input.GetAxis("Mouse Y") > 0) {
    Debug.Log("Mouse moved up");
}

if (Input.GetMouseButtonDown(0)) {
    Debug.Log("Pressed primary button.");
}

if (Input.GetMouseButtonDown(1)) {
    Debug.Log("Pressed secondary button.");
}

if (Input.GetMouseButtonDown(2)) {
    Debug.Log("Pressed middle click.");
}
```

### Touch
```csharp
if (Input.touchCount > 0) {
    touch = Input.GetTouch(0);

    if (touch.phase == TouchPhase.Began) {
        Debug.Log("Touch began");
    }

    if (touch.phase == TouchPhase.Moved) {
        Debug.Log("Touch moves");
    }

    if (touch.phase == TouchPhase.Ended) {
        Debug.Log("Touch ended");
    }
}
```

## UI


```csharp
// Button is used to handle user clicks and interactions.
// Attach this script to a Button component to respond to button clicks.

using UnityEngine.UI;

Button myButton = GetComponent<Button>();
myButton.onClick.AddListener(MyButtonClickHandler);

void MyButtonClickHandler() {
    Debug.Log("Button Clicked!");
}
```

### Button

```csharp
// Button is used to handle user clicks and interactions.
// Attach this script to a Button component to respond to button clicks.

using UnityEngine.UI;

Button myButton = GetComponent<Button>();
myButton.onClick.AddListener(MyButtonClickHandler);

void MyButtonClickHandler() {
    Debug.Log("Button Clicked!");
}
```

### Slider
```csharp
// Slider is used for selecting a value within a range.
// Attach this script to a Slider component to respond to value changes.

using UnityEngine.UI;

Slider mySlider = GetComponent<Slider>();
mySlider.onValueChanged.AddListener(MySliderValueChangedHandler);

void MySliderValueChangedHandler(float value) {
    Debug.Log("Slider Value: " + value);
}
```

## Audio

### Basic Audio Play

```csharp
public class PlayAudio : MonoBehaviour {
    public AudioSource audioSource;

    void Start() {
        // Calling Play on an Audio Source that is already playing will make it start from the beginning
        audioSource.Play();
    }
}
```


## Design Patterns
### Singleton

```csharp
// Define singleton class
public class SingletonClass: MonoBehaviour {
    private static SomeClass instance;

    public static SomeClass Instance { get { return instance; } }

    private void Awake() {
        if (instance != null && instance != this) {
            Destroy(this.gameObject);
        } else {
            instance = this;
        }
    }
}

// Use it in another class
public class AnotherClass: MonoBehaviour {
    public Singleton instance;

    private void Awake() {
       instance = Singleton.Instance;
    }
}
```
### Practical Use Cases
### Keep Screen's Ratio
```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ScaleBackground : MonoBehaviour
{
    private SpriteRenderer background;
    private Camera cam;

    void Start()
    {
        background = GetComponent<SpriteRenderer>();
        cam = Camera.main;

        // Get the size of the camera
        float cameraHeight = 2f * cam.orthographicSize;
        float cameraWidth = cameraHeight * cam.aspect;

        // Get the size of the current background
        float bgHeight = background.sprite.bounds.size.y;
        float bgWidth = background.sprite.bounds.size.x;

        // Calculate the scale ratio
        float scaleX = cameraWidth / bgWidth;
        float scaleY = cameraHeight / bgHeight;

        // Apply the scale ratio to the background
        transform.localScale = new Vector3(scaleX, scaleY, 1f);
    }
  }
}
```

### References 
LUIS RAMIREZ JR. (Unity Game Development Cheat Sheet)

Ozan Kaşıkçı (Unity Cheat Sheet)
