# Font Icon

This is a method of including custom icon fonts into your site.  I've been using [fontello.com] (http://fontello.com) to select only the icons I want to use in addition to custom icons I upload.

*Note: upload svg icons at 2048x2048 to avoid resizing issues on horizontal or vertical icons.*

To maintain this file, set some variables to for your font icon text.  Example would be `$icon-world: '\e81';`


## Example
`.item { @include icon-font($fa-github,'font-family',after,.5em,inside,green,true,1.5em); }`


## Usage
`@include icon-font( [$icon], [font-family], [placement], [padding], [alignment], [color], [replace-text], [icon-size] );`


### Icon
Use the variables you created in your variables file.

Example: `$icon-check`


### Font Family
Include the font-family style (or a sass variable).


### Placement
Set the placement of the icon in relation to the element

`before`: the icon is placed before the element [default]

`after`: the icon is placed after the element


### Padding
Specify the amount of spacing between the icon and element.

`px`, `%`, `em`, `rem`

Recommended use of 'em' to keep spacing relevant to element


### Alignment
Specify where the icon should be in relation to the bounding box of the element being applied

`inside`: icon within the bounding box

`outside`: icon outside the bounding box with absolute positioning

_Note: 'outside' applies 'relative' positioning to the element_


### Color
Set the color of the icon. Default will inherit the element color.
`[string]`


### Replace Text
Set the variable to `true` to set the icon only and make the text transparent.  

`false`: [default]

`true`: sets the text to transparent and the icon defaults to #000 unless specified by `[color]`

_Note: The icon will be 1em of whatever you have the font set.  You can set the font size of that particular item larger to make the icon larger and will only affect that class/element selector._

### Icon Size
Set the size of the icon if different than the font size.

`[string]`: use a font size in any valid size attribute.  Default `false`

## Performance

Do not use the 'icon-font' mixin for each icon type/variable.  This will lead to repetitive code output and thus bloat.
	
Instead, use a 'default' variable set to '' and then use Sass Maps to loop through your font variables to specify the content of the individual class.

	$icon-font-family: 'icon-font';
	$icon-placement: before;
	$icon-default: '';
	$icon-padding: 1em;
	$icon-alignment: inside;
	
	
	*[class*='icon'],
	*[class*='icon-only'] {
		@include icon-font( $icon-default, $icon-font-family, $icon-placement, $icon-padding, $icon-alignment, #000, false, false );
	}
	
	@each $icon-class, $icon-variable in 	(name-1, $icon-name-1),
											(name-2, $icon-name-2) {
		*[class*='icon-#{$icon-class}']
		*[class*='icon-only-#{$icon-class}'] {
			&:#{$icon-placement} {
				content: $icon-variable;
			}
		}
	}