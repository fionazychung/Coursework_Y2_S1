# Tutorial 3: 
### 1) Randomize the orientation of blocks
To randomize the orientation at the start of the play the line of code must be written in `start`. Making use of the counter, the counter is randomized from a range of 0 to 3. This makes use of `Random.Range`. For `Random.Range(0, 4)` 0 is the starting number and since the last number is excluded, the second number must be set to 4 instead of 3. 

### 2) Set up a correct orientation that can be entered for each block individually in the inspector
For this you need to make two public booleans before start and update. By making these booleans public, it is then possible to set them to either true of false in the inspector. After this set up two `if statements`, one for the `verticalCount` and one for the `horizontalCount`. Both if statements are set to `true`, so depending on if the block is checked for `verticalCount` or `horizontalCount` as true in the inspector, the puzzle will be solved only when the set conditions are met.

### The full script:
```
 private Collider coll;

    public int Counter = 0;
    
    // Public booleans, 1 for the vertical and one for the horizontal position of the block.
    public bool verticalCount = true;
    public bool horizontalCount = true;
    
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
        
        // Depending on what is checked as true, one of the if statements that is correct will come into play.
        if (verticalCount == true)
        {
           // Enter what happens when the block is in the right position, e.g. the puzzle is solved and an area is unlocked (deactive collider).
        }
        if (horizontalCount == true)
        {
            // Use debug.log to check if the setting of true and false in the inspector works.
            Debug.Log("solved");
        }
    }
```
