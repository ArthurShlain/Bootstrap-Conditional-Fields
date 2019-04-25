This script allows you to show/hide fields depending on the values of another fields.

Demo: https://codepen.io/ArtZ91/pen/YBPYrm

HTML
```html
<form class="form-conditional">
  <div>
    <label for="field1">Field 1</label>
    <select name="field1" id="field1" class="form-control condition-trigger">
      <option value="1">Option 1</option>
      <option value="2">Option 2</option>
      <option value="3">Option 3</option>
      <option value="4">Option 4</option>
      <option value="5">Option 5</option>
    </select>
  </div>
  <div data-condition="field1" data-condition-value="2;5">
    <label for="field2">Field 2</label>
    <input name="field2" id="field2" type="text" class="form-control condition-trigger">
  </div>
</form>
```

JS
```js
jQuery(function(){
  $('.form-conditional').conditionalFields('init');
});
```

AJAX Example
```js
$.ajax({
  url: '/my-form',
  method: 'GET',
  dataType: "html",
  success: function (html) {
      $('.form-conditional').html(html);
      $('.form-conditional').conditionalFields('update');
  }
});
```

Example: all fields must be valid
```html
<div class="form-group condition-logical-and" data-condition="floors[]" data-condition-value="1">
  ...
</div>
```

Example: at least one field is valid
```html
<div class="form-group condition-logical-or" data-condition="floors[]" data-condition-value="1">
  ...
</div>
```

Adding triggers with delay
```html
<a href="#" data-toggle="collapse" data-target=".my-animated-div" 
   class="condition-trigger-delayed" data-delay="600">I need more fields</a>
