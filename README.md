Checkbox
========

Drupal Checkbox Tools

https://drupal.org/sandbox/jaesin/2020893

Everyone has said it. "Why doesn't the permissions administration page allow you to check all of the check boxes on a column".

I can't answer that question but I can answer the question how.
 ```javascript
 (function ($) {
  Drupal.behaviors.checkbox = {attach: function (context) {
    var columns = $("#permissions tr.even").first().find("input.form-checkbox").length;

    var heads = $("#permissions thead th");
    for (var i=1; i<columns+1; i++) {
      var cbToggler = $("<input type=checkbox>").data('column', i);
      cbToggler.click(function(e) {
        var checked = this.checked;
        var allCheckboxes = $("#permissions tbody input.form-checkbox");
        for (var n=$(this).data('column')-1; n<allCheckboxes.length; n+=columns) {
          var chkbox = allCheckboxes.get(n);
          chkbox.checked = checked;
        }
      });    
      heads.eq(i).append( $('<div class="checkbox-toggler"/>').append(cbToggler) );
    }
  }};
})(jQuery);
```
