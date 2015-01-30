![inuitcss](logo-inuitcss.png)

# Getting started

This is the interim documentation for the new inuitcss. Until we get some proper
stuff in place, I hope this will see to 90% of questions and issues.

## What is inuitcss?

inuitcss is a powerful, Sass-based, BEM, OOCSS framework designed with scalability
and performance in mind. It has a tiny footprint (the [Starter
Kit]((https://github.com/inuitcss/starter-kit)) comes in at 1KB, gzipped), and
can be scaled as much or as little as you need.

inuitcss provides a solid architectural foundation upon which you can build any
size or style of website or app. inuitcss has been used on [single-page
marketing sites](https://www.fasetto.com/), [medium-sized
blogs](http://csswizardry.com), to [full products for the likes of the
NHS](http://csswizardry.com/case-studies/nhs-nhsx-elearning-platform/). inuitcss
is what you make of it—it helps you get started, and then gets out of your way.

inuitcss is a framework in its truest sense. It is not a UI Toolkit, with
opinionated views on design; it is not one giant download, with hundreds of
unnecessary lines of CSS; it is not a 1001-UI-components-plus-the-kitchen-sink,
with loads of bloated rules. It is a collection of tiny, composable,
configurable, interdependent modules that you can piece together how you want
to, when you want to. inuitcss’ focus is less upon the actual code within it,
but upon the principles of a solid, scalable CSS architecture.

Say goodbye to bloated old UI Toolkits and opinionated, monolithic libraries.

**Say hello to inuitcss.** ![inuitcss](logo-inuitcss-tiny.png)

## As quick as possible

The quickest, simplest way to get started with inuitcss is via the [Starter
Kit](https://github.com/inuitcss/starter-kit). Simply run

    $ bower install --save inuit-starter-kit

or use npm for this:

    $ npm install --save inuit-starter-kit

…to grab the correct dependencies, and then import them into a bare Sass project
in the following order:

    @import "bower_components/inuit-defaults/settings.defaults";

    @import "bower_components/inuit-functions/tools.functions";
    @import "bower_components/inuit-mixins/tools.mixins";

    @import "bower_components/inuit-normalize/generic.normalize";
    @import "bower_components/inuit-box-sizing/generic.box-sizing";

    @import "bower_components/inuit-page/base.page";

This source order is imperative, and underpins the entire inuitcss framework.
If you use npm instead, replace `bower_components` with `node_modules`.

## New to Bower / npm?

If you are new to [Bower](http://bower.io/) or [npm](https://www.npmjs.com/),
but would like to install inuitcss through it, then this is a quick guide to
getting up and running:

Install [node.js](http://nodejs.org/) on your system following the website’s
instructions. This automatically installs `npm` for you.

If you want to use Bower in addition, follow the next steps. Otherwise
continue from installing the individual modules of inuit.

Install Bower globally (`-g`).

    $ [sudo] npm install -g bower

Initialise Bower in your CSS directory (and follow the command line wizard):

    $ cd path/to/your/css/directory
    $ bower init

Once you have filled out the interactive wizard, you should now have a new
`bower.json` file in your current (i.e. CSS) directory.

From here on in, running:

    $ bower install --save inuit-[module]

…inside the same directory will install the specified module in a
`bower_components` directory, and will save it (`--save`) to your `bower.json`.

That really is a very superficial overview; please do be sure to take the time
to [read up on Bower](http://bower.io/).

## Setting up a project

With inuitcss, you are in charge of almost everything; this includes your master
Sass file.

You will need to create your own master Sass file, e.g. `main.scss`, and
`@import` yours and inuitcss’ modules into that. This kind of architecture
allows you to intersperse inuitcss code with your own, whereas most other CSS
Frameworks and UI Toolkits only permit you to work before or after you’ve
imported them. This is a perfectly valid (example) setup in inuitcss world:

    @import "bower_components/inuit-defaults/settings.defaults";
    @import "settings.colors";
    @import "bower_components/inuit-responsive-settings/settings.responsive";

    @import "bower_components/inuit-functions/tools.functions";
    @import "bower_components/inuit-mixins/tools.mixins";
    @import "bower_components/inuit-responsive-tools/tools.responsive";
    @import "tools.aliases";

    @import "bower_components/inuit-normalize/generic.normalize";
    @import "bower_components/inuit-box-sizing/generic.box-sizing";
    @import "bower_components/inuit-shared/generic.shared";

    @import "bower_components/inuit-page/base.page";
    @import "bower_components/inuit-headings/base.headings";
    @import "base.links";
    @import "base.quotes";

    @import "bower_components/inuit-buttons/objects.buttons";
    @import "bower_components/inuit-layout/objects.layout";
    @import "bower_components/inuit-media/objects.media";

    @import "components.page-head";
    @import "components.page-foot";
    @import "components.site-nav";
    @import "components.ads";
    @import "components.promo";

    @import "bower_components/inuit-widths/trumps.widths";
    @import "bower_components/inuit-spacing/trumps.spacing";

Note how we are interlacing inuitcss code with our own? This is how inuitcss is
designed to work. It doesn’t act overly opinionated, and it doesn’t try to do
your job for you: you call upon inuitcss when you need it, and do your own thing
when you don’t.

## Import order

Because inuitcss is broken apart into lots of small, composable modules, it is
important that you as the developer piece things together in the correct order.
That order is:

* **Settings:** Global variables, site-wide settings, config switches, etc.
* **Tools:** Site-wide mixins and functions.
* **Generic:** Low-specificity, far-reaching rulesets (e.g. resets).
* **Base:** Unclassed HTML elements (e.g. `a {}`, `blockquote {}`, `address {}`).
* **Objects:** Objects, abstractions, and design patterns (e.g. `.media {}`).
* **Components:** Discrete, complete chunks of UI (e.g. `.carousel {}`). This is
  the one layer that inuitcss doesn’t get involved with.
* **Trumps:** High-specificity, very explicit selectors. Overrides and helper
  classes (e.g. `.hidden {}`).

The order of partials within each layer is fairly open; it is the sections
themselves that are important to get in the correct order.

**N.B.** All partials—including your own—follow the `<section>.<file>` naming
convention, e.g. `_objects.box.scss`, `_components.carousel.scss`.

Eventually, this architecture will be written up at [itcss.io](http://itcss.io).
Keep an eye on [the Twitter account](https://twitter.com/itcss_io) for updates.

## Core functionality

There are very few **required** inuitcss modules, and the ones that are deal
only with config and tooling.

Before it can do anything, inuitcss needs to know your base `font-size` and
`line-height`. These settings are stored in `settings.defaults` (as
`$inuit-base-font-size` and `$inuit-base-line-height`), and can be overridden in
the same way you’d [override any of inuitcss’
config](https://github.com/inuitcss/getting-started#modifying-inuitcss).

Probably the most opinionated thing inuitcss will ever do is reassign your
`$inuit-base-line-height` variable to `$inuit-base-spacing-unit`. This value
then becomes the cornerstone of your UI, acting as the default (remember, you
can override everything in inuitcss) margin and padding value for any components
that require it.

While this might seem overly opinionated, it does mean that:

1. **You get a free vertical rhythm** because everything sits on a multiple of
   your baseline, and…
2. **We reduce the amount of [magic
   numbers](http://csswizardry.com/2012/11/code-smells-in-css/#magic-numbers) in
   our codebase** because we can rationalise where the majority of values in our
   CSS came from.

A lot of inuitcss modules will also require `tools.functions`, which is a very
simple file containing only a handful of math helper functions. These are used
to quickly create size variants of objects, e.g.
`padding: double($inuit-base-spacing-unit);`.

The other likely piece of required functionality is the `tools.mixins` module.
This contains a simple font-sizing mixin that is used later on in certain
type-based modules.

Aside from that, most inuitcss partials have very few interdependencies, and
those that do are all dependency managed (if you are using Bower).

## Installing new modules

Installing new modules via Bower is simple, just refer to the module’s GitHub
repository’s README for the specific command.

Almost all of inuitcss’ modules depend on inuitcss’ default
[settings](https://github.com/inuitcss/settings.defaults) and
[functions](https://github.com/inuitcss/tools.functions). If you are using Bower
then you will get these installed automatically. If you are not using Bower,
please ensure you have downloaded them manually.

### Not using Bower / npm?

That’s cool, you can either install inuitcss dependencies as [Git
Submodules](http://git-scm.com/docs/git-submodule), or just save the individual
files to disk. What is important, however, is that you ensure you have the
correct versions of each file (Bower would solve this problem for you
automatically), and that you include them in the correct order.

## Modifying inuitcss

inuitcss is highly configurable, but **should not be edited directly**. The
correct way to make changes to inuitcss is to pass in variables **before** you
`@import` the specific file. Let’s take
[`settings.defaults`](https://github.com/inuitcss/settings.defaults) as an
example—in this file we can see the variables `$inuit-base-font-size` and
`$inuit-base-line-height`. If we want to keep these as-is then we needn’t do
anything other than `@import` the file. If we wanted to change these values to
`12px` and `18px` respectively (don’t worry, inuitcss will convert these pixel
values to rems for you) then we just need to pass those values in before the
`@import`, thus:

    $inuit-base-font-size:   12px;
    $inuit-base-line-height: 18px;
    @import "bower_components/inuit-defaults/settings.defaults";

The same goes for any inuitcss module: you can configure it by predefining any
of its variables immediately before the `@import`:

    $inuit-btn-background:      #BADA55;
    $inuit-btn-radius:          3px;
    $inuit-enable-btn--full:    true;
    @import "bower_components/inuit-buttons/objects.buttons";

    $inuit-enable-layout--middle:   true;
    @import "bower_components/inuit-layout/objects.layout";

    @import "bower_components/inuit-media/objects.media";

    $inuit-enable-flag--rev:        true;
    $inuit-enable-flag--responsive: true;
    @import "bower_components/inuit-flag/objects.flag";

You could also chunk your inuitcss overrides into their own file,
`settings.inuitcss`, for example. Again, this (as with all inuitcss overrides)
needs `@importing` **before** the inuitcss partial to which it relates.

This method of modifying the framework means that you don’t need to edit any
files directly (thus making it easier to update the framework), but also means
that you’re not left with huge, bloated, monolithic variables files from which
you need to configure an entire library.

## Off by default

In the interests of reducing the amount of code in your project, all of
inuitcss’ module-variants are turned off by default. This gives inuitcss two
layers of reduced bloat:

1. **You only include the specific files you need**, so you’re immediately
   starting with a very trimmed down codebase.
2. **Any variants are switched off by default**, so if you _just_ want buttons,
   you don’t get every different size and permutation of them unless you
   explicitly tell inuitcss you want them.

To turn features on, just set their switches to true (again, _before_ you
`@import` the file):

    $inuit-enable-btn--full:    true;
    $inuit-enable-btn--large:   true;
    @import "bower_components/inuit-buttons/objects.buttons";

## Extending inuitcss

Two things about inuitcss make it very extensible. Firstly, it is a framework in
its truest sense; it is designed to lay an unopinionated foundation upon which
_you_ do the majority of the work. Secondly, scalability is one of inuitcss’
core principles, so it is designed to get larger over time.

Extending inuitcss is made very simple because of its very decoupled nature. As
opposed to having a monolithic framework which acts as one giant black box, you
can add your own functionality in and around inuitcss code. This means that you
can grow your codebase in any direction from any point. inuitcss has some
default tooling, but there’s no reason you cannot create your own tools
partials, there is no reason why you couldn’t add some of your own objects that
inuitcss doesn’t have.

To extend inuitcss, simply create a partial in the `<section>.<file>` format,
and `@import` it wherever it is needed.

As you can see in inuitcss’ implementation on my own site, I have `@imported`
the default inuitcss `base.page` module, and also added [one of my own to extend
the default module’s functionality](https://github.com/csswizardry/csswizardry.github.com/blob/5a6bfbabc5f30b717d57e075a8f9261062830b31/css/csswizardry.scss#L116-L117).

**inuitcss is not designed to do your work for you, it is designed to help you
do your own work _faster_.**

### Aliases

In order to avoid clashes with your own code, all of inuitcss’ mixins and
variables are namespaced with `inuit-`, for example: `$inuit-base-spacing-unit`.
These variables and mixins can become very tedious and time consuming to type
over and over, so it is recommended that you alias them to something a little
shorter. You can do this by creating a `tools.aliases` file
(`_tools.aliases.scss`) which would be populated with code like this:

    // Reassign `$inuit-base-spacing-unit` to `$spacing-unit`.
    $spacing-unit: $inuit-base-spacing-unit;

    // Reassign lengthy font-size mixin to `font-size()`.
    @mixin font-size($args...) {
        @include inuit-font-size($args...);
    }

You can now use your own aliases onto inuitcss’ defaults throughout your
project.

### Components

inuitcss is a design-free, OOCSS framework—it does its best to provide zero
cosmetic styling. This means that inuitcss can be used on any and all types of
project (and it has been) without dictating (or even suggesting) a
look-and-feel. If you do require a UI out of the box, then inuitcss is probably
not the best tool for you. I’d recommend looking at a UI Toolkit such as
[Bootstrap](http://getbootstrap.com/).

Because inuitcss does no cosmetic styling, it is up to you to author the
Components layer. Components are small partials that contain discrete chunks of
UI that utilise the layers that came before it, for example, a carousel, or a
dropdown nav, or an image gallery, and so on.

## Namespacing

inuitcss is designed for use on larger projects, where namespacing can often be
very useful. With this in mind, inuitcss contains two ways in which you can
namespace its modules: globally, or on a per-component basis.

### Global namespacing

If you want the entire framework to carry a namespace, you simply need to
predefine the `$inuit-namespace` variable held in `settings.defaults`, like so:

    $inuit-namespace: inuitcss-;
    @import "bower_components/inuit-defaults/settings.defaults";

Now every class in every module that inuitcss imports will be prepended with
`inuitcss-`, e.g. `.flag` now becomes `.inuitcss-flag`. This allows you to
visually denote which classes are your own, and which are inuitcss’, and also
helps reduce the chance of collisions.

### Module namespacing

If you do not wish to set a global namespace, you can set namespaces on
individual `@imports`, e.g.:

    $inuit-flag-namespace: foo-;
    @import "bower_components/inuit-flag/objects.flag";

Now the flag object’s class is `.foo-flag`, but the rest of inuitcss remains
un-namespaced.

#### Combining the two

You can have a combination of global and per-component namespacing in a project:

    $inuit-namespace: inuitcss-;
    @import "bower_components/inuit-defaults/settings.defaults";

    ...

    $inuit-flag-namespace: foo-;
    @import "bower_components/inuit-flag/objects.flag";

Now all of your inuitcss modules will have a prefix of `inuitcss-`, except the
flag object, whose namespace is `foo-`.

## Learn by example

My site, [CSS Wizardry](http://csswizardry.com), is built upon inuitcss. View
the source code to see how things piece together, and hopefully reverse engineer
things from there: [github.com/…/csswizardry.github.com/…/css](https://github.com/csswizardry/csswizardry.github.com/tree/master/css)
