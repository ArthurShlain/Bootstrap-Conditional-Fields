This script allows you to show/hide fields depending on the values of another fields.
This version tested with Bootstrap 3.

Funtion to update fields state:

```php
function init_conditional_fields(){
  function update_fields() {
    var $fields = $('[data-condition][data-condition-value]'), $field, condition, val, $trigger, trigger_value;
    $.each($fields, function (value) {
        $field = $(this);
        condition = $field.attr('data-condition');
        val = $field.attr('data-condition-value').toString().split(';');
        $trigger = $('[name="' + condition + '"]');
        if ($trigger.length) {
            trigger_value = $trigger.val().toString();
            if($trigger.is('[type="checkbox"]')){
                trigger_value = $trigger.prop( "checked" ) ? '1' : '0';
            }
            if ($.inArray(trigger_value, val) !== -1) {
                if (!$field.is(':visible'))
                    $field.css('display', 'none').removeClass('hidden').slideDown(500);
            }
            else {
                if ($field.is(':visible')) {
                    $field.slideUp(500, function () {
                        $(this).addClass('hidden');
                    });
                }
            }
        }
    });
  }

  $('.condition-trigger').on('change', function () {
      update_fields();
  });

  update_fields();
}
```

Usage example:

```html
<form>
  <div class="form-group">
    <label for="field1">Field 1</label>
    <select name="field1" id="field1" class="form-control">
      <option value="1">No</option>
      <option value="2">Yes</option>
      <option value="3">No</option>
      <option value="4">No</option>
      <option value="5">Yes</option>
    </select>
  </div>
  <div class="form-group" data-condition="field1" data-condition-value="2;5">
    <label for="field2">Field 2</label>
    <input name="field2" id="field2" type="text" class="form-control condition-trigger">
  </div>
</form>
```
