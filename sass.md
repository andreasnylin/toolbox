#Get light or dark color

```css
@function light-or-dark($color) {
	@if (lightness($color) > 50) {
		@return #000;
	}
	@else {
		@return #fff;
	}
}

$color = light-or-dark(#fff); 
/* => #000 */
```
