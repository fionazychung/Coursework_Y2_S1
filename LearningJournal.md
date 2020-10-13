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



