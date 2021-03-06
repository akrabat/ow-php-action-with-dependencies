# OpenWhisk PHP action with Composer dependency

This is an example of a simple OpenWhisk Docker action that uses PHP internally with a Composer dependency. Nowadays though, it's easier to use the built-in [PHP support][1].

It creates a [docker action][2], which has a `router.php` to respond to the 
OpenWhisk invocation API calls and a `src/action.php` which contains the PHP function
to execute.

The `src/action.php` must have a `main()` function with the following signature:

```php
    function main(array $args) : array
```

The `$args` contains the parameters passed to the action as an associative array and you must return an associative array which is then returned to the caller.

## Install

* Ensure you have installed Docker and have logged in using `docker login`.
* Ensure you have set up OpenWhisk and have a working `wsk` command line client.
* Copy `local.env.dist` to `local.env` and change `DOCKER_USER` to your username.
* Run `./build.sh` to build the docker container, create the action and run it.

Example:

```text
$ ./build.sh
Updating dependencies
Creating Docker container
Successfully built 0e6f436101c5
Tagging and pushing to Docker hub
Updating OpenWhisk action 'phpaction2'
Invoking OpenWhisk action: wsk action invoke -br phpaction2 --param name Everyone
{
    "Uuid": "275b906c-d7af-4e57-9038-f1c8767cbf46",
    "greeting": "Hello Everyone!",
    "time": "Wed, 07 Jun 2017 11:23:41 +0000"
}
```

## Run

To just run the action:

```text
wsk action invoke -br hellophp --param name Everyone
```


## License

For the avoidance of doubt, you may use this code however you like and do not need to attribute or include this notice. 

```text
Copyright 2017 Rob Allen

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

[1]: https://github.com/apache/incubator-openwhisk/blob/master/docs/actions.md#creating-php-actions
[2]: https://github.com/apache/incubator-openwhisk/blob/master/docs/actions.md#creating-docker-actions
