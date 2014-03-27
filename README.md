# Abracadabra

A lightweight gem for swapping out text with a fully-compliant Rails form in one click.

Much of the concepts and html mark-up were taken from the awesome [x-editable](http://vitalets.github.io/x-editable/) plugin and the Rails version of this, [x-editable-rails](https://github.com/werein/x-editable-rails). However, this was written from the ground up and uses fully Rails-compliant forms without hacking into x-editable's core files, or overriding them.

## Installation

Add this line to your application's Gemfile:

    gem 'abracadabra'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install abracadabra

## Usage

* Requires JQuery, JQuery-UJS (rails.js), Bootstrap and Font-Awesome (unless you override the framework specific classes with CSS)

In your `application.css`, AFTER Bootstrap (currently only supports Bootstrap), include the css file:

```css
 *= require abracadabra
```

In your `application.js`, AFTER Jquery (required), include the javascript file:

```js
 //= require abracadabra
```

## Helpers

The bread and butter of abracadabra is its helper, `click_to_edit`. Its pretty much as readable as it gets:

```ruby
<%= click_to_edit @user, path: user_path(@user), attribute: :name %>
```

When a user clicks the link generated by this helper, a form with a text field input will replace the link. It's fully Rails compliant, and looks identical to a `form_for` with `remote: true`. Currently, it only responds to javascript, but other datatypes will be supported soon. Here's what it looks like:

![Abracadabra Demo](http://recordit.co/CbgPTahYix.gif "Abracadabra Demo")

The first parameter is the object to be edited, and the only other required parameters are `path` and `attribute`. `path` specifies where the form will be submitted, and `attribute` specifies the column being updated.

It accepts the following optional hash keys (more will be added soon):

```ruby
class: "my-class"
# A class to be added to the text input of the form. The class "abracadabra" is added either way.
# Default: only "abracadabra"

value: "blah"
# An alternate value, other than what object.attribute would return.
# Default: object.attribute

method: "patch"
# HTTP REST method to use. Use anything but "get".
# Default: "patch"

remote: true
# Same as link_to's remote: true, initiates ajax response
# Default: true

type: :js
# Content type -- responds to any content types (:js and :script can both be used to respond with Javascript).
# Default: :script (:js)
# IMPORTANT: Requires the remote: true option to work
```

## Future & Contributing

1. I would love anyone to add date pickers and other alternate field types to this.

2. I would love the different Bootstrap classes to be overridable with an initializer (config/abracadabra.rb) so that any framework could be used. Same with the fonts.

Any other ideas, feel free to contribute!

1. Fork it ( http://github.com/TrevorHinesley/abracadabra/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
