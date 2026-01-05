# UnityDeepLink
UnityDeepLink


https://github.com/Unity-Technologies/NotchSafeAreaSample

https://wotkd34sport.notion.site/DeepLink-2df95befd00180a4af89c3472b2beb28?source=copy_link

### AOS

<img width="898" height="339" alt="image" src="https://github.com/user-attachments/assets/7770506d-b24b-45b6-9c9b-4133cd002f6f" />


### iOS

<img width="429" height="108" alt="image" src="https://github.com/user-attachments/assets/9ca56b2b-83a1-4e73-8eb7-19f7218da1ab" />



### HTML

```HTML

<html>
<head>
<meta http-equiv=Content-Type content="text/html; charset=windows-1252">
</head>

<body >

<h1>My Deep Link Test page</h1>

<h2 >
<a href="unitydl://mylink">Launch with no parameter</a>
</h2>
<h2 >
<a href="unitydl://mylink?DisplayNotchSafeArea">Goto Scene DisplayNotchSafeArea</a>
</h2>
<h2 >
<a href="unitydl://mylink?SafeAreaControl">Goto Scene SafeAreaControl</a>
</h2>
<h2 >
<a href="unitydl://mylink?Menu">Goto Scene Menu</a>
</h2>
<h2 >
<a href="unitydl://mylink?Random">Random parameter value</a>
</h2>
</body>

</html>



```


### UnityCode

```C#

public class ProcessDeepLinkMngr : MonoBehaviour
{
    public static ProcessDeepLinkMngr Instance { get; private set; }
    public string deeplinkURL;

    private void Awake()
    {
        if (Instance == null)
        {
            Instance = this;                 
            Application.deepLinkActivated += onDeepLinkActivated;

            if (!String.IsNullOrEmpty(Application.absoluteURL))
            {
                // cold start and Application.absoluteURL not null so process Deep Link
                onDeepLinkActivated(Application.absoluteURL);
                Debug.Log("AbsoluteURL: " + Application.absoluteURL);
            }
            // initialize DeepLink Manager global variable
            else deeplinkURL = "[None]";
            DontDestroyOnLoad(gameObject);
        }
        else
        {
            Destroy(gameObject);
        }
    }

    private void onDeepLinkActivated(string url)
    {
        // update DeepLink Manager global variable, so URL can be accessed from anywhere 
        deeplinkURL = url;

        //Decode the DeepLink url to determine action
        string sceneName = url.Split("?"[0])[1];
        Debug.Log($"Deep Link Scene:{sceneName}");
        bool validScene;
        switch (sceneName)
        {
            case "DisplayNotchSafeArea":
                validScene = true;
                break;
            case "SafeAreaControl":
                validScene = true;
                break;
            case "Menu":
                validScene = true;
                break;
            default:
                validScene = false;
                break;
        }
        if (validScene) SceneManager.LoadScene(sceneName);
    }
}


```
