:warning: This element is **DEPRECATED**, we lack of resorces to support it any longer. Please write an issue if you are interested in maintaining it.

# &lt;juicy-tile-list&gt; ![Bower Version](https://badge.fury.io/bo/juicy-tile-list.svg) [![Build Status](https://travis-ci.org/Juicy/juicy-tile-list.svg?branch=master)](https://travis-ci.org/Juicy/juicy-tile-list)

> `<juicy-tile-list>` is masonry-like Custom Element for sortable tiles that packs efficiently without changing HTML structure (changes CSS only).

## Features

It gives you:
 - masonry-like, gap-less layout (bin-packing),
 - layout applied in Shadow DOM - so it doesn't mess with your styles,
 - prioritizing items,
 - grouping into virtual, nested containers,
 - alignment in different orientations and directions,
 - dynamically changing size,
 - auto adjusting container sizes,
 - gutter/cell-spacing between tiles,
 - adapting to window size changes.


## Demo

[Check it live!](http://juicy.github.io/juicy-tile-list)

## Usage

1. Install the component using [Bower](http://bower.io/):

    ```sh
    $ bower install juicy-tile-list --save
    ```

2. Import Web Components' polyfill, if needed:

    ```html
    <script src="bower_components/webcomponentsjs/webcomponents.js"></script>
    ```

3. Import Custom Element:

    ```html
    <link rel="import" href="../juicy-tile-list/dist/juicy-tile-list.html">
    ```

4. Start using it!

    ```html
    <juicy-tile-list></juicy-tile-list>
    ```

## Options

Attribute                    | Options             | Default      | Description
---                          | ---                 | ---          | ---
`defaultTileSetup`           | *Object*            | see below    | Overwrites default values for Tiles (`setup.items[?].?`)
`gutter`                     | *Number*            | `0`          | Overwrites default value of `setup.gutter`
`duration`                   | *Number*            | `0.5`        | Duration of repack animation (in seconds).
`setup`                      | *Object*            |              | Tiles setup
`setup.width`                | *Number*            |              | Container width to be used for packing in `horizontal` direction, if not given  `innerWidth(this)` will be used.
`setup.heigh`                | *Number*            |              | Container height to be used for packing in `vertical` direction, if not given  `innerWidth(this)` will be used.
`setup.gutter`               | *Number*            | `0`          | Gutter/cell-spacing size in px
`setup.direction`            | *String*            | `horizontal` | How to align our package (horizontal layers `horizontal`, or vertiacal layers: `vertical`)
`setup.rightToLeft`          | *Boolean*           | `false`      | If set to `true`, tiles within this container will be arranged from the right to the left.
`setup.bottomUp`             | *Boolean*           | `false`      | If set to `true`, tiles within this container will be arranged from the bottom to the top.
`setup.items`                | *Array*             | `[]`         | Tiles setup
`setup.items[?].priority`    | *Number* (0-1)      | `0`          | Importance of tile, used for sorting elements.
`setup.items[?].width`       | *Number*            | `1`          | Tile width
`setup.items[?].precalculateWidth` | *Boolean*     | `false`      | Set to `true` to automatically pre-calculate width before every (re-)packing.
`setup.items[?].heigh`       | *Number*            | `1`          | Tile height
`setup.items[?].precalculateHeight`| *Boolean*     | `false`      | Set to `true` to automatically pre-calculate height before every (re-)packing.
`setup.items[?].id`          | *String*            |              | Element/group id by default order in DOM will be used
`setup.items[?].content`     | *String*            |              | HTML content for (for virtual containers)
`setup.items[?].oversize`    | *Number*            | `0`          | Make container's box & background bleed for this amount of pixels out of packed box. So, render box bigger, but pack with its original size (for virtual containers)
`setup.items[?].items`       | *Array(Items)*      |              | Recursive setup (for virtual containers)
`setup.items[?].gutter`      | *Number*            | `0`          | Recursive setup (for virtual containers)
`setup.items[?].direction`   | *String*            |              | Recursive setup (for virtual containers)
`setup.items[?].rightToLeft` | *Boolean*           |              | Recursive setup (for virtual containers)
`setup.items[?].bottomUp`    | *Boolean*           |              | Recursive setup (for virtual containers)
`refreshOnMutation`          | *Boolean*           | `false`      | If set to `true`, tile-list will be repacked and re-rendered once nodes are added or removed.
`refreshOnResize`            | *Boolean*           | `false`      | If set to `true`, tile-list will be repacked and re-rendered once window or container gets resized
`refreshOnAttached`          | *Boolean*           | `true`       | If set to `true`, tile-list will be repacked and re-rendered once (re-)attached to DOM

## Properties

Name                 | Options        | Description
---                  | ---            | ---
`elements`           | *Array*        | Array of children which are going to be arranged.
`duration`           | *Number*       | Duration of repack animation (in seconds).
`setup`              | *Object*       | Up to date tiles setup. Structure as in attributes.
`allItems`           | *Object*       | Map of setup nodes. Root container is available under `allItems['root']`.
`items[.].container` | *Object*       | Reference to container item. (non-enumerable property)

## Methods

Name               | Param name | Type               | Default | Description
---                | ---        | ---                | ---     | ---
`resizeItem`       |            |                    |         | Resize any item (real element or virtual container)
                   | item       | *Item*             |         | Reference to the setup item
                   | width      | *Number*           | `0`     | new width
                   | height     | *Number*           | `0`     | new height
`reprioritizeItem` |            |                    |         | Change priority/weight of any item
                   | item       | *Item*             |         | Reference to the setup item
                   | increase   | *Boolean*          | `false` | `true` - increases, `false` decreases priority
                   | end        | *Boolean*          | `false` | `true` to move to the end of list
`moveToContainer`  |            |                    |         | Move any item to given container, or wrap it with new one
                   | what       | *Item*             |         | Reference to the setup item
                   | where      | *Item*             |         | Reference to the destination container item.
                   | noPacking  | *Boolean*          | `false` | `true` to prevent  re-packing after setup change.
`createNewContainer`|           |                    |         | Create new empty virtual container.
                   | name       | *String*           |         | Name for the container
                   | where      | *Item*             | `"root"`| Reference to the container setup item
                   | rectangle  | *Rectangle*        |         | Rectangle setup (width, height, priority)
                   | noPacking  | *Boolean*          | `false` | `true` to prevent  re-packing after setup change.
`deleteContainer`  |            |                    |         | Delete virtual container, move items (if any) to one above.
                   | what       | *Item*             |         | Reference to the container setup item to delete.
                   | noPacking  | *Boolean*          | `false` | `true` to prevent  re-packing after setup change.

## Events

Name                      | Data | Description
---                       | ---  | ---
`juicy-tile-list-refresh` |  -   | Triggered once layout is refreshed

## Refresh/repack

`<juicy-tile-list>` can refresh/repack your tiles interactively. You can set it by attributes: `refreshOnMutation`, `refreshOnResize`, `refreshOnAttached`.

## :space_invader: :construction: Per-item declarative setup (experimental feature)

If you would like to provide more declaratively setup for each element of `<juicy-tile-list>`, you can do so by adding custom attribute `juicy-style` on child element, and provide setup in CSS-like syntax:
```html
<juicy-tile-list>
 <div juicy-style="width: 50%; height: 20;">smth</div>
</juicy-tile-list>
```
instead of setting it via setup:
```javascript
juicytilelist.setup = {
  // ...    
  items:[
    {
      id: 0,
      priority: 0.2,
      width: "50%",
      height: 20
    }
  ]
}
```
Properties provided in `juicy-style` **extends** defaults, but may be overwritten by explicit setup entry.

The importance of setups, looks as follows:

1. `juicy-tile-list`'s `setup` attribute/property,
2. `juicy-tile-list`'s child `juicy-style` attribute (extends defaults mentioned below),
3. `juicy-tile-list`'s `defaultTileSetup` attribute,
3. `juicy-tile-list`'s build in default tile setup.

Meaning, that a setup higher on the list overwrites previous values

## Tile ids

Every tile gets its id, it's used in ShadowDom (so it won't collide with your markup) to match Light DOM content with positioned tile (and its setup).
In HTML ids get created automatically, from order in DOM, so in your setup JSON you simply need to match the index of child node.

### :construction: Custom ids (experimental feature)

If for some reason, consecutive numbers does not fit your needs, you can assign id manually, by setting `juicytile` attribute:
```html
<juicy-tile-list>
 <div juicytile="myFancyTileId">smth</div>
</juicy-tile-list>
```
```javascript
juicytilelist.setup = {
  items:[
    {
      id: "myFancyTileId",
      priority: 0.2
    }
  ]
}
```
### Scoped ids (experimental feature)

You can also add name-space to your id in declarative way.
```html
<juicy-tile-list>
  <juicy-tile-group name="fruits">
    <div>apple</div>
  </juicy-tile-group>
  <juicy-tile-group name="veggies">
    <div>carrot</div>
  </juicy-tile-group>
</juicy-tile-list>
```
```javascript
juicytilelist.setup = {
  items:[
    {
      id: "fruits/0",
      priority: 0.2
    },
    {
      id: "veggies/0",
      priority: 0.4
    }
  ]
}
```

## Related components

- [`<juicy-tile-editor>`](Juicy/juicy-tile-editor) - GUI for editing tiles JSON setup
- [`<juicy-tile-grid>`](Juicy/juicy-tile-grid) - Tiles rendered with CSS Grid Layout

## Development
Naturally stary with `npm install` and `bower install`.

#### Minify
To minify  code you can use `grunt minify`

#### Release

To minify, bump versions and release it, use `grunt release`


## Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## History

For detailed changelog, check [Releases](https://github.com/Juicy/juicy-tile-list/releases).

## License

MIT
