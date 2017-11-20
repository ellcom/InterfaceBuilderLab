# Interface Builder

Interface builder is the tool within Xcode for creating a User Interface via a GUI. 

## History

Interface Builder has been around since 1988, in 2008 a special iPhone version of Interface Builder was released to allow for the building iPhone interfaces. As of Xcode 4 Interface Builder became integrated into Xcode, before this Interface Builder had been its own application.

Sometimes Interface Builder will be refered to as IB. In some cases you may find Interface Builder files called .xib or .nib, this stands for NeXT interface builder dating back to the NeXTSTEP company Steve Jobs created after leaving Apple.

Interface Builder had been used by Tim Berners-Lee to create the WorldWideWeb Browser back in 1990.



## Storyboards

In previous versions of Xcode, a .nib files would be required for each View Controller, As of Xcode 4.2 Storyboards have been available.

One of the notable advantages of Storyboards is *Segues*, Segues allow for linking of View Controllers to other View Controllers within Interface Builders GUI. Previously linking View Controllers would have to be done via code, it is worth noting that you can still link View Controllers together with Code.



## Views

When creating an Interface in Interface Builder, most of the time a View will be used. A View inherits or directly implements the `UIView` Class. A View on the Interface Builder is a rectangular area the handles drawing and touch/gesture events.

Most Objects in the Object library inherit from`UIView`, e.g. Button, TextField, Slider, ...

Views can and are typically nested, i.e. a View sits inside another View. The relationship between nested Views are described as a SuperView and a SubView, the Super being the outer and the Sub being the Inner.



## Auto Layout

Auto Layout is a dynamic way of describing layouts of Views. This can be particularly helpful for designing interfaces that work well on all sizes of the iPhone, with Auto Layout the same described layout can be made to run well on a 4 inch screen threw to a 5.8 inch screen.

Auto Layout is a system of *Constraints* defining size and position of Views within their relative SuperView.

### Getting Started with Auto Layout

Within Interface Builder, the toolbar at the bottom of the editor is where the Auto Layout Menus and Options can be found.



![Interface Builder Toolbar](images/bottom-toolbar.png)



On the left side of the toolbar is the device that the editor is currently displaying, you can change the device to see how the interface will look. Clicking on the current device brings up the options for changing device and Orientation of the device.



![Bottom toolbar device selector](images/bottom-toolbar-device.png)



Next to the iPhone device is the Size Class of the selected device in its orientation, for the iPhone 8 in portrait it is wC hR. This means, compact width and regular height. Changing the device to landscape results in the height becoming compact. Size classes can be used to alter the constraints applied to the Views.

On the left side of the toolbar, a collection of menu's and buttons can be found, from left to right:

- Update Frames, updates the view displayed on the editor with the current constraints applied
- Embed in stack, this will place the selected views inside a Stack View
- Alignment constraints
- Height and Position constraints
- Resolve auto layout issues button



###Height and Position Constraints

Starting with Height and Position constrains or "A new layout constraint". 



![New Constraint](images/new-constraint.png)

A new constraint can have a defined height and width, spacing to nearest neighbour and some additional constraints to be discussed later.



###Alignment Constraints

Alignment constraints allow for positioning views aligned with one another. 



![Alignment Constraint](images/alignment-constraint.png)



To activate this option, you need to `command` + `click` at least two Views from the left side toolbar.



![Cmd Click Views](images/cmd-click-views.png)

### Safe Area

In Xcode 9 the *Safe Area* Layout Guide is available, think of this as a set of margins in which it is safe to draw content within. 

To further illustrate, here is a View Controller root View with a background of Green and a subview that has been given a 0 point positioning to the layout guide edges. 



![Zero Margin to Safe Area](images/safe-area-constraints.png)



The Subview has a black background, here is the layout shown in Portrait



![Safe Area Portrait](images/safe-area-portrait.png)



As shown, the green colour around the edges of the back Subview indicates the Safe Layout Guide, here it the same View in Landscape



![safe-area-landscape](images/safe-area-landscape.png)



The safe area on the iPhone X does not encroach on home button and the *notch*, on the iPhone 8 the safe area is aligned to the edge of the device on the left, bottom and right sides. On the top side when the Top Bar is present, the safe area will be below this.

The safe area will also change when a Bottom Tab Bar or Navigation Bar is present.



### Aligning to Centres of Views

To centre a View within its Superview, the alignment constraint can be used. This constrain in located within the alignment constraint menu.



![Align in Centre](images/align-in-centre.png)



When the device is rotated to landscape, the button will still be in the middle of the Superview.



### Relative Heights and Widths

A height or width can be set to relate to another views height or width, to do this both views need to be selected in the left toolbar and a constraint applied in the Constraints Menu.

In this example I have a View inside a the root View, the Subview is called `GreenView`



![align-in-centre](images/view-inside-root-view.png)



In the example the GreenView will have the same width as the root View and half the height of the root View. The View will be zero aligned to the top and left Safe Area.



![Equal Width Constraint](images/equal-width-constraint.png)



Take care to select both the Safe Area and GreenView is selected. Click Add 1 Constraint To Add the Constraint.

To set the height as half the width of the safe area, repeat the width constraint but for Equal Heights, then in the right side drawer under the Attribute Inspector ![][attribute-inspector] set the Multiplier to be 0.5



![Equal Width Constraint](images/half-height-constraint.png)



**Task 1**

Create a new Projected Called LayoutApp1, implement the above example about applying all constraints However have your view aligned to the bottom of the safe area. Test to make sure that the project Works in Landscape and Portrait.



Example of the completed view:

![Half Height Bottom Aligned](images/half-bottom-task.png)



### Size Class Variation

In some cases constraints may differ between size classes, for example in landscape a constraint may not be needed or should differ from than in landscape.

In this example, we shall work with the last task. In Portrait the height should be equal to half, however in Landscape the height should be equal.

This can be achieved by adding a size class variation to the Equal Height Constraint. In the left side toolbar click on the `GreenView.height = 0.5 × Safe Area.height` constraint, in the right side drawer under the Attribute inspector the constraint is *Installed*, unticking this option uninstalls the constraint. To the left side is a `+` button, Clicking on the button brings up the option to add a Variation based on the height, width and Gamut. Selecting Width: Any, Height: Regular will introduce a variation. 



![Half in portrait](images/half-in-portrait.png)



Notice the constraint has been uninstalled and Installed for hR, this means the constraint will any apply to regular heights.

On the iPhone, All devices in Portrait have the Size class of hR wC and in landscape hC wC.

Setting the height to be equal in landscape can be achieved by having two constraints with variations.



![Half size variation](images/half-full-size-variation.png)



**Task 2** 

Create a new project called LayoutApp2, implement the above example about applying all constraints However in landscape have the GreenView width to be half Safe Area and in portrait have the width to be equal. The GreenView should be Zero Aligned on the top, left and bottom to the safe area. Test to make sure that the project Works in Landscape and Portrait.



### Stack Views

Stack views allows for creating more complicated layouts quicker and easier.



![Stackview](images/stackview.png)



Consider the above layout, to draw this layout using Alignment and Equal Height Constraints would require the following constraints

1. Equal Heights for each view
2. A view with a relative height to the Safe Area
3. Width Constraint for each View
4. Leading Each Constraint
5. Vertical Space Constraints for each view
6. any probably some more...

If after creating these constraints another view needed to be added to the layout, it would not be simple, this is where Stack Views come in.

Stack Views have the following properties:

**Alignment**

How each view is aligned to each edge

**Axis**

How the views within the Stack View are *Stacked*, this can be horizontally (side by side) or vertically (on top of each other)

**Spacing**

How much space is between each of the views

**Distribution**

How each View will fill the available space within the Stack View



To create the above example, three Views will be placed onto a root view, theses sub Views are called GreenView, RedView and BlueView. 



![Embed in Stack View](images/embed-in-stack.png)



To place the views within a Stack View, on the bottom toolbar click on the circled button in the image above, the three views are now sub Views of a Stack View.



![Stack view created](images/stack-view-created-with-errors.png)



In the Attribute inspector of the Stack View you can see the axis, alignment, distribution and spacing properties.



**Task 3**

Create a new project called LayoutApp3, implement the above example, in addition figure out how to add the following:

- Zero Top, Bottom, Leading and trailing edge constraints on the StackView to the Safe Area

- Distribute the views equally so that each views height is equal

- Introduce some spacing between the views

- Add a Variation on the Axis so that in landscape the views are Horizontal

  ​

![Horizontal Stack View](images/stackview-horizontal.png)



Test to make sure that the project Works in Landscape and Portrait, and respect the safe area.



### Intrinsic Size

Sometimes the size of views isn't always known before runtime, for example, when downloading information from the internet or localised strings.

This can be achieved using *Intrinsic Content Size*, the intrinsic content size is dynamic and will be calculated at runtime; this is an *implicit* constraint verses the *explicit* constraints described above.

Not every view has intrinsic content sizing, such as the `UIView` class, however `UILabel` and `UIImageView` do, allowing for downloading of variable length strings and images of differing dimensions from the internet to be able to render correctly at runtime.



### Content Hugging & Content Compression Resistance Priority

Intrinsic content sizes can conflict with other intrinsic content size views, for example, multiple `UILabel` instances stacked horizontally. In this scenario, which label gets "Priority".

A views priority can be described two ways, first by using the **Content Hugging** priority, which says that a view may not grow and is "Hugged". With a higher priority, the more resistance to growth beyond the intrinsic size is applied to the view.

The second, **Compression Resistance** priority which describes how the view will "Resist" being compressed by other views intrinsic size. The higher the priority, the more the view will resist being compressed or "made smaller" than its intrinsic size.



![Resistance & Hugging](images/resistance-hugging.png)



Both the intrinsic size and the priorities can be found in the size inspector ![][size-inspector] in the right side drawer.



![Right Draw under Size Inspector](images/intrinsic-hugging-compression.png)



Content compression resistance priority can be set to any value, however Xcode gives three suggested values:

- 1000 being required priority
- 750 being high priority
- 250 being low priority

The same is true for content hugging priorities.



An **example** use case could be a login screen typically comprising of two textfields and labels, one pair for the username and another for the password. The labels should start about 25 points from the leading edge and have some 10 points spacing before the textfield begins, then the textfield should end 25 points from the trailing edge. However, the textfields should be the same width.



![Intrinsic without constraints](images/intrinsic-example-without.png)



The following constraints allow us to achieve this:

1. Username label leading = Safe area leading + 25
2. Username textfield leading = Username label trailing  + 10
3. Safe area trailing = Username textfield trailing  + 25

To have the text of the label and textarea be level with each other, `alt` + `click` the label and text area and align to baseline.

Repeat these steps for the password label and textfield.

To ensure that the textfield have the same width, `alt` + `click` both textfields to select them both and give them an equal width constraint.

Finish by adding relevant top constraints.



**Task 4**

Complete the example above, test to make sure that the project Works in Landscape and Portrait, respect the safe area and works on the iPhone 8 Plus as well as iPhone SE



## Localisation

The localisation feature within Xcode allows an App to support other languages. When designing an App the first language used to design the interface is known as the base language, once the interface has been designed localisation work can begin. This is where you can add additional language support such as French, there is no limit on the number of languages you can support.

To add localisation support to a project, head over to the project root in the left draw, click project in the editor and work on the info tab. Once here scroll down to the localisations header.



![Localisations header](images/local-default.png)

Click on the plus arrow to add another language, In this example the French Language will be added, at the dialog click Finish.

You now have another language supported. To start adding additional french words to your storyboard, to do this, enable localisation on the storyboard by opening the storyboard in the editor and ticking the french  option in the right drawer under the file tab.



![Enable French](images/local-enable-french.png)



In the left drawer on the storyboard file, a folder has opened up showing a Main.strings (French) file, click on this and change the username and password to their French versions.

Username is "Nom d'utilisateur" and password is "Mot de passe".

To test to make sure that the localisation work has been completed, `alt` + `click` on the simulator device on the toolbar and change the application language to French.



![Change Language](images/local-alt-click.png)



If the intrinsic size has set up the correctly, the label and textfield widths will automatically change to accommodate the content.



**Task 5** 

Create a login screen consisting of:

- Username Label
- Password Label
- Username Textfield
- Password Textfield
- Login Button
- View with all the above inside



![Task 5](images/content-size-constraint.png)



The textfields should be of equal width, have relevant constraints and be of a desired width of 200 points, the login button should be centred, the labels should expand based on their content size.

The View should be centred vertically and horizontally with a constraint saying it must not be any closer then  30 points to the trailing edge of the superview. This means that width of the textfield will be of lesser priority than the trailing edge constraint.

Add French localisation to the storyboard using "s'identifier" for login. Finish by testing the App in two iPhone sizes and both languages.



Example of the App running on the iPhone SE

![task4-8p-en](images/task4-se-fr.png)![task4-8p-en](images/task4-se-en.png) 



Example of the App running on the iPhone 8 plus

![task4-8p-en](images/task4-8p-fr.png)![task4-8p-en](images/task4-8p-en.png)





[attribute-inspector]: images/attribute-inspector.png
[size-inspector]:images/size-inspector.png

