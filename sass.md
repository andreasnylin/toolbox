#Get light or dark color

@function light-or-dark($color) {
	@if (lightness($color) > 50) {
		@return #000000; // Lighter backgorund, return dark color
	}
	@else {
		@return #ffffff; // Darker background, return light color
	}
}
