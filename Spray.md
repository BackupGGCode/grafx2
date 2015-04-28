# Spray #

## Left click ##

Selects the spray as the active drawing tool. This drawing tool allows to change the fore and back colors when being in use.

## Right click ##

Displays a menu where you can configure the spray:

**TODO add screenshot of menu**

  * Size: Defines the diameter of the circle in which will effectively fit the spray.
  * Delay: Defines the time interval (in tenth of seconds) that will be waited for between two flows of spray.
  * Mode: Defines whether you want to use a monochrome spray or a multi-colored one.
  * Mono-flow: Defines the number of paintbrushes that will be pasted in the circle of the spray at each cycle.
  * Palette: Left-click on a color of the palette to see how much it will be used in the multicolored flow, and modify it by using the gauge on the right. If the flow of this color was equal to 0, then the "Init" value will be applied. Or set the flow of a color to 0 by clicking on it with the right mouse button.
  * Clear: Removes all the colors from the multicolored flow. Actually, this puts a 0 value in the use of each color.
  * Init: Allows you to define a value that will be set to the color you click on in the palette if its value is equal to 0. This permits to tag a set of colors more quickly.

  * +1,-1,x2,ö2: Modify the values of all the tagged colors (and only them).

Tip: If you often use the Shade mode, and are bored to click many times on a color to reach the color you want, you can define a spray with "Size"=1, "Mono-flow"=1, and "Delay"=2 (or more, according to your reflexes). And then, you'll just have to click a few hundredths of second to modify a color.