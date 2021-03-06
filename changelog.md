# ImageBox Change Log

## 1.1.2.1
### Changes and new features
* Added missing `GetOffsetRectangle` overload which supports `Rectangle` structs.

### Bug Fixes
* The `ZoomToFit` method didn't support virtual mode and crashed if called.

## 1.1.2.0
### Changes and new features
* Added `IsPointInImage` method. This function returns if a given point is within the image viewport, and is useful for combining with `PointToImage`.
* Added `ImageBorderColor` property, allowing you to customize the color of the image border
* Added a new `ImageBoxBorderStyle`, `FixedSingleGlowShadow`. This style allows for a more smoother outer glow shadow instead of the existing clunky drop shadow.
* Added  `ShowPixelGrid` and `PixelGridColor` properties. When set, a dotted grid is displayed around pixels when zooming in on an image.
* Added new overload to `PointToImage` which allows you to specify if the function should map the given point to the nearest available edge(s) if the point is outside the image boundaries
* Added `AllowDoubleClick` property. When set, the normal double click events and overrides work as expected.
* Additional documentation added via XML comments

### Bug Fixes
* If the `GridDisplayMode` property is set to `Image` an explicit image border is no longer drawn, instead the `ImageBorder` property is correctly honoured.
* Fixes a problem where half the pixels of the first row/column were lost when zooming. Thanks to Rotem for the fix.
* The `GetImageViewport` method now correctly returns a width and height that accounts for control size, padding and zoom levels.
* Fixed incorrect attributes on `AutoSize` property
* Fixes "see also" documentation errors for events

## 1.1.1.0
### Changes and new features
* Added `VirtualMode` and `VirtualSize` properties. These new properties allow you to use all functionality of the ImageBox control without having to set the `Image` property. You can also use the new `VirtualDraw` event to provide custom drawing without having to override existing drawing functionality.

### Bug Fixes
* Fixed the image viewport sometimes being the incorrect size when zoomed in. Thanks to WMJ for the fix.

## 1.1.0.0
### Changes and new features
* Zooming with the mouse is now smoother, and the control attempts to keep the area under the mouse before the zoom in the same area after the zoon.
* Added a `ZoomLevels` property which allows you to configure the different zoom levels supported by the control. Now instead of the control trying to guess the next zoom level, it cycles appropriately through the defined levels. *Currently ZoomLevels (apart from the default series) can only be set at runtime.*
* The `ZoomIncrement` property has been removed due to the introduction of the new zoom levels.
* New `CenterAt` and `ScrollTo` methods allow you to scroll to a given location in the source image.
* Split shortcut handling into two methods `ProcessScrollingShortcuts` for handling arrow keys and `ProcessImageShortcuts` for handling pretty much anything else.
* Added `EnableShortcuts` property, allowing the built in keyboard support to be disabled. When this property is true, `ProcessImageShortcuts` is not called, allowing the control to still be scrolled via the keyboard, but not zoomed etc.
* Zooming can now be performed by the -/+ keys (`OemMinus` and `Oemplus`).
* When zooming (except via mouse action), if the `AutoCenter` property is set, the control will always center the image even when scrollbars are present.
* Nestable `BeginUpdate` and `EndUpdate` methods allow you to disable and enable painting of the control, for example when changing multiple properties at once.
* Added a new `GetSelectedImage` method which creates a new `Bitmap` based on the current selection.
* Added new `FitRectangle` method which takes a given rectangle and ensure it fits within the image boundaries
* The `AllowClickZoom` property now defaults to `false`.
* The `PointToImage` function no longer adds +1 to the result of the function.
* Added a new `ZoomToRegion` method. This will caculate and appropriate zoom level and scrollbar positions to fit a given rectangle.
* Added new `SelectionMode.Zoom`. When this mode is selected, drawing a region will automatically zoom and position the control to fit the region, after which the region is automatically cleared.

### Bug fixes
* Panning no longer tries to activate if no scrollbars are visible
* A new base class, `VirtualScrollableControl` is now used instead of `ScrollableControl`. This removes completely the flicker issues present in previous versions of the control.
* The BorderStyle property has been moved to the `ScrollControl` class, so that borders now correctly surround the control (including scrollbars) rather than just the client area.
* If the `AllowZoomClick` property is `true`, the control no longer magically zooms after panning or selecting a region. Code previously in the `OnMouseClick` override is now in `OnMouseUp`.
* If both `AutoPan` and a valid `SelectionMode` are set, only selections are processed, instead of the control tying to do both. As a result of this fix, setting the `SelectionMode` property no longer resets `AutoPan`
* With the introduction of the `VirtualScrollableControl`, the `MouseWheel` event is now raised as expected.

### Known issues
* The `ScrollProperties` class hasn't been fully integrated with the `ScrollControl`, setting properties on this class won't update the owner control.

## 1.0.0.5
* Initial GitHub release