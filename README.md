# App.js - mobile webapps made easy

*App.js* is a lightweight JavaScript UI library for creating mobile webapps that behave like native apps, sacrificing neither performance nor polish.

* cross-platform (Android 2.2+, iOS 4.3+)
* themable platform-specific UI designs
* configurable native-like transitions
* automatically managed navigation stack
* built-in widgets for general use-cases

The goal of App.js is to provide a robust starting point for mobile webapps, handling general scenarios, and maintaining compatiblity with other common JavaScript libraries.

[Check out the documentation here](http://code.kik.com/app/)

## Usage

`$ bower install kik-app --save`

Reference kik-app.js from your application, f.ex from index.html

```html
<script type="text/javascript" src="/bower_components/kik-app/kik-app.js"></script>
```

Also reference the styles like this:

```html
<script type="text/javascript" src="/bower_components/kik-app/dist/app.css"></script>
```

## Stylesheets 

`default.css` (same as `app.css`), includes inline css images
`base.css` excludes inline images and is useful for testing

## Build

Simply concatenate all the files:

`cat src/*.js src/lib/*.js > kik-app.js`

### Integration with popular Javascript MVC frameworks

To integrate with an MVC framework such as Ember.js or Angular.js:

Have your router (or some other "action controller" function or object) call the respective KikApp page controller to do a page transition.

Have a template of some sort

```handlebars
<div class="app-page" data-page="contact">
  <div class="app-topbar">
    <div class="app-title">Contact</div>
  </div>
  <div class="app-content">
    <div class="first-name">{{firstName}}</div>
    <div class="last-name">{{lastName}}</div>
  </div>
</div>
```

```javascript
App.controller('contact', function (page) {
  // Leave it to Ember and handlebars to do the templating
  // $(page).find('.first-name').text(contact.firstName);
  // $(page).find('.last-name' ).text(contact.lastName );
});
```

```javascript
From https://gist.github.com/cavneb/26c4a12b1f77ae868232

import Ember from 'ember';

export default Ember.Route.extend({
  model: function() {
    return this.store.find('contact');
  },

  actions: {
    refresh: function() {
      Ember.run.later(this, function() {
      	// get some data

        this.store.find('contact').then(function(data) {

          // will cause the template to be evaluate and the mustaches {{}} 
          // updated to reflect the incoming controller data
          this.controller.set('content', data); 

          // Transition to the page and make it visible (and on top?)!
          App.load('contact');

        }.bind(this));
      }, 100);
    }
  }
});
```

The above route should of course be generalized in some manner...

Easy as pie ;)


