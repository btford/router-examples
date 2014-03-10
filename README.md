# router examples

## conventions
setting a name without the other options default them

```javascript
router.config([
  {
    name: 'user/:id'
    // automatically provided
    // controller: 'UserController',
    // templateUrl: 'user/user.html'
  }
]);
```

**idea:** you can just give a string instead of an object:

```javascript
router.config([
  'user/:id'
]);
```


## preloading models

```javascript
router.config([
  {
    name: 'user/:id',
    resolve: {
      // not sure how to implement this
      user: UserResolver
    }
  }
]);


/*
 * elsewhere
 */
class UserResolver {
  constructor () {
    this.fetch();
  }
  function fetch () {
    http.get(this.url()).then(function (data) {
      this.data = data;
    }.bind(this));
  }
  function url () {
    return UserResolver.base + '/' + this.id;
  }
}
```

## parallel routes
this is challenging because there's no heirarchy here

TOOD: that email from brad

imagine a text editor with three panes open:
```
*---*---*---*
| 1 | 2 | 3 |
*---*---*---*
```

## nested

```javascript
router.config([
  {
    name: 'user/:id'
    children: [{
      name: ''
    }]
  }
]);
```


## spacial layouts
useful for mobile devices

```
         *--------*
         |  top   |
*--------*--------*--------*
|  left  | middle | right  |
*--------*--------*--------*
         | bottom |
         *--------*
```

needs to be able to animate in and out

### example

```javascript
router.config([
  { name:     'main' },

  { name:     'settings',
    position: 'settings <-> main' }, // neighbors

  { name:     'pane 1',
    position: 'main <- pane 1' }, // next open to right of main

  { name:     'pane 2',
    position: 'main <- pane 2' }, // next open to right of main
]);
```

yields:

```
*----------*------*--------*--------*
| settings | main | pane 1 | pane 2 |
*----------*------*--------*--------*
```

TODO: look into tiling window managers
TODO: tobias's document


## menus

```javascript
router.config();
// ->
// [{
//   name: 'foo'
// }]
```

```javascript
// https://example.com/foo
router.current();
// -> 'foo'
```

## License
Apache 2.0
