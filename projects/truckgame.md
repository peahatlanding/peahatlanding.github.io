---
layout: projects
comments: false
title:  "The Truck Game"
anchor: #truckgame

---

# The Truck Game

*Tools:* Unity 3D, Blender, C#

I tried my hand at  making a low poly 3D game. I started by working through [Unity 3d's Roll-a-Ball tutorial], then modified the Roll-a-Ball game with different 3D models and scripts.

Features:

 - Arrow key and WASD control of the truck.
 - Boxes that rotate and can be picked up.
 - Score-keeping.

## Scripts

I used these scripts to control each object's behavior. Unity 3D is a great way to practice coding. It only takes a little bit of knowledge to start making cool games.

I encourage you to try these scripts out, especially if you're a beginner. [@ me](http://twitter.com/peahat) if you have questions, and I'll do my best to help!

By the way... how cool is it that C# generates comments automatically? REALLY cool.

### PlayerController

Script for controlling the player object (the truck).  It also makes the boxes disappear when the truck collides with them and adds +1 to the score each time it happens.

The player object in the Roll-a-Ball tutorial is a sphere, so I had to modify this script to control a truck.

```
using UnityEngine;
using UnityEngine.UI;
using System.Collections;

public class PlayerController : MonoBehaviour {

	public float turnSpeed = 1000f;
	public float accellerateSpeed = 1000f;


	public Text countText;
	public Text winText;

	private Rigidbody rb;
	private int count;

	/// <summary>
	/// Initializes rigidbody, count, count text, and win text on start.
	/// </summary>
	void Start ()
	{
		rb = GetComponent<Rigidbody>();
		count = 0;
		SetCountText ();
		winText.text = "";
	}

	/// <summary>
	/// Controls speed and direction of the truck
	/// </summary>
	void Update ()
	{
		float h = Input.GetAxis( "Horizontal" );
		float v = Input.GetAxis( "Vertical" );

		rb.AddTorque( 0f, h * turnSpeed * Time.deltaTime, 0f );
		rb.AddForce( transform.forward * v * accellerateSpeed * Time.deltaTime );

	}


	/// <summary>
	/// If the player collides with pickup object, set pickup object to false and add +1 to count.
	/// </summary>
	void OnTriggerEnter(Collider other)
	{
		if (other.gameObject.CompareTag ("Pickup"))
		{
			other.gameObject.SetActive (false);
			count = count + 1;
			SetCountText ();
		}
	}


	void SetCountText ()
	{
		countText.text = "Count: " + count.ToString ();
		if (count >= 6)
		{
			winText.text = "YOU WIN!!!!! I love you!";
		}
	}

}
```

**Note:** The up key moves the truck forward regardless of where the nose is pointing. This turned out to be a pretty funny bug.

![](/images/truck.gif)


### CameraController

 Controls camera behavior. In this case, the camera follows the player object around the plane but stays at a fixed point above it.

```

 using UnityEngine;
 using System.Collections;

 public class CameraController : MonoBehaviour {

 	public GameObject player;

 	private Vector3 offset;

 	void Start ()
 	{
 		offset = transform.position - player.transform.position;
 	}

 	void LateUpdate ()
 	{
 		transform.position = player.transform.position + offset;
 	}
 }

```

### Rotator
This script rotates the boxes.

```

 using UnityEngine;
 using System.Collections;

 public class Rotator : MonoBehaviour {

 	// Update is called once per frame
 	void Update () {
 		transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);

 	}
 }
```

## Models

Learning how to use Blender often gave me a lot of ideas for how to make tutorial videos in my own work. My biggest takeaway is the importance of helping the user build something useable as quickly as possible. A related takeaway: Do not underestimate the danger of frustration and discouragement.

### The Box

![](/images/box.gif)

### The Field

![](/images/hillhill.gif)
