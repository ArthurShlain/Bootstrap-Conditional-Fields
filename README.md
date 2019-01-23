This script allows you to show/hide fields depending on the values of another fields.

```php
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
```
