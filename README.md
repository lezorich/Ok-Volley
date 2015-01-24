# Ok-Volley
=====================================
<b>Ok-Volley</b> is an Android networking library which combines Square's <a href="http://square.github.io/okhttp/">OkHttp</a> client with <a href="http://developer.android.com/training/volley/index.html">Volley</a> Networking toolkit for Android. It already has implemented the common Volley classes:

* <b>VolleyManager</b>: Singleton class that encapsulates RequestQueue and other volley functionality
* <b>GsonRequest</b>: Volley adapter for json requests that will be parsed into Java objects by Gson.
* <b>LruBitmapCache</b>: Implementation of an in-memory lru cache


## Making a request
-----------------------------------
```
VolleyManager manager = VolleyManager.getInstance(getApplicationContext());
String url ="http://www.google.com";

// Request a string response from the provided URL.
StringRequest stringRequest = new StringRequest(Request.Method.GET, url,
            new Response.Listener() {
    @Override
    public void onResponse(String response) {
        // response
    }
}, new Response.ErrorListener() {
    @Override
    public void onErrorResponse(VolleyError error) {
        Toast.makeText(getApplicationContext(), "That didn't work!", 
            Toast.LENGTH_LONG).show();
    }
});

manager.getRequestQueue().add(stringRequest)
```


The library encapsulates Volley <i>RequestQueue</i> and other functionality in the <i>VolleyManager</i> class. VolleyManager is a singleton class, and ```VolleyManager.getInstance(context)``` returns the singleton instance. A key concept is that context must be the Application context, not an Activity context. This  ensures that the RequestQueue will last for the lifetime of your app, instead of being recreated every time the activity is recreated (for example, when the user rotates the device). 
