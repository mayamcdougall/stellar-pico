# Stellar Theme for Pico
Port of HTML5 UP's [Stellar][] theme for [PicoCMS][].

> Say hello to Stellar, a slick little one-pager with a super vibrant color palette

## Getting Started

To use this theme:

1. Download the [Latest Release][] on GitHub.
2. Extract `themes/stellar` to your Pico `themes` folder.
3. Optionally extract all files in `content-sample/` to your `content` folder.
4. Set your `theme` to `stellar` in Pico's `config.yml`.
5. Optionally, set your site to order pages by `index` in Pico's `config.yml`. See below.
6. Configure your website using the YAML options in `index.md`.
7. Add sections to your page with new `.md` files.

## Details

This theme constructs a one-page site out of individual sections, each in their own `.md` file.

There are four main section layouts: `Generic`, `Spotlight`, `Features`, and `Statistics`.

Your `index.md` acts as both theme configuration and the contents of your page footer.

Each type of section has a collection of features exposed through the page's YML header.

We'll go into them in more detail below.

### Page Order

Pico has several choices when it comes to ordering your pages (alphabetically, by date, or using a page meta property).  Since you probably want your sections to display in a static order, the easiest way to do this is to add an `index` property to every page and sort by that (eg `index: 0`, `index: 1` and so on).

In Pico's `config.yml`, change `pages_order_by` to `meta`, and `pages_order_by_meta` to `index`.  You'll also want to set your `pages_order` to ascending (`asc`) if it's not already.

```
pages_order_by_meta: index
pages_order_by: meta
pages_order: asc
```

### Index

#### Theme Options

The first half of the options in `index.md` consist of general options for the entire site.  These options all exist as children of the `stellar` key, and should be indented as such.

- **logo** - The path to your site logo (eg, `assets/logo.png`).  Optionally supports a `no_logo` option, but leaving this undefined will default to the Stellar logo.

- **description** - A short description that goes below the logo and `site_title` (which is defined in your Pico `config.yml`).

- **copyright** - A string for the copyright at the bottom of the page. Defaults to using your `site_title` if undefined.

- **robots** - PicoCMS's default handling of the `robots` meta option. Whatever you enter here (eg `noindex, nofollow`) will be put in the `content` attribute of the meta robots tag.

- **css** - The path to a custom `.css` file (eg `assets/override.css`) that you can use to override and augment this theme's css styles.

- **fonts** - The url or path to a custom font via a CSS stylesheet.  You can provice your own, or use a Google Fonts API url to easily add more fonts.  You can also specify more than one URL by indenting each on a new line with a dash.

```
fonts:
- 'https://fonts.googleapis.com/css?family=Roboto'
- 'https://fonts.googleapis.com/css?family=Ubuntu'
```


- **og_image** - An "Open Graph" standard image.  This is the little preview image that displays when someone shares your URL via most modern messaging apps.

#### Footer Options

The *content* of your `index.md` will be used for the body text on the left side of the footer.

- **title** - This is the heading for the left side of the page footer.

- **actions** - Each individual section of this theme, as well as the page footer, support displaying action buttons at the bottom of their content. See the **Actions** section below for more information.

#### Contact Options

The right side of the footer supports adding contact information (or anything else) in a Definition List, as well as button links to social networks, etc.

- **title** - The heading for the right side of the page footer.

- **items** - Add whatever contact information you'd like in the format of `Key: Value`, each indented on a new line under `items`.  The `key` for each item is used for the Definition Term, while the value is used for the Definition Description.

```
items:
  Phone: 000-000-0000
  Email: someone@example.com
```

- **actions** - In this case, the **actions** system is used to generate social icons instead of buttons.  The syntax is the same, but some of the available options are different.  See the **Actions** section below for more information.

### Sections

In this theme, each `page` of your Pico `content` folder will become a section of the main page.  There are four supported "modes" each with a different layout and options.

#### Generic Mode

When you don't specify a `mode`, the section will be rendered in `generic` mode.  Generic mode is the most basic layout, and is pretty much just text-on-a-page below a section header.  If you're feeling ambitious though, you could always use generic mode to code your own layout by writing some HTML into your markdown.

In most modes, the page `content` will be displayed immediately under the title and description.  In the `Statistics` layout, content is instead placed at the bottom of the section and formatted into columns.  Including content is always *optional*, but `Features` and `Statistics` are the only layouts that can really serve their purpose without it.

The following options are supported by **ALL** modes, including Generic:

- **title** - The heading for each section.

- **description** - A short description that goes below the title.  This description utilizes `raw` mode for a little extra flexibility.  This means you'll be able to add HTML tags to it without them being escaped (mostly so you can `<br>` when you want a hard line break). Just be mindful of your special characters.

- **center** - Setting this option to `true` will center the section's contents (including heading and description) when using the Generic or Spotlight page layouts.  Features and Statistics modes are *already* centered by default.

- **actions** - Each individual section of this theme supports displaying action buttons at the bottom of their content. See the **Actions** section below for more information.

#### Spotlight Mode

- **image** - The path to the image you want to put in the "Spotlight" circle (eg `assets/image1.png`).

#### Features Mode

- **icons** - An array of icons to display on the page.  Each `key` will act as the heading text beneath its icon.  The layout for the `sub-keys` is very similar to the **Actions** layout.

  - **icon** - A Font Awesome class name for your desired icon (eg `fa-clock`).
  - **description** - A short description that will be displayed below the icon's heading.
  - **options** - Extra options for customizing your icons.  You can supply a single option, or supply multiple by putting each on its own line, indented with a dash.

    - **style(1-5)** - The options `style1`, `style2`, `style3`, `style4`, and `style5` will allow you to set slightly different colors for your icons.  They represent the following pastel colors: Pink, Lilac, Purple, Blue, and Sky Blue.  Using one of these is highly recommended, as the icons look very plain without color.
    - **solid** - Setting the `solid` option will use the Font Awesome *Solid* font, giving many of the available icons a filled-in look.  Some icons are only found in this set.
    - **brands** - Setting the `brands` option will use the Font Awesome *Brands* font.  Most commercial website logos and social network icons will be found in this set.

```
icons:
  Amazing Feature:
    icon: fa-exclamation
    description: This feature is really, really amazing! You'll have to see it for yourself!
    options: style1
```

#### Statistics Mode

Statistics mode uses all of the same settings as **Features** above does.  The only difference is that `style` changes the color of the surrounding box, and not the icon itself.

### Actions

Every page section supports having "actions" buttons at the bottom of it. The YAML layout for `actions` looks like this:

- **actions** - An array of buttons to display on the page.  Each `key` will act as the button text, or as an accessibility label on your social buttons.

  - **url** - The URL you'd like your button to go to.  This is the HTML `href` attribute, so don't forget your `http://` if you're linking externally.  Also, if you'd like to link to an `anchor` on your current page, you can escape the `#` with a `\` (otherwise YAML will make it into a comment!), for example `url: \#downloads`.
  - **icon** - A Font Awesome class name if you'd like your button to have an icon (eg `fa-download`).
  - **options** - Extra options for customizing your buttons.  You can supply a single option, or supply multiple by putting each on its own line, indented with a dash.  **Social Icons** on the site footer *only* support the `brands` and `no_circle` options.

    - **primary** - Makes this button a solid blue color.
    - **large** - Makes this button larger.
    - **small** - Makes this button smaller.
    - **disabled** - Makes this button greyed-out and unclickable.
    - **fit** - Makes **ALL** buttons equal in width and stretched to fill the page horizontally.  Setting this on *any* of your buttons affects all of them.
    - **stacked** - Makes **ALL** buttons stack vertically instead of horizontally.  Setting this on *any* of your buttons affects all of them.
    - **center** - Makes **ALL** buttons centered on layouts where they otherwise wouldn't be (`Generic` and `Spotlight` modes).  Setting this on *any* of your buttons affects all of them.
    - **solid** - If using an icon, setting the `solid` option will use the Font Awesome *Solid* font, giving many of the available icons a filled-in look.  Some icons are only found in this set.
    - **brands** - If using an icon, setting the `brands` option will use the Font Awesome *Brands* font.  Most commercial website logos and social network icons will be found in this set.
    - **no_circle** - Only used in social icon mode (eg, on the site footer).  Displays icons *without* their usual circle border.

```
actions:
  Issue Tracker:
    url: http://example.com
    icon: fa-github
    options:
      - brands
      - primary
```

## Issues and Feature Requests

If you have any issues with this port, or would like to request a feature, please create a new [Issue][] on GitHub.

[Stellar]: https://html5up.net/stellar
[PicoCMS]: http://picocms.org/
[Latest Release]: https://github.com/mayamcdougall/stellar-pico/releases
[Issue]: https://github.com/mayamcdougall/stellar-pico/issues

---

## Original Readme

Stellar by HTML5 UP
html5up.net | @ajlkn
Free for personal and commercial use under the CCA 3.0 license (html5up.net/license)


Say hello to Stellar, a slick little one-pager with a super vibrant color palette (which
I guess you can always tone down if it's a little too vibrant for you), a "sticky" in-page
nav bar (powered by my Scrollex plugin), a separate generic page template (just in case
you need one), and an assortment of pre-styled elements.

Demo images* courtesy of Unsplash, a radtastic collection of CC0 (public domain) images
you can use for pretty much whatever.

(* = not included)

AJ
aj@lkn.io | @ajlkn


Credits:

    Demo Images:
        Unsplash (unsplash.com)

    Icons:
        Font Awesome (fontawesome.io)

    Other:
        jQuery (jquery.com)
        Scrollex (github.com/ajlkn/jquery.scrollex)
        Responsive Tools (github.com/ajlkn/responsive-tools)
