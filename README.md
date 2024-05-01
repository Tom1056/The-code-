# The-code-
Working flashlight (does not seem to work)
using System.Collections;
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

#Picking up a flashlight (does not seem to work)
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class pickupFlashlight : MonoBehaviour
{
    public GameObject inttext, flashlight_table, flashlight_hand;
    public AudioSource pickup;
    public bool interactable;
 void OnTriggerStay(Collider other)
    {
        if (other.CompareTag("MainCamera"))
        {
            inttext.SetActive(true);
            interactable = true;
        }
    }
    void OnTriggerExit(Collider other)
    {
        if (other.CompareTag("MainCamera"))
        {
            inttext.SetActive(false);
            interactable = false;
        }
    }
    void Update()
    {
        if(interactable == true)
        {
            if (Input.GetKeyDown(KeyCode.E))
            {
                inttext.SetActive(false);
                interactable = false;
                //pickup.Play();
                flashlight_hand.SetActive(true);
                flashlight_table.SetActive(false);
            }
        }
    }
}

#Walking and jumping (only program that would work)
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SC_FPSController : MonoBehaviour
{
    public float walkingSpeed = 7.5f;
    public float runningSpeed = 11.5f;
    public float jumpSpeed = 8.0f;
    public float gravity = 20.0f;
    public Camera playerCamera;
    public float lookSpeed = 2.0f;
    public float lookXLimit = 45.0f;
  CharacterController characterController;
    Vector3 moveDirection = Vector3.zero;
    float rotationX = 0;
   [HideInInspector]
    public bool canMove = true;
   void Start()
    {
        characterController = GetComponent<CharacterController>();
        Cursor.lockState = CursorLockMode.Locked;
        Cursor.visible = false;
    }
    void Update()
    {
        Vector3 forward = transform.TransformDirection(Vector3.forward);
        Vector3 right = transform.TransformDirection(Vector3.right);
        // Press Left Shift to run
        bool isRunning = Input.GetKey(KeyCode.LeftShift);
        float curSpeedX = canMove ? (isRunning ? runningSpeed : walkingSpeed) * Input.GetAxis("Vertical") : 0;
        float curSpeedY = canMove ? (isRunning ? runningSpeed : walkingSpeed) * Input.GetAxis("Horizontal") : 0;
        float movementDirectionY = moveDirection.y;
        moveDirection = (forward * curSpeedX) + (right * curSpeedY);
        if (Input.GetButton("Jump") && canMove && characterController.isGrounded)
        {
            moveDirection.y = jumpSpeed;
        }
        else
        {
            moveDirection.y = movementDirectionY;
        }
        if (!characterController.isGrounded)
        {
            moveDirection.y -= gravity * Time.deltaTime;
        }
        characterController.Move(moveDirection * Time.deltaTime);
        if (canMove)
        {
            rotationX += -Input.GetAxis("Mouse Y") * lookSpeed;
            rotationX = Mathf.Clamp(rotationX, -lookXLimit, lookXLimit);
            playerCamera.transform.localRotation = Quaternion.Euler(rotationX, 0, 0);
            transform.rotation *= Quaternion.Euler(0, Input.GetAxis("Mouse X") * lookSpeed, 0);
        }
    }
}

#Tigger to make a jumpscare for a bit (Does not work)
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class scaryEventTrigger : MonoBehaviour
{
    public GameObject scare;
    public Collider collision;
    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            scare.SetActive(true);
            //scareSound.Play();
            collision.enabled = false;
        }
    }
}

The video: 
https://github.com/Tom1056/The-code-/assets/150391192/c4946598-8e6f-4668-8672-7bd042e17533
