# Unity

## Unity HUB and Editor

### Hierarchy
- contains all the GameObjects in the current scene.
- the changes to the `GameObject` transform will propagate to the children
  - ie: we move the parent the children also move
- child and parent `GameObject` are treated as one.
- The **frame of reference** of the children `GameObject` is the center of the parent `GameObject`.

### Project Window
- contains all the assets available to your entire project

### Scene
- each level in the game is a different scene
- e.g: Game's main manu is another scene

### Shortcuts:
- ALT + LEFT CLICK = ORBIT (with hand tool)
- ALT + RIGHT CLICK = ZOOM (with hand tool)
- F to focus on a selected GameObject (in cursor mode)
- Q and E to control flight in flying mode
- The camera tools can be accessed with QWERTY (in this order)
- CTRL + D to duplicate gameObjects
- Ctrl+Shift+F to move a gameObject to the current scene view ( the in HUB camera)

### Y-axis is the UP axis

## Important Methods
### Start
 - is used only once when an object is initialized.

### Update
 - is called every frame to figure out where an object needs to be in space and its rotation.
#### Time.deltaTime
 - used in `update()` function.
 - it represents the time between frames.
 - used for frame invariant movement -> multiply with something that needs to change every frame and to keep it consistent regarding of framerate.


### FixedUpdate
 - is called a fixed amount of times (independent of framerate).
 - is used for physics updates.
 - this is where the movements under **physical simulation** must be done.
### Time.fixedDeltaTime
 - used in `fixedUpdate()` function.
 - it represents the time between consecutive physics ticks.

### LateUpdate
 - is called after all `Update()` functions are done.

## Vectors
 - `Vector2` and `Vector3` are used to represent points in space or vectors
   - `Vector2` has x and y components.
   - `Vector3` has x, y and z components.
 - To get direction vectors (unit vectors for pointing in one direction) use the syntax **`Vector3._direction_`**:
   - E.g: `Vector3.Forward;`

## Components
### Transform
 - it contains the following information about the object that is attached to it:
   - Spatial position
   - Rotation
   - Size
 - default measurement unit is **meter**.
 - the **local coordinate system** starts at the **center** of the `GameObject`.
 - to translate the object you can use the following: `Transform.Translate(_vector_)`.

#### Rotation
 - Rotation is done around the axis we mention. The axis we mention acts like a pivot.
 - The value of the rotation is in degrees.

### Rigid Body
 - used to give physical properties.
 - you can freeze `GameObjects` in certain axis to keep objects from falling.

### Material
 - components that define the surface characteristics of objects.

#### Features of the Material
 - `Albedo` specifies the base color of a material.
 - `Texture Map` is a texture that can be applied to the material. This in turns changes the surface of the `GameObject`.
 - `Tiling`represents how many times is the texture repeated
 - `Physic material` changes **friction** and **bounce** but NOT texture.

## Prefabs
 - templates of GameObjects.
 - can create multiple copies called **instances**.

### Instantiation
 - use the `gameObject` field of the `MonoBehaviour` class to get the current attached `GameObject`.
 - use `Destroy(gameObject)` and `Instantiate(gameObject)` to control the instantiation of different `GameObjects`.

### How to use prefabs
 - Dragging a `GameObject` from a scene to a folder makes it a `Prefab`.
 - Dragging a `Prefab` to a scene makes an instance of it ( and marks it with blue in the hierarchy).

### Prefab view
 - To enter the **Prefab view** click on the right-pointing arrow of a `Prefab` in the **Hierarchy**.
   - Here you can change a `Prefab` -> **ALL INSTANCES OF THAT PREFAB WILL BE CHANGED!**

### Overriding properties
 - Instances can override properties so that they differ from the parent `Prefab`.
   - They will be marked with **blue** in the inspector overview.
 - You can change the main `Prefab` by selecting to apply the changes from an instance with **Overrides**.
 - You can create a new `Prefab Variant` by dragging a `Prefab Instance with Overrides` into the folder and select `Prefab Variant`.
 - Prefabs can only find other prefabs by Reference: e.g. by using `GameObject.Find(...)`.

## Scripting
### User input
#### Basic Way
- `Input` class with its static methods return `true` if a certain key was pressed in a frame.
- `GetKey` returns true when the user holds down on the key.

#### Advanced Way - Input Manager
To activate the advanced way: EDIT -> PROJECT SETTINGS -> INPUT MANAGER

Here you can find all the axes, each axis allows movement forwards and backwards on each axis.

To get the direction of a movement in a certain axis use `Input.GetAxis(_axis_name)`. This will return a value between -1 and 1 for that particular axis.

To find the name for a certain axis check the `Input Manger`.

To Add new Keybindings select a greater number at the size of axes in input manager.

#### New Way - Input System 
To be researched.

### From Screen Coordinates to in-game Coordinates
- use `Camera. *cameraName* . ScreenToWorldPoint (*PointCoordinatesInPixels*)` for this conversion.

### Mathf - utility math class for Unity

### Repeating functions
 - `InvokeRepeating (MethodName,StartTime,RepeatingTime)`.
 - To be used only in `start` method.


## Audio
- To add audio you need `Audio Source Component` to be added to a `GameObject`.
- `Audio Clip` is used to add the actual audio  content to the Audio Source.
- `Audio Listener` acts as the ears, it relays to the player whatever it hears.
	- Only 1 can exist inside a Scene.
- `Spatial Blend` set to 1 to make a sound behave 3D ( getting louder as getting closer, etc.).
- `The Rolloff` is used to set how much the sound is getting weaker as you go further.
	- MIN DISTANCE = the area where you can hear the sound at maximum.
	- MAX DISTANCE = the area where you can hear the sound - outside this = no sound.

## Colliders 
 - A collider marked by `IsTrigger` will not interact with physics but will trigger the following methods:
    - `OnTriggerEnter`
    - `OnTriggerStay`
    - `OnTriggerExit`
 - For a trigger collision to register the following must be true:
   - One of the object must be a `Rigid Body`.
   - One of the objects must be a `Trigger`.
 - For collision under physics simulation both objects `MUST NOT` be `Triggers`.
   - OnCollisionEnter
   - OnCollisionStay
   - OnCollisionExit   

## Saving Player data
 - To save data use: `PlayerPrefs`
 - Persists in memory Key,Value pairs