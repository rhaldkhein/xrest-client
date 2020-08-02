# Xrest Client

Flexible REST API testing in Visual Studio Code using **Simple Javascript Object**. Just like writing JSON!  
  
![xrest-client](https://raw.githubusercontent.com/rhaldkhein/vscode-xrest-client/master/static/demo.gif) 

## Features

- Create HTTP request files with simple Javascript object (just like JSON)
- Send requests directly from VS Code
- Pretty response panel/tab view that match with current theme
- Build multiple requests in single file
- Import common files like json or another js
- Auto persist cookies
- Auto save last successful responses (200 status code)
- Auto import `*.rc.js` (common config files)
- Load saved responses
- Supports images
- All features from Javascript for very complex request

## Requirements

The only requirements are to use specific file extensions.

1. `*.req.js` - for request files
2. `*.rc.js` - for common request configuration files

No other requirements or installation!

## Basic Usage

Dead simple example, with just URL.

#### 1. Create a request file.
Write the following code inside `mytodos.req.js`
```js
// Send Request
exports.get = 'http://jsonplaceholder.typicode.com/todos'

// Send Request
exports.post = {
  url: 'http://jsonplaceholder.typicode.com/todos',
  data: {
    title: 'New Todo'
  }
}
```
#### 2. Send the request.
Click the `Send Request` CodeLen above it. Or simply right click anyware inside editor and select `Send Request`.
#### 3. View response panel.
A response panel/tab view will auto show and give you complete information about the request.

## Advanced Usage

Following are the options you can use to build the request.  

```js
// axios request config object
exports.post = {
  url: 'https://jsonplaceholder.typicode.com/posts',
  // Add custom headers
  headers: {
    'X-Custom-Header': 'This is a custom data'
  },
  // Add body data. Can also be string
  data: {
    title: 'Hello',
    body: 'This is a body',
    userId: 1
  },
  // Add query string parameters
  params: { 
    foo: 'bar'
  },
  // Manual override method
  method: 'PATCH'
}
```
  
Most common options you might need are:

* `url` - resource url
* `params` - the query string `foo=bar&page=1&offset=6` but in object format
* `data` - the body of request  
* `headers` - request headers
* `method` - GET, POST, PUT, PATCH, ... 

Also check out axios [request config](https://github.com/axios/axios#request-config) object for more information.  

#### The `*.rc.js` files

A "Request Configuration" file holds the common data for all request files `*.req.js`.
Once you execute a request file, it will look for any configuration file and import all the data.

```js

// _common.rc.js
module.exports = {
  baseURL: 'https://myserver.com', // Auto prepend to `url`
  email: 'you@email.com',
  password: 'ssshhh',
  headers: {
    'X-Custom': 'Custom Data' // Auto merge to request
  }
}

// mytodos.req.js
module.exports = (config) => ({
  url: '/signin',
  method: 'POST',
  data: {
    email: config.email,
    password: config.password
  }
})

/*
Will request to https://myserver.com/signin 
with email, password and custom headers
*/

```
Notes: 
- Multiple rc files will be merged.
- `baseURL` will auto merge to `url` in req file
- `headers` will also auto merge to `headers` in req file

-----------------------------------------------------------------------------------------------------------

## License

[MIT License](LICENSE.txt)

