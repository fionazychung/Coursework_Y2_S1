# Tutorial 2: Creating a Counter for the Rotation of the Block

This tutorial builds on the script and Unity project created in tutorial 1.

Adding to the script `RotateBlock`, create a counter before void Start.
```
int Counter = 0;
```
Then within `if (hit.collider.tag == "MyBlock")` change the contents to
```
// Adds 1 to the counter value every time the block is clicked/rotated.
Counter = Counter + 1;
// Rotates the block on the z axis by 90 degrees and multiplies the counter by 90
transform.rotation = Quaternion.Euler(0.0f, 0.0f, 90.0f * Counter);
```
How the counter works:

0 * 90 = 0

1 * 90 = 90

2 * 90 = 180

3 * 90 = 270

By using the counter in this way, the degrees values are converted into integers that do not have decimal points. This gets rid of the possible error when using euler angles, for example when the rotation is not exactly 90 degrees. 

Inside of `if (Input.GetMouseButtonDown(0))` add:
```
 if (Counter > 3)
            {
                Counter = 0;
            }
```
This sets the counter back to 0 once it reaches 4.

To view the counter:
Add to `if (coll.Raycast(ray, out hit, 100.0f))`
```
Debug.Log(Counter);
```
