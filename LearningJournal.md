# Learning Journal

## 13/10/2020
I was able to successfully rotate my block by 90 degrees, however if there are 2 blocks, they both rotate at the same time. This could be useful for some puzzles in my game (to make them harder), but I also need blocks that only rotate by themselves when they are clicked.
I had to change the `Physics Raycast` to a `Collider Raycast` and that solved the issue.
```
public class RotateBlock : MonoBehaviour
{

    Collider coll; 

    // Start is called before the first frame update
    void Start()
    {
        coll = GetComponent<Collider>();
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
                if(hit.collider.tag == "MyBlock")
                {
                    transform.Rotate(Vector3.back, 90.0f);
                }
            }
        }
    }
}
```

## 20/10/2020
I first tried to figure out how to create a counter by myself. For this I created a separate if statement. This did not work and was more lines of code than needed.

First attempt:
```
RotationCounter();
   private void RotationCounter()
    {
        if (MyBlock.transform.eulerAngles.z == 90)
        {
            Counter = 1;
            Debug.Log("Counter = 1");
        }

    }
```
Solution:
Change in raycast if statement to
```
if (hit.collider.tag == "MyBlock")
                {
                    Counter = Counter + 1;
                    transform.rotation = Quaternion.Euler(0.0f, 0.0f, 90.0f * Counter);
                }
                Debug.Log(Counter);
            }
            if (Counter > 3)
            {
                Counter = 0;
            }
```

## 30/10/2020
I tried to make a point and click character movement for my 3D game using the `NavMesh` function, but I don't know why I can't bake the areas of the ground. I need to bake the areas of the ground that the can be clicked and walked on, but this is not working. I think everything should work once the areas of the ground are baked. 

## 3/11/2020
I am trying to randomize the rotation at the start of whent he blocks are set up. I had to change my script around and I thought that was the issue, but it still doesn't work. The randomization of the counter works, but changing the counter does not change the rotation at the start. 
