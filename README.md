# The-code

[Uploading FlashLight.cs…]()using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class FlashLight : MonoBehaviour
{
    public GameObject light;
    public bool toggle;
    public AudioSource toggleSound;

    void Start()
    {
        if(toggle == false)
        {
            light.SetActive(false);
        }
        if (toggle == true)
        {
            light.SetActive(true);
        }
    }
    
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.F))
        {
            toggle = !toggle;
            //toggleSound.Play();
            if(toggle == false)
            {
                light.SetActive(false);
            }
            if (toggle == true)
            {
                light.SetActive(true);
            }
        }
    }
}



The video: 
https://github.com/Tom1056/The-code-/assets/150391192/c4946598-8e6f-4668-8672-7bd042e17533

The video that helped me:
https://youtu.be/HAPILQXbG2s?si=-H9IIAOqkKJ2cSPv
