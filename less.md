```css
.text-shadow (@string: 0 1px 3px rgba(0, 0, 0, 0.25)) {
	text-shadow: @string;
}

.box-shadow (@string) {
	-webkit-box-shadow: @string;
	-moz-box-shadow:    @string;
	box-shadow:         @string;
}

.drop-shadow (@x: 0, @y: 1px, @blur: 2px, @spread: 0, @alpha: 0.25) {
	-webkit-box-shadow:	@x @y @blur @spread rgba(0, 0, 0, @alpha);
	-moz-box-shadow:	@x @y @blur @spread rgba(0, 0, 0, @alpha);
	box-shadow:		@x @y @blur @spread rgba(0, 0, 0, @alpha);
}

.inner-shadow (@x: 0, @y: 1px, @blur: 2px, @spread: 0, @alpha: 0.25) {
	-webkit-box-shadow: inset @x @y @blur @spread rgba(0, 0, 0, @alpha);
	-moz-box-shadow:    inset @x @y @blur @spread rgba(0, 0, 0, @alpha);
	box-shadow:         inset @x @y @blur @spread rgba(0, 0, 0, @alpha);
}

.box-sizing (@type: border-box) {
	-webkit-box-sizing: @type;
	-moz-box-sizing:    @type;
	box-sizing:         @type;
}

.border-radius (@radius: 5px) {
	-webkit-border-radius: @radius;
	-moz-border-radius:    @radius;
	border-radius:         @radius;

	-moz-background-clip:    padding;
	-webkit-background-clip: padding-box;
	background-clip:         padding-box;
}

.border-radiuses (@topright: 0, @bottomright: 0, @bottomleft: 0, @topleft: 0) {
	-webkit-border-top-right-radius:    @topright;
	-webkit-border-bottom-right-radius: @bottomright;
	-webkit-border-bottom-left-radius:  @bottomleft;
	-webkit-border-top-left-radius:     @topleft;

	-moz-border-radius-topright:        @topright;
	-moz-border-radius-bottomright:     @bottomright;
	-moz-border-radius-bottomleft:      @bottomleft;
	-moz-border-radius-topleft:         @topleft;

	border-top-right-radius:            @topright;
	border-bottom-right-radius:         @bottomright;
	border-bottom-left-radius:          @bottomleft;
	border-top-left-radius:             @topleft;

	-moz-background-clip:    padding; 
	-webkit-background-clip: padding-box; 
	background-clip:         padding-box; 
}

.opacity (@opacity: 0.5) {
	-webkit-opacity: 	@opacity;
	-moz-opacity: 		@opacity;
	opacity: 		@opacity;
}

.gradient (@startColor: #eee, @endColor: white) {
	background-color: @startColor;
	background: -webkit-gradient(linear, left top, left bottom, from(@startColor), to(@endColor));
	background: -webkit-linear-gradient(top, @startColor, @endColor);
	background: -moz-linear-gradient(top, @startColor, @endColor);
	background: -ms-linear-gradient(top, @startColor, @endColor);
	background: -o-linear-gradient(top, @startColor, @endColor);
}

.horizontal-gradient (@startColor: #eee, @endColor: white) {
 	background-color: @startColor;
	background-image: -webkit-gradient(linear, left top, right top, from(@startColor), to(@endColor));
	background-image: -webkit-linear-gradient(left, @startColor, @endColor);
	background-image: -moz-linear-gradient(left, @startColor, @endColor);
	background-image: -ms-linear-gradient(left, @startColor, @endColor);
	background-image: -o-linear-gradient(left, @startColor, @endColor);
}

.background-size (@backgroundSize) {
	-moz-background-size: @backgroundSize;
	-o-background-size: @backgroundSize;
	-webkit-background-size: @backgroundSize;
	background-size: @backgroundSize;
}

.clearfix() {
	*zoom: 1;

	&:before,
	&:after {
		content: " ";
		display: table;
	}

	&:after {
		clear: both;
	}
}

.center() {
  display: block;
  margin-left: auto;
  margin-right: auto;
}

.inline-block() {
	display: inline-block;
	*display: inline;
	*zoom: 1;
}

.panel(@background: @pink, @padding: @panelPadding, @margin: @panelMargin) {
	background: @background;
	padding: @padding;
	margin: @margin;
}

.reset-list(@margin: 0, @padding: 0) {
	list-style: none;
	margin: @margin;
	padding: @padding;
}

.reset-button(@color: @white, @background: transparent, @border: none) {
	color: @color;
	background: @background;
	border: @border;
}

.stacked-icon-circle(@color) {
	color: @color;
	font-size: @fontSizeStackedIconCircle;
}

.stacked-icon(@color) {
	color: @color;
	font-size: @fontSizeStackedIcon;
}

.word-break(@break: break-all) {
	-ms-word-break: @break;
	word-break: @break;
}

.hyphens(@hyphens: auto) {
	-ms-word-break: break-all;
     word-break: break-all;
	-webkit-hyphens: @hyphens;
	-moz-hyphens: @hyphens;
	-ms-hyphens: @hyphens;
	hyphens: @hyphens;
}
```
