# Tutorial 3: Randomize the orientation of blocks and set up a correct orientation that can be entered for each block individually in the inspector


```
 private Collider coll;

    public int Counter = 0;

    // Making the variable public allows it to be seen and edited in the Unity inspector.
    public int CorrectCounter;

    // Start is called before the first frame update
    void Start()
    {
        coll = GetComponent<Collider>();

        // Sets the counter to a random number of either 0, 1, 2 or 3 at the start.
        Counter = Random.Range(0, 4);
    }

    // Update is called once per frame
    void Update()
    {
        if (Input.GetMouseButtonDown(0))
        {
            Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
            RaycastHit hit;
            if (coll.Raycast(ray, out hit, 100.0f))
            {
                if (hit.collider.tag == "MyBlock")
                {
                    Counter = Counter + 1;
                    if (Counter > 3)
                    {
                        Counter = 0;
                    }
                }
            }
        }
        // Transform must be outside of the if statements so that the block is being rotated by the counter, rather than by euler angles.
        // This allows the rotation of the block to be randomized by positions of 90, 180, and so on on the Z axis.
        transform.rotation = Quaternion.Euler(0.0f, 0.0f, 90.0f * Counter);
        
        // Checks if the counter is the same as/equal to the correct counter that is set in the inspector.
        if (Counter == CorrectCounter)
        {
            // Enter what happens when the block is in the right position, e.g. the puzzle is solved and an area is unlocked (deactive collider).
        }
    }
```
