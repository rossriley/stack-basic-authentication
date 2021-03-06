HTTP Basic Authentication Stack Middleware
==========================================

A [Stack][0] middleware to enable [HTTP Basic Authentication][1] following the
[STACK-2 Authentication][2] conventions.


Fork Information
==========================================

Package forked from the original work here: https://packagist.org/packages/dflydev/stack-basic-authentication

This is an attempt to make it framework agnostic, since the original depends on Silex / Pimple

Installation
------------

Through [Composer][3] as [rossriley/stack-basic-authentication][4].


Usage
-----

The BasicAuthentication middleware accepts the following options:

 * **authenticator**: *(required)* A callback used to ensure that the specified
   credentials are correct.
 * **realm**: The HTTP Basic Authentication realm as defined by [RFC1945][5].
 * **firewall**: A firewall configuration compatible with
   [dflydev/stack-firewall][6].

```php
<?php

$authenticator = function ($username, $password) {
    // Given a username and password credentials, ensure that
    // the credentials are correct and return a token that
    // represents the user for this request.
    if ('admin' === $username && 'default' === $password) {
        return 'admin-user-token';
    }
};

$app = new Dflydev\Stack\BasicAuthentication($app, [
    'firewall' => [
        ['path' => '/', 'anonymous' => true],
        ['path' => '/login'],
    ],
    'authenticator' => $authenticator,
    'realm' => 'here there be dragons',
]);
```

Examples
--------

See the `examples/` directory for some live examples of this middleware in
action.


License
-------

MIT, see LICENSE.


Community
---------

If you have questions or want to help out, join us in the **#stackphp** or **#dflydev** channels on **irc.freenode.net**.


[0]: http://stackphp.com/
[1]: http://en.wikipedia.org/wiki/Basic_access_authentication
[2]: http://stackphp.com/specs/STACK-2/
[3]: http://getcomposer.org
[4]: https://packagist.org/packages/dflydev/stack-basic-authentication
[5]: http://tools.ietf.org/html/rfc1945#section-11
[6]: https://packagist.org/packages/dflydev/stack-firewall
