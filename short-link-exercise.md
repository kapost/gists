We'd like you to create a simple URL shortener, similar to [bit.ly](https://bitly.com).  Your service should support creating a short link for a valid URL, and then redirecting to that URL when the short link is accessed.

You should spend around 2 hours on this, no more.  Error on the side of completeness of individual features, over completing all features.  You can use any language and tools you'd like.  

Your submission should include the following
- the source code
- steps to setup, initialize and run the application
- anything else you think is helpful for us to test things out

You can submit a zip, a tarball, or a github repo. 

## Creating a Short Link
```
POST http://localhost:8080/short_link
{
  "long_url": "<long_url>"
}
```
Your API should accept a `POST` request with a JSON body and a content-type of `application/json`.  The `long_url` should be a valid URL like `https://kapost.com`.

If the `long_url` has already been shortened, you should return the previously created `short_link`.  Otherwise, you should return a new `short_link`.  The response should look something like 
```
{
  "long_url": "<long_url>",
  "short_link": "<short_link>"
}
```
where the `short_link` looks something like `http://localhost:8080/a1B2c3D4`

## Accessing a Short Link
Once you have a generated short link, you should be able to access the short link and be redirected to the long link (original URL).  The request would look something like
```
GET http://localhost:8080/a1B2c3D4
```
which would return a 301 that redirects the user to the original URL.

## Bonus Points
If you have time, you could create an analytics view for a given short link that will show analytics about each time the short link has been accessed. The analytics view is signified by adding a `+` to the end of a given short link. For example
```
GET http://localhost:8080/a1B2c3D4+
{
  "response": [
    { 
      "time": "2018-10-01T10:00:00Z", 
      "referrer": "none", 
      "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36" 
    },
    { 
      "time": "2018-10-01T15:30:10Z", 
      "referrer": "none", 
      "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36" 
    }
  ]
}
```
In the above example, the `referrer` is `none` because the link was directly pasted into a browser.  It should follow the same semantics of the HTTP referrer header.
    
