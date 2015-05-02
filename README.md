# MCA WP

MCA WP is a small Persona marketing framework intended for developers. Using MCA WP you can:

  - Create and manage custom marketing Personas inside WordPress
  - Create custom landing pages tailored specifically to your visitors
  - Venerate the late Adam Yauch

### Emm-Cee-Aye?

From [Wikipedia](http://en.wikipedia.org/wiki/Adam_Yauch):

> Adam Nathaniel Yauch (pronounced /ˈjaʊk/; August 5, 1964 – May 4, 2012) was an American rapper, musician, film director, and human rights activist. He was best known as a founding member of the hip hop group Beastie Boys. He was frequently known by his stage name, MCA, and sometimes worked under the pseudonym Nathanial Hörnblowér. Yauch founded Oscilloscope Laboratories, an independent film production and distribution company based in New York City. As a Buddhist, he was involved in the Tibetan independence movement and organized the Tibetan Freedom Concert.

MCA may also stand for Marketing Content Assistant, I guess.

### Version

1.0.0

### Dependencies

MCA WP depends on [Advanced Custom Fields](https://github.com/elliotcondon/acf) 4.0 by [Elliot Condon](http://www.elliotcondon.com/). A copy of the plugin is included in `'mca-wp/includes/acf/'` and is activated upon plugin initialization. MCA WP defers to your WordPress's install of ACF if activated. 

### Installation & Use

1. Upload 'mca-wp' to the `'/wp-content/plugins/'` directory.
2. Activate MCA WP via the 'Plugins' menu in WordPress.
3. Create a new Persona via the 'MCA Personas' dashboard option.
4. Read further to display your Persona's data on landing pages.

### General Use

MCA WP uses two types of data: Persona data and Individual data. 

Persona data describes a particular group or archetype. Persona data lives in the WordPress database and is managed by ACF.

Individual data represents personal information (first name, last name, location, so forth). This information is passed to your landing page via $_GET variables in the URL. The retrieved values are sanitized prior to use.

Persona data and Individual data can both be accessed via shortcodes or PHP calls.

### User API

#### Shortcodes

##### Echo a Persona detail from database:
 * `persona_detail` = Persona detail to be queried (string). Persona details are referred to by their database keys. Persona details 1, 2, and 3 each override, respectively, to the three details in the default Persona field group.
 * `default_persona` (optional) = Default Persona to query if one is not passed in the URL. This can be passed in the form of a Persona's slug (string) or ID (int).
 
```
[mca_d persona_detail (default_persona)]
```

##### Echo an Individual detail from URL:
 * `individual_field` = Key in URL with value to output.
 * `default_output` (optional) = Default output if no value for `individual_field` is given in the URL.

```
[mca_u individual_field (default_output)]
```

Note that both shortcodes output nothing on error. This is by design.

#### URL Paramaters

Installs with basic permalinks use the scheme below:
```
http://uknowueatshellfish.com/?p=$pageid&pid=$pid&mcau1=$detail
```

Installs with custom permalinks the scheme below:
```
http://uknowueatshellfish.com/your-content/?pid=$pid&mcau1=$detail
```

Individual data may be given and retrieved with any key, but it is wise to avoid keys that may be used elsewhere on your site. When in doubt, start keys with `'mcau'` (or the like) to prevent conflicts. $pid should always be an integer value, as it corresponds to a Persona's post ID.

### Development API

#### Theme / Plugin Integration

##### Echo a Persona detail from database:
 * `$persona_detail` = Persona detail to be queried (string). Persona details are referred to by their database keys. Persona details 1, 2, and 3 each override, respectively, to the three details in the default Persona field group.
 * `$default_persona` (optional) = Default Persona to query if one is not passed in the URL. This can be passed in the form of a Persona's slug (string) or ID (int).

```php
<?php mca_wp_d( $persona_detail [, $default_persona] ); ?>
```

##### Echo an Individual detail from URL:
 * `$individual_field` = Key in URL with value to output.
 * `$default_output` (optional) = Default output if no value for `$individual_field` is given in the URL.

```php
<?php mca_wp_u( $url_detail [, $default_output] ); ?>
```

Note that both functions output nothing on error. This is by design.

#### Register Custom Persona Field Groups

Additional groups of persona details can be registered via `'mca_wp_add_persona_group'`. The code below should be run at plugin/theme init or in your `functions.php`.
```php
<?php add_action( 'mca_wp_add_persona_group', 'mca_wp_register_your_group' ); ?>
```
An example field group is given in `'includes/groups/mca-wp-default-group.php'`.

### Shoutouts

To Adquisitions, Elliot Condon, Adam Yauch, The Sangha, and Gautama Buddha.

### Todo

- Beef up documentation, include screenshots

### License

Released under the [GPLv2](http://www.gnu.org/licenses/gpl-2.0.txt) license.

Copyright (c) 2015 Justin Carver / Adquisitions
