# Abracadabra

A lightweight gem for swapping out text with a fully-compliant Rails 4 form in one click.

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

The bread and butter of abracadabra is its helper, `click_to_edit`. It's pretty much as readable as it gets:

```ruby
<%= click_to_edit @user, path: user_path(@user), attribute: :name %>
```

When a user clicks the link generated by this helper, a form with a text field input will replace the link. It's fully Rails compliant, and the form markup that is generated is identical to a `form_for` with `remote: true`. Here's what it looks like:

![Abracadabra Demo](http://recordit.co/CbgPTahYix.gif "Abracadabra Demo")

The first parameter of `click_to_edit` is the object to be edited, and the only other required parameters are `path` and `attribute`. `path` specifies where the form will be submitted, and `attribute` specifies the column being updated.

It accepts the following parameters:

```ruby
### REQUIRED ###
path: user_path(@user)
# Specifies where the form will be submitted.

attribute: :name
# Specifies what attribute your text field will be updating.


### OPTIONAL ###
class: "my-class"
# Class(es) to be added to the text input of the form. The class "abracadabra" is added # either way.
# Default: only "abracadabra"

value: "blah"
# An alternate value, other than what object.attribute would return.
# Default: object.attribute

method: "patch"
# HTTP REST method to use. Use anything but "get".
# Default: "patch"

buttonless: true
# Removes submit and cancel buttons, submission and cancellation is then done through the
# Enter/Tab and Escape keys, respectively.
# Default: false

remote: true
# Same as link_to's `remote: true`, form submits via AJAX.
# Default: true

# IMPORTANT: `type` will be ignored if `remote = false` is used. HTML is the default 
# in Rails for standard form submissions.
type: :js
# Content type -- responds to any content type (:js and :script can both be used to respond with Javascript).
# Default: :script (:js)

# IMPORTANT: On ajax:success, this will remove the specific abracadabra instance from 
# the DOM entirely.
# Boolean: DELETE will be submitted without a confirmation dialog
deletable: true
# OR
# String: Confirmation dialog, with the string as the message, will be displayed after 
# clicking the DELETE link
deletable: "Are you sure?"
# Puts a link to DELETE the object (obviously, it always uses DELETE as the HTTP verb).
# Default: false

deletable_path: user_path(@user)
# Specifies where the form will be submitted. 
# Default: path (uses the same path as the main form if `deletable_path` isn't declared).
```

## Configuration

Abracadabra allows some customization. If you would like to change what icon classes are used for the `submit`, `cancel`, and `delete` icons, you can change them globally. 

In any Javascript file that loads **BEFORE** abracadabra's Javascript file that you required above, change any/all of the following variables to suit your project's needs:

```javascript
abracadabraSubmitIcon = "fa fa-check"; // default

abracadabraCancelIcon = "fa fa-times"; // default

abracadabraDeleteIcon = "fa fa-times-circle-o"; // default
```

## Future & Contributing

1. I would love anyone to add date pickers and other alternate field types to this.

2. I would love the different Bootstrap classes to be overridable with an initializer (config/abracadabra.rb), rather than Javascript (not sure if this is even possible), so that any framework could be used. Same with the Font-Awesome button classes.

3. I would love for a `buttons: false` option to be offered that would allow only `Tab`, `Enter` and `Escape` to submit or cancel the form submission.

4. I would love for a `tabbable: true` option to be offered that would tab to the next text input with the `abracadabra` class.

Any other ideas, feel free to contribute!

1. Fork it ( http://github.com/TrevorHinesley/abracadabra/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
