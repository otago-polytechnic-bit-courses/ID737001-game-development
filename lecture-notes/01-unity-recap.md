# 01: Unity Recap

In this lecture, we will cover a variety of topics while building the foundations of a 2D platformer game. You will later extend this game in the **Project: Game Development + Demo** assessment.

## GitHub Repository

## Setting up a Unity project

1. Click on the **New Project** button in the Unity Hub.

![](../resources/img/01/01-setting-up-a-unity-project/01.png)

2. Select **2D (URP)** as the template for the project. Name the project and select the location of the repository to save the project.

![](../resources/img/01/01-setting-up-a-unity-project/02.png)

3. The project will open in Unity. You can now start working on the project.

![](../resources/img/01/01-setting-up-a-unity-project/03.png)

The **Universal Render Pipeline (URP)** is a prebuilt **Scriptable Render Pipeline**, made by Unity. It is optimised for performance and is designed to be used on all platforms. It is a great choice for 2D games.

## Texture Importer Preset

When importing textures into Unity, you can use the **Texture Importer Preset** to set the default settings for the texture. This is useful if you want to set the default settings for all textures in the project. In this project, you will use textures that are 16x16 in size.

1. Click on **Edit > Project Settings** to open the Project Settings window.

![](../resources/img/01/02-texture-importer-preset/01.png)

2. Click on **Preset Manager > Add Default Preset > TextureImporter** to add a new preset for the texture importer.

![](../resources/img/01/02-texture-importer-preset/02.png)

3. In the **Assets** directory, add a new texture. In this example, we will use a 16x16 texture.

![](../resources/img/01/02-texture-importer-preset/03.png)

4. Click on the texture to open the **Inspector** window. Configure as follows:

![](../resources/img/01/02-texture-importer-preset/04.png)

Click on **Apply** to apply the changes to the texture.

5. In the **Assets** directory, create a new directory called **Presets**.

![](../resources/img/01/02-texture-importer-preset/05.png)

6. Click on **Select Preset > Create new Preset...**. Name the preset and save it in the **Presets** directory.

![](../resources/img/01/02-texture-importer-preset/06.png)

In the **Presets** directory, you will see the preset file. You can now use this preset to set the default settings for all textures in the project.

![](../resources/img/01/02-texture-importer-preset/07.png)

## Adding Assets

In the **assessments > project-game-development-demo** directory, you will find two directories called **Art** and **UI**. Copy the contents of these directories into the **Assets** directory. Feel free to add any additional assets you want to use.

![](../resources/img/01/03-adding-assets/01.png)

## Cinemachine

**Cinemachine** is a powerful and flexible camera system for Unity. It is a free package that you can install from the Unity Package Manager.

1. Navigate to the **Window > Package Manager** window.

![](../resources/img/01/04-cinemachine-and-input-system/01.png)

2. Search for **Cinemachine** and install the package.

![](../resources/img/01/04-cinemachine-and-input-system/02.png)

![](../resources/img/01/04-cinemachine-and-input-system/03.png)

**Resource:** <https://docs.unity3d.com/Packages/com.unity.cinemachine@3.0/manual/index.html>

## Input System

The **Input System** is a package that provides an easy way to manage input in Unity. Inputs include keyboard, mouse and gamepad. It is a free package that you can install from the Unity Package Manager.

1. Search for **Input System** and install the package.

![](../resources/img/01/04-cinemachine-and-input-system/04.png)

2. You will be prompted to restart Unity. Click on **Yes** to restart Unity.

![](../resources/img/01/04-cinemachine-and-input-system/05.png)

The Input System package requires a restart to be fully installed.

**Resource:** <https://docs.unity3d.com/Packages/com.unity.inputsystem@1.8/manual/index.html>

## Background

1. In the **Art** directory, you will find a directory called **Tilesets**. This directory contains the backgrounds, individual tiles and props.

![](../resources/img/01/05-background/01.png)

2. In the **Scenes** directory, rename the **SampleScene** to **GameplayScene**.

![](../resources/img/01/05-background/02.png)

3. Create a new **GameObject** called **Background**. This will be the parent object for the backgrounds.

![](../resources/img/01/05-background/03.png)

4. Inside the **Background** object, create a new **GameObject** called **Background One**. Add a **Sprite Renderer** component to the **Background One** object. Set the **Sprite** property to an appropriate background sprite. These can be found in the **Tilesets > Backgrounds** directory.

![](../resources/img/01/05-background/04.png)

The **Sprite Renderer** component renders the sprite on the screen. It is a required component for any object that uses a sprite.

5. Repeat the process for the **Background Two** object.

![](../resources/img/01/05-background/05.png)

6. Again, repeat the process for the **Background Three** object.

![](../resources/img/01/05-background/06.png)

Pay careful attention to the **Order in Layer** property of the **Sprite Renderer** component. This property determines the order in which the sprites are rendered. The higher the value, the further back the sprite will be rendered.

## Player

1. Create a new **GameObject** called **Player**. Add a **Sprite Renderer** component to the **Player** object. Set the **Sprite** property to an appropriate player sprite. These can be found in the **Art > Adventurer** directory. Also, add a **Rigidbody 2D** component to the **Player** object.

![](../resources/img/01/06-player/01.png)

The **Rigidbody 2D** component is a physics component that allows the object to be affected by forces and collisions. It is a required component for any object that uses physics.

2. In the **Assets** directory, create a new directory called **Characters**. In the **Characters** directory, create two new directories called **Enemies** and **Player**.

![](../resources/img/01/06-player/02.png)

3. In the **Player** directory, create a **Prefab** of the **Player** object. This will allow you to reuse the player object.

![](../resources/img/01/06-player/03.png)

4. In the **Assets > Scripts** directory, create a new script called **PlayerController.cs**.

![](../resources/img/01/06-player/04.png)

5. Open the **PlayerController.cs** script and add the following code:

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.InputSystem;

[RequireComponent(typeof(Rigidbody2D))]
public class PlayerController : MonoBehaviour
{
    Vector2 moveInput;
    Rigidbody2D rb;

    public float walkSpeed = 5f;

    [SerializeField]
    private bool _isMoving = false;

    public bool IsMoving 
    {
        get { return _isMoving; }
        set { _isMoving = value; }
    }

    private void Awake()
    {
        // Get the Rigidbody2D component
        rb = GetComponent<Rigidbody2D>();
    }

    // Start is called before the first frame update
    void Start() {}

    // Update is called once per frame
    void Update() {}

    private void FixedUpdate()
    {
        // Move the player
        rb.velocity = new Vector2(moveInput.x * walkSpeed, rb.velocity.y);
    }

    // This event will be called when the player moves
    public void OnMove(InputAction.CallbackContext context)
    {
        // Get the move input
        moveInput = context.ReadValue<Vector2>();

        // Set the is moving flag
        IsMoving = moveInput != Vector2.zero;
    }
}
```

6. Add a **Player Input** component to the **Player**. This component is used to handle input from the player.

![](../resources/img/01/06-player/05.png)

7. Click on **Create Actions...** to create a new input actions asset. Name it **PlayerInputActions**. This should be saved in the **Assets > Characters > Player** directory. This asset will contain the input actions for the player.

![](../resources/img/01/06-player/06.png)

8. Change **Fire** to **Attack**.

![](../resources/img/01/06-player/07.png)

9. In the **Player Input** component, set the **Actions** property to the **PlayerInputActions** asset.

![](../resources/img/01/06-player/08.png)

10. Apply the **PlayerController.cs** script to the **Player**.

![](../resources/img/01/06-player/09.png)

11. In the **Player Input** component, set the **Events > Player > Move** property to the **PlayerController > OnMove** method.

![](../resources/img/01/06-player/10.png)

## Camera

1. In the **Hierarchy** window, create a new **2D Camera** called **Virtual Camera**.

![](../resources/img/01/07-camera/01.png)

2. Add a **Cinemachine Pixel Perfect** component to the **Virtual Camera** object. This component is used to make the camera pixel perfect meaning the camera will render the pixels in the game at the correct size.

![](../resources/img/01/07-camera/02.png)

3. Make sure the **Transform** component of the **Virtual Camera** object's **Position** property is set to **(0, 0, -10)**.

![](../resources/img/01/07-camera/03.png)

## Parallax Effect

**Parallax Effect** is a technique used in 2D games to create the illusion of depth by moving the background at a different speed than the foreground. This creates a sense of depth and immersion in the game.

1. In the **Assets > Scripts** directory, create a new script called **ParallaxEffect.cs**. Add the following code to the script:

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ParallaxEffect : MonoBehaviour
{
    public Camera camera;
    public Transform target;

    Vector2 startPosition;
    float startingZ;

    Vector2 cameraMoveSinceStart => (Vector2)camera.transform.position - startPosition;
    float zDistanceFromTarget => transform.position.z - target.transform.position.z;
    float clippingPlane => (camera.transform.position.z + (zDistanceFromTarget > 0 ? camera.farClipPlane : camera.nearClipPlane));
    float parallaxFactor => Mathf.Abs(zDistanceFromTarget) / clippingPlane;

    // Start is called before the first frame update
    void Start()
    {
        startingPos = transform.position;
        startingZ = transform.position.z;
    }

    // Update is called once per frame
    void Update()
    {
        Vector2 newPosition = startingPos + cameraMoveSinceStart * parallaxFactor;
        transform.position = new Vector3(newPosition.x, newPosition.y, startingZ);
    }
}
```

2. Apply the **ParallaxEffect.cs** script to the **Background One** object.

![](../resources/img/01/08-parallax-effect/01.png)

3. Repeat the process for the **Background Two** object.

![](../resources/img/01/08-parallax-effect/02.png)

4. Again, repeat the process for the **Background Three** object.

![](../resources/img/01/08-parallax-effect/03.png)

## Animator

**Animator** is a powerful tool in Unity that allows you to create animations for your game. It is used to animate the player, enemies, backgrounds and more.

1. Apply the **Animator** component to the **Player**.

![](../resources/img/01/09-animator/01.png)

2. In the **Assets > Characters > Player** directory, create a new **Animator Controller** called **PlayerAnimationController**. This will be used to control the animations.

![](../resources/img/01/09-animator/02.png)

3. In the **Animator** component, set the **Controller** property to the **PlayerAnimationController**.

![](../resources/img/01/09-animator/03.png)

4. Open the **Animation** window by clicking on **Window > Animation > Animation**.

![](../resources/img/01/09-animator/04.png)

5. Click the **Create** button to create a new animation.

![](../resources/img/01/09-animator/05.png)

6. You should see the following **Animation** window. Create a new **Animation Clip** called **PlayerIdleAnimation**. This will be used to animate the player when they are idle.

![](../resources/img/01/09-animator/06.png)

7. Show the sample rate by clicking on the **Show Sample Rate**. This will show the sample rate of the animation.

![](../resources/img/01/09-animator/07.png)

8. Set the sample rate to 10. This means that the animation will play at 10 frames per second.

![](../resources/img/01/09-animator/08.png)

9. Drag and drop the following sprites into the **Dopesheet**:
   - adventurer-idle-0
   - adventurer-idle-1
   - adventurer-idle-2
   - adventurer-idle-3

The **Dopesheet** is a timeline that shows the keyframes of the animation.

![](../resources/img/01/09-animator/09.png)

10. Create two more animations called **PlayerWalkAnimation** and **PlayerRunAnimation**. These will be used to animate the player when they are walking and running.

![](../resources/img/01/09-animator/10.png)

11. In the **Animator** window, create a new **Sub-State Machine** called **GroundStates**. This will be used to control the ground states of the player.

A **Sub-State Machine** is a state machine that is nested inside another state machine. It is used to organise the states of the animator.

![](../resources/img/01/09-animator/11.png)

12. Drag and drop the **PlayerIdleAnimation**, **PlayerWalkAnimation** and **PlayerRunAnimation** into the **GroundStates**.

![](../resources/img/01/09-animator/12.png)

13. In the **GroundStates**, set the **PlayerIdleAnimation** as the **Layer Default State**.

![](../resources/img/01/09-animator/13.png)

14. Create two new **Parameters** called **IsMoving** and **IsRunning**. Right-click on **PlayerIdleAnimation** and select **Make Transition**. Drag the arrow to **PlayerRunAnimation**. Add the **IsMoving** and **IsRunning** parameters in the **Conditions**. Set the **IsMoving** and **IsRunning** to **true**.

![](../resources/img/01/09-animator/14.png)

15. Right-click on **PlayerIdleAnimation** and select **Make Transition**. Drag the arrow to **PlayerWalkAnimation**. Add the **IsMoving** and **IsRunning** parameters in the **Conditions**. Set the **IsMoving** to **true** and **IsRunning** to **false**.

![](../resources/img/01/09-animator/15.png)

16. Right-click on **PlayerRunAnimation** and select **Make Transition**. Drag the arrow to **PlayerIdleAnimation**. Add the **IsMoving** parameter in the **Conditions**. Set the **IsMoving** to **false**. Repeat the process for the **PlayerWalkAnimation**.

![](../resources/img/01/09-animator/16.png)

17. Right-click on **PlayerWalkAnimation** and select **Make Transition**. Drag the arrow to **PlayerRunAnimation**. Add the **IsRunning** parameter in the **Conditions**. Set the **IsRunning** to **true**.

![](../resources/img/01/09-animator/17.png)

18. Right-click on **PlayerRunAnimation** and select **Make Transition**. Drag the arrow to **PlayerWalkAnimation**. Add the **IsRunning** parameter in the **Conditions**. Set the **IsRunning** to **false**.

![](../resources/img/01/09-animator/18.png)

19. In the **PlayerInputActions** asset, create a new action called **Run**. Set the **Binding > Path** to **Left Shift [Keyboard]**.

![](../resources/img/01/09-animator/19.png)

20. In the **PlayerController.cs** script, add the following code:

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.InputSystem;

[RequireComponent(typeof(Rigidbody2D))]
public class PlayerController : MonoBehaviour
{
    Vector2 moveInput;
    Rigidbody2D rb;
    Animator anim;

    public float walkSpeed = 5f;

    [SerializeField]
    private bool _isMoving = false;
    [SerializeField]
    private bool _isRunning = false;

    public bool IsMoving 
    {
        get { return _isMoving; }
        set
        {
            _isMoving = value;
            animator.SetBool("isMoving", value);
        }
    }

    public bool IsRunning 
    {
        get { return _isRunning; }
        set
        {
            _isRunning = value;
            animator.SetBool("isRunning", value);
        }
    }

    private void Awake()
    {
        rb = GetComponent<Rigidbody2D>();

        // Get the Animator component
        animator = GetComponent<Animator>();
    }

    // ...

    public void OnRun(InputAction.CallbackContext context)
    {
        if (context.started)
        {
            IsRunning = true;
        }
        else if (context.canceled)
        {
            IsRunning = false;
        }
    }
}
```

21. In the **Player Input** component, set the **Events > Player > Run** property to the **PlayerController > OnMove** method.

![](../resources/img/01/06-player/20.png)

22. Run the game and test the animations. You will notice that the player will animate when they are idle, walking and running. However, the animations for moving left is not working correctly. This is because the player is not flipping when moving left.

**Task:** Currently, the player walks and runs at the same speed. Update the **PlayerController.cs** script to make the player run faster when the **IsRunning** parameter is set to **true**.

## Flip Sprite

In the **PlayerController.cs** script, add the following code to flip the player sprite when moving left:

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.InputSystem;

[RequireComponent(typeof(Rigidbody2D))]
public class PlayerController : MonoBehaviour
{
    // ...

    [SerializeField]
    private bool _IsMovingRight = true;

    // ...

    public bool IsMovingRight 
    {
        get { return _IsMovingRight; }
        set
        {
            if (_IsMovingRight != value)
            {
                transform.localScale *= new Vector2(-1, 1);
            }
            _IsMovingRight = value;
        }
    }

    //...

    private void SetDirection(Vector2 moveInput)
    {
        if (moveInput.x > 0 && !IsMovingRight)
        {
            IsMovingRight = true;
        }
        else if (moveInput.x < 0 && IsMovingRight)
        {
            IsMovingRight = false;
        }
    }

    public void OnMove(InputAction.CallbackContext context)
    {
        moveInput = context.ReadValue<Vector2>();
        IsMoving = moveInput != Vector2.zero;
        SetDirection(moveInput);
    }

    // ...
}
```

`transform.localScale *= new Vector2(-1, 1);` is used to flip the player sprite. The `IsMovingRight` property is used to determine if the player is moving right or left.

## Tilemap

**Tilemap** is a system used to create 2D tile-based maps. It is used to create the ground, walls, platforms and more.

1. Open the tile palette by clicking on **Window > 2D > Tile Palette**.

![](../resources/img/01/10-tilemap/01.png)

2. Go to the **spritesheet** file in the **Assets > Art > Tilesets** directory. Change the **Sprite Mode** to **Multiple** and click on **Sprite Editor**.

![](../resources/img/01/10-tilemap/02.png)

3. We want to slice the **spritesheet** file into individual tiles. Click on **Slice** and set the **Type** to **Grid by Cell Size**. Set the **Pixel Size** to **16x16**. Click on **Slice** to slice the spritesheet into individual tiles. 

![](../resources/img/01/10-tilemap/03.png)

![](../resources/img/01/10-tilemap/04.png)

4. In the **Tile Palette** window, click on **Create New Palette**. Name the palette **Main Palette** and save it in the **Assets > Art > Palette** directory. **Note:** You have to create a new directory called **Palette** in the **Art** directory.

![](../resources/img/01/10-tilemap/05.png)

![](../resources/img/01/10-tilemap/06.png)

5. The **Main Palette** will be created. Drag and drop **spritesheet** file into the palette. These will be the tiles that you will use to create the map.

![](../resources/img/01/10-tilemap/07.png)

6. In the **Hierarchy** window, create a new **2D Object > Tilemap > Rectangular**. This should create a **Grid** and a **Tilemap** object. Rename the **Tilemap** object to **Tilemap**.

![](../resources/img/01/10-tilemap/08.png)

![](../resources/img/01/10-tilemap/09.png)

7. Using the **Tile Palette**, paint the tiles on the **Tilemap** object. 

![](../resources/img/01/10-tilemap/10.png)

8. In the **Player > Rigidbody 2D**, set the **Gravity Scale** to **1**. This will make the player fall to the ground.

![](../resources/img/01/10-tilemap/11.png)

9. Add a **Capsule Collider 2D** component to the **Player**. Edit the **Offset** and **Size** properties to fit the player.

![](../resources/img/01/10-tilemap/12.png)

10. Add a **Composite Collider 2D** and **Tilemap Collider 2D** component to the **Tilemap**. This will allow the player to collide with the tiles.

![](../resources/img/01/10-tilemap/13.png)

11. Play around with the tiles to create the ground, walls and platforms.

![](../resources/img/01/10-tilemap/14.png)

12. In the **Grid** object, create a new **2D Object > Tilemap > Rectangular**. Rename the **Tilemap** object to **No Collision Tilemap**. This **tilemap** will be useful for tiles that the player can go through.

![](../resources/img/01/10-tilemap/15.png)

## Air States

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TouchController : MonoBehaviour
{
    Animator anim;
    CapsuleCollider2D cc;
    RaycastHit2D[] groundHits = new RaycastHit2D[5];

    public ContactFilter2D contactFilter;
    public float groundDistance = 0.5f;

    [SerializeField]
    private bool _isGrounded = false;

    public bool IsGrounded 
    {
        get { return _isGrounded; }
        set 
        { 
            _isGrounded = value; 
            anim.SetBool("isGrounded", value);
        }
    }

    private void Awake() 
    {
        anim = GetComponent<Animator>();
        cc = GetComponent<CapsuleCollider2D>();
    }

    // ... 

    private void FixedUpdate() 
    {
        IsGrounded = cc.Cast(Vector2.down, contactFilter, groundHits, groundDistance) > 0;
    }
}
```