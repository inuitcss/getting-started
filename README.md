# Getting started

This is the interim documentation for the new inuitcss. Until we get some proper
stuff in place, I hope this will see to 90% of questions and issues.

## As quick as possible

The quickest, simplest way to get started with inuitcss is via the [Starter
Kit](https://github.com/inuitcss/starter-kit). 

NB. If you have not previously installed Bower, first do so globally: 
    $ [sudo] npm install -g bower
then initialize an instance of it in your working directory:
    $ bower init
After that you can simply run

    $ bower install --save inuit-starter-kit

…to grab the correct dependencies, and then import then into a bare Sass project
in the following order:

    @import "bower_components/inuit-defaults/settings.defaults";

    @import "bower_components/inuit-functions/tools.functions";
    @import "bower_components/inuit-mixins/tools.mixins";

    @import "bower_components/inuit-normalize/generic.normalize";
    @import "bower_components/inuit-box-sizing/generic.box-sizing";

    @import "bower_components/inuit-page/base.page";

This source order is imperative, and underpins the entire inuitcss framework.

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

* **Settings**
* **Tools**
* **Generic**
* **Base**
* **Objects**
* **Components** (this is the design layer; this is the one layer that inuitcss
  doesn’t get involved with)
* **Trumps**

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
2. **We reduce the amount of magic numbers in our codebase** because we can
   rationalise where the majority of values in our CSS came from.

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

### Not using Bower?

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

This method of modifying the framework means that you don’t need to edit any
files directly (thus making it easier to update the framework), but also means
that you’re not left with huge, bloated, monolithic variables files from which
you need to configure an entire library.

## Learn by example

My site, [CSS Wizardry](http://csswizardry.com), is built upon inuitcss. View
the source code to see how things piece together, and hopefully reverse engineer
things from there: [github.com/…/csswizardry.github.com/…/css](https://github.com/csswizardry/csswizardry.github.com/tree/master/css)
