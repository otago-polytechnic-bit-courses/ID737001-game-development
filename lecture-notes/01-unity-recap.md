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

What is the **Universal Render Pipeline (URP)**? The **Universal Render Pipeline (URP)** is a prebuilt **Scriptable Render Pipeline**, made by Unity. It is optimised for performance and is designed to be used on all platforms. It is a great choice for 2D games.

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

Why do you need to restart Unity? The Input System package requires a restart to be fully installed.

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

What is the **Sprite Renderer** component? The **Sprite Renderer** component renders the sprite on the screen. It is a required component for any object that uses a sprite.

5. Repeat the process for the **Background Two** object.

![](../resources/img/01/05-background/05.png)

6. Again, repeat the process for the **Background Three** object.

![](../resources/img/01/05-background/06.png)

Pay careful attention to the **Order in Layer** property of the **Sprite Renderer** component. This property determines the order in which the sprites are rendered. The higher the value, the further back the sprite will be rendered.

## Player

1. Create a new **GameObject** called **Player**. Add a **Sprite Renderer** component to the **Player** object. Set the **Sprite** property to an appropriate player sprite. These can be found in the **Art > Adventurer** directory. Also, add a **Rigidbody 2D** component to the **Player** object.

![](../resources/img/01/06-player/01.png)

What is the **Rigidbody 2D** component? The **Rigidbody 2D** component is a physics component that allows the object to be affected by forces and collisions. It is a required component for any object that uses physics.

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

    public bool IsMoving {
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

6. Add a **Player Input** component to the **Player** object. This component is used to handle input from the player.

![](../resources/img/01/06-player/05.png)

7. Click on **Create Actions...** to create a new input actions asset. Name it **PlayerInputActions**. This should be saved in the **Assets > Characters > Player** directory. This asset will contain the input actions for the player.

![](../resources/img/01/06-player/06.png)

8. Change **Fire** to **Attack**.

![](../resources/img/01/06-player/07.png)

9. In the **Player Input** component, set the **Actions** property to the **PlayerInputActions** asset.

![](../resources/img/01/06-player/08.png)

10. Apply the **PlayerController.cs** script to the **Player** object.

![](../resources/img/01/06-player/09.png)

11. In the **Player Input** component, set the **Events > Player > Move** property to the **PlayerController > OnMove** method.

![](../resources/img/01/06-player/10.png)

## Camera

1. In the **Hierarchy** window, create a new **2D Camera** called **Virtual Camera**. 

![](../resources/img/01/07-camera/01.png)

2. Add a **Cinemachine Pixel Perfect** component to the **Virtual Camera** object. This component is used to make the camera pixel perfect meaning the camera will render the pixels in the game at the correct size.

![](../resources/img/01/07-camera/02.png)

3. Make sure the **Transform** component of the **Virtual Camera** object's **Position** property is set to **(0, 0, -10)**.

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
        startingPosition = transform.position;
        startingZ = transform.position.z;
    }

    // Update is called once per frame
    void Update()
    {
        Vector2 newPosition = startingPosition + cameraMoveSinceStart * parallaxFactor;
        transform.position = new Vector3(newPosition.x, newPosition.y, startingZ);
    }
}
```