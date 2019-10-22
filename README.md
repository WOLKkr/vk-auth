meteor-vk-auth
==================

Login service for VKontakte accounts (https://vk.com).

Usage
-----

1. Add the package to your project using meteorite:
```sh
$ meteor add wolkkr:vk-auth
```

2. Configure vkontakte login service. You can do mannually or using GUI.

    **Manually**: Just add next code to your config file.
    ```js
        if (Meteor.isServer) {
            ServiceConfiguration.configurations.remove({
                service: 'vk'
            });

            ServiceConfiguration.configurations.insert({
                service: 'vk',
                appId:   '1234567',       // Your app id
                secret:  'someappsecret', // Your app secret
                scope:   'email,status',  // Your app scope
                v:        '5.102'          // VK API version
            });
        }
    ```

    **GUI**:
    * Add `accounts-ui` package to your project:

        ```sh
        $ meteor add accounts-ui
        ```
    * Set `{{> loginButtons}}` into your template
    * Go to your browser, open page with `{{> loginButtons}}`
    * Click on "configure Vk login" button
    * Fill "App Id", "App Secret", "[Scope](https://vk.com/dev/permissions)" fields in popup window following by instructions

3. Use `Meteor.loginWithVk(options, callback)` for user authentication (you can omit `options` argument).

4. For customization of new user creation you must set 'createUser' event handler:
```js
    if (Meteor.isServer) {
        Accounts.onCreateUser(function(options, user) {
            user.custom_field = "custom value";
            // ...
            return user;
        });
    }
```

***Enjoy!***

```
If this package helped you - STAR it on github. This is not difficult for you, but important for me.
```

Dependencies
------------

1. **accounts-base**
2. **accounts-oauth**
3. **accounts-ui** (if you want to use GUI)
