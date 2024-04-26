# LookAtCamera
LookAtCamera Unity for UI
```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class UILookAt : MonoBehaviour
{
    public bool lockYRotation = true; 
    public Vector3 positionOffset; 
    Transform mainCamera; 

    private void Start()
    {
        mainCamera = Camera.main.transform;
    }

    void Update()
    {
        Vector3 directionToCamera = mainCamera.position - transform.position;
        directionToCamera.y = 0; // Nolkan nilai sumbu y untuk menghilangkan rotasi pada sumbu y
        if (directionToCamera != Vector3.zero)
        {
            Quaternion targetRotation = Quaternion.LookRotation(directionToCamera);

            transform.eulerAngles = new Vector3(
              lockYRotation ? 0f : targetRotation.eulerAngles.x, // Atur rotasi x berdasarkan lockYRotation
              targetRotation.eulerAngles.y, // Pertahankan rotasi y dari targetRotation
              0f); // Nolkan rotasi z
            transform.eulerAngles += positionOffset; // Tambahkan offset ke rotasi akhir
        }
    }
}
```
