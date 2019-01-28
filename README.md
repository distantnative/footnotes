# Footnotes for Kirby 2 CMS

[![Release](https://img.shields.io/github/release/distantnative/footnotes.svg)](https://github.com/distantnative/footnotes/releases)  [![Issues](https://img.shields.io/github/issues/distantnative/footnotes.svg)](https://github.com/distantnative/footnotes/issues)
[![Moral License](https://img.shields.io/badge/buy-moral_license-8dae28.svg)](https://gumroad.com/l/kirby-footnotes)

This plugin extends [Kirby CMS](http://getkirby.com) with some basic and extremely easy footnote functionalities. The syntax is simple to understand and if the plugin is removed the remaining text still makes sense.

**With the release of [Kirby 3](https://getkirby.com), this plugin has been archived and will not be maintained.**


## Table of Contents
1. [Requirements](#Requirements)
2. [Installation & Update](#Installation)
3. [Usage](#Usage)
4. [Options](#Options)
5. [Help & Improve](#Help)
6. [Version History](#VersionHistory)

## Requirements <a id="Requirements"></a>
Since version 1.0.0 the footnotes plugin requires Kirby CMS 2.3.0 or higher.  
If you are running an older version of Kirby, please use [version 0.9.0](https://github.com/distantnative/footnotes/releases/tag/v0.9).

## Installation & Update <a id="Installation"></a>
1. Download [Footnotes](https://github.com/distantnative/footnotes/zipball/master/)
2. Add to `site/plugins/footnotes/`
3. Add CSS for the footnotes (optional)  
`.footnote`: in-text reference mark, `sup` tag  
`.footnotes`: `div` wrapper for list of footnotes, `ol` list inside  
`.footnotedivider`: `div` element before the `ol` list  

#### With the [Kirby CLI](https://github.com/getkirby/cli)
```
kirby plugin:install distantnative/footnotes
```


## Usage <a id="Usage"></a>
Use the footnotes method on the field: `$page->text()->footnotes()` or `$page->text()->ft()`. Adding footnotes to your Kirbytext field is simple. Just type them inline in your post in square brackets like this:

```
[^This is a footnote.]
[^ This is another.]
```

Each footnote must start with a caret (`^`) and will be numbered automatically. Footnotes can contain anything you want including links or images. Entries in the bibliography are automatically linking back to the spot in the text where the note was made.

```
“In a deterritorialized context, the conventional one-to-one 
relationship between state and territory is increasingly 
questioned and challenged” [^Wong, L. (2002): Home away from 
home? Abingdon: Routledge. Seite 171]
```

**In-text reference mark:**  
![In-text reference mark](https://cloud.githubusercontent.com/assets/3788865/18232001/fa5dc6d8-72c6-11e6-841e-57e37f292646.png)
**Bibliography at the end of the text:**  
![Bibliography](https://cloud.githubusercontent.com/assets/3788865/18232000/fa5d552c-72c6-11e6-8ba0-c17a8f79bb52.png)

*Notes:*  
- You should not include square brackets [] inside a footnote.

#### Footnotes without reference mark
To have a footnote/an information included in the bibliography, but without any reference mark inside the text, just prepend a `!` to the footnote:
```
[^! **Photo credits:** (link:http://www.flickr.com/photos/cubagallery/ text:Cuba Gallery)]
```



## Options <a id="Options"></a>

#### Remove footnotes
If you want show footnotes of a text field on specific pages (e.g. single blog article) but not on others (e.g. blog overview), you can add a parameter to the footnotes field method in e.g. `templates/blog.php` to remove all footnotes:
```php
<?= $post->text()->footnotes(false) ?>
<?= $post->text()->footnotes(['convert' => false]) ?>
```

#### Separate bibliography output
If you do not want the bibliography to be appened right after the field text, you first have to deactivate thhe bibliography in the field method:
```php
<?= $page->text()->footnotes(['bibliography' => false]) ?>
```
And then output the bibliography where wanted:
```php
<?= KirbyFootnotes::bibliography($page->text()) ?>
```

#### Smooth scrolling
With the following options, you can enable a smooth scrolling effect to the bibliography as well as define a scroll speed and an offset to the scrolling position (e.g. if a fixed header menu is used). Add them to your `site/config/config.php`:

```php
c::set('plugin.footnotes.scroll',        true);
c::set('plugin.footnotes.scroll.offset', 60);
c::set('plugin.footnotes.scroll.speed',  500);
```

#### Global footnotes
In addition to converting footnotes via the field method, you can set an option to activate it for all Kirbytext outputs globally. Add the following to your `site/config/config.php`:
```php
c::set('plugin.footnotes.global', true);
```

#### Specific templates
**Allowed**  
You can allow footnotes only on specific templates by adding the following to your `site/config/config.php`:
```php
c::set('plugin.footnotes.templates.allow', array(
  'about',
  'blog',
  'project'
));
```

**Ignored**
You can restrict footnotes from specific templates by adding the following to your `site/config/config.php`:
```php
c::set('plugin.footnotes.templates.ignore', array(
  'about',
  'blog',
  'project'
));
```


## Help & Improve <a id="Help"></a>
*If you have any suggestions for further configuration options, [please let me know](https://github.com/distantnative/footnotes/issues/new).*


## Version history <a id="VersionHistory"></a>
You can find a more or less complete version history in the [changelog](CHANGELOG.md).

## License
[MIT License](http://www.opensource.org/licenses/mit-license.php)

## Author
Nico Hoffmann - <https://nhoffmann.com>
