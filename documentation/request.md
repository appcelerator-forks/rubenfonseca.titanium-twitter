# Request

_This documentation is not in sync with the Apple documentation_

## Properties

### url

The URL to make the request. Ex: `http://api.twitter.com/1/statuses/public_timeline.json`.

### method

On of the 3 request methods:

- Twitter.REQUEST_METHOD_GET
- Twitter.REQUEST_METHOD_POST
- Twitter.REQUEST_METHOD_DELETE

### account (optional)

If you want to authenticate/sign the request, you must provide a valid 
[Account](account.html) object to this property, before you make the request.

## Events

### success

Fired when the Twitter Request succeeds. The returned JSON response is
deserialized on the `data` key on the event object.

    var request = Twitter.createRequest({
      url: 'http://api.twitter.com/1/statuses/public_timeline.jso',
      method: Twitter.REQUEST_METHOD_GET
    });

    request.addEventListener('success', function(e) {
      Ti.API.log(e.data);
    });

    request.perform();

### failure

Fired when the Twitter Request fails. An error explanation should be present
on the `error` key.

    var request = Twitter.createRequest({
      url: 'http://api.twitter.com/1/statuses/public_timeline.jso',
      method: Twitter.REQUEST_METHOD_GET
    });

    request.addEventListener('failure', function(e) {
      Ti.API.log("STATUS CODE IS " + e.status);
      Ti.API.log("ERROR: " + e.error);
    });

    request.perform();

## Tasks

### perform()

Performs the request. Set the success/failure handlers before calling this method. The
result will be delivered async.

### addMultiPartData({...})

Adds a binary object to the request, like an image. It accepts the following 3 required keys:

- *name*: the name of the argument

- *data*: a TiBlob with the data to add to the request

- *type*: a mime type string

      var request = Twitter.createRequest({...})
      var image = Ti.Filesystem.getFile(...);

      request.addMultiPartData({
        name: 'media[]',
        data: image.read(), // always a TiBlob
        type: 'image/png'
      });

      request.perform();

