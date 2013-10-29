# jQuery

## jQuery hide element on click outside

```javascript
$(document).click(function() {
	$('#myElement').hide();
});

$('#myElement').click(function(e){
    e.stopPropagation();
});
```
