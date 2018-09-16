using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerMovementController : MonoBehaviour {



    public Vector3 startPosition;
    public Vector3 startRotation;
    public float movementSpeed = 20;
    public float rotationSpeed = 45;
    public float throttle;

	private void Start () {
        this.transform.SetPositionAndRotation(startPosition, Quaternion.Euler(startRotation));
	}
	
	private void Update() {
        if (Input.GetKey(KeyCode.W)) {
            transform.Rotate(new Vector3(1, 0, 0) * Time.deltaTime * rotationSpeed, Space.Self);
        }
        if (Input.GetKey(KeyCode.S)) {
            transform.Rotate(new Vector3(-1, 0, 0) * Time.deltaTime * rotationSpeed, Space.Self);
        }
        if (Input.GetKey(KeyCode.D)) {
            transform.Rotate(new Vector3(0, 1, 0) * Time.deltaTime * rotationSpeed, Space.Self);
        }
        if (Input.GetKey(KeyCode.A)) {
            transform.Rotate(new Vector3(0, -1, 0) * Time.deltaTime * rotationSpeed, Space.Self);
        }
        if (Input.GetKey(KeyCode.Q)) {
            transform.Rotate(new Vector3(0, 0, 1) * Time.deltaTime * rotationSpeed, Space.Self);
        }
        if (Input.GetKey(KeyCode.E)) {
            transform.Rotate(new Vector3(0, 0, -1) * Time.deltaTime * rotationSpeed, Space.Self);
        }
        if(Input.GetKey(KeyCode.LeftShift)) {
            throttle += 1.0f;
            if (throttle > 100f) throttle = 100f;
        }
        if (Input.GetKey(KeyCode.LeftControl))
        {
            throttle -= 1.0f;
            if (throttle < 0f) throttle = 0f;
        }
        if (Input.GetKey(KeyCode.Z))
        {
            throttle = 0f;
            if (throttle < 0f) throttle = 0f;
        }
    }

    private void FixedUpdate() { //anything and everything physics related must go here or you will die
        if(throttle > 0)
        {
            transform.Translate(Vector3.forward * Time.deltaTime * ((throttle / 100) * 100));
        }
    }
}
