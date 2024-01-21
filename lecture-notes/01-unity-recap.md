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

![](../resources/img/01/02-texture-importer-preset/07.png)



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
    
    public bool IsMoving { get; private set; }

    private void Awake()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        
    }

    private void FixedUpdate() 
    {
        rb.velocity = new Vector2(moveInput.x * walkSpeed, rb.velocity.y);
    }

    public void OnMove(InputAction.CallbackContext context)
    {
        moveInput = context.ReadValue<Vector2>();
        IsMoving = moveInput != Vector2.zero;
    } 
}
```

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