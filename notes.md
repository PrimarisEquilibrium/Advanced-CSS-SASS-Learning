## THE THREE PILLARS OF GOOD HTML & CSS
# Responsive design: *A responsive website is one that all platforms can access.*
# Maintainable and scalable code: *Write code that is clean, easy to understand, growable, and reusable.*
# Web performance: *Build your website in a way that performs quickly.*


# HOW DOES CSS WORK
Load HTML -> Parse HTML --> Document Object Model (DOM)
          -> Load CSS -> Parse CSS ( --> CSS Object Model (CSSOM)
            1. Resolve conflicting CSS declarations [cascade]
            2. Process final CSS values
            )
-> Render Tree -> Website rendering: the visual formatting model -> Final rendered website


# CSS TERMINOLOGY
.my-class <- Selector 
{         <- Declartion block
    color: blue; <- Declartion
    font-size [Property]: 20px [Declared value];
}


# PARSING CSS (CASCADE)
Cascade: Process of combining different stylesheets and resolving conflicts between different CSS rules and declarations, when more than one rule applies to a certain element.

- Author CSS (CSS you write)
- User CSS (CSS the user declares)
- Browser [user agent] (Default browser CSS)

How Cascade Works
Importance > Specificity > Source Order

*IMPORTANCE*
1. User !important declarations
2. Author !important declarations
3. Author declarations
4. User declarations
5. Default browser declartions

*SPECIFICITY*
1. Inline styles
2. IDs
3. Classes, psuedo-classes, attribute
4. Elements, psuedo-elements
(CSS checks all selectors and tallies how many of each of the mentioned specificities exist, then it compares starting from 1 to 4 checking in each category which has the higher number)

*SOURCE ORDER*
- The last declaration in the code will be used.

**IMPORTANT NOTES**:
- CSS declarations marked with !important have the highest priority.
- Only use !important as a last resource, it's better to use correct specificities.
- Inline styles will always have priority over styles in external stylesheets.
- A selector that contains 1 ID is more specific than one with 1000 classes.
- A selector that contains 1 class is more specific than one with 1000 elements.
- The universal selector has no specificity value.
- Rely on specificity rather than order of selectors.
- Rely on order when using 3rd-party stylesheets - always put your author stylesheet last.


# PARSING CSS #2 (Value Processing)
1. Declared value (author declarations)
2. Cascaded value (after the cascade)
3. Specified value (defaulting, if there is no cascaded value)
4. Computed value (converting relative values to absolute)
5. Used value (final calculations, based on layout)
6. Actual value (browser and device restrictions)

- If no values were declared or cascaded then it will use an initial value
- If there is no declaration but a user agent has a default value then it will use that instead
- Certain values are inherited such as children elements, for example a parent font size will be passed to the childrenss specified value if one does not already exist.

How units are converted from relative to absolute (px)
- % (fonts) -> x% * parent's computed font-size
- % (length) -> x% * parent's computed width
- em (font) -> x * parent computed font-size
- em (lengths) -> x * current element computed font-size
- rem -> x * root computed font-size
- vh -> x * 1% of viewport height
- vw -> x * 1% of viewport width  

**IMPORTANT NOTES**:
- Each property has an initial value, used if nothing is declared (and if there is no inheritance).
- Browers specify a root font-size for each page (usually 16px).
- Percentages and relative values are always converted to pixels.
- Percentages are measured relative to their parent's font-size, if used to specify font-size.
- Percentages are measured relative to their parent's width, if used to specify lengths.
- em are measured relative to their parent font-size, if used to specify font-size.
- em are measured relative to the current font-size, if used to specify lengths.
- rem are always measured relative to the document's root font-size.
- vh and vw are simply percentage measurements of the viewport's height and width.


# PARSING CSS #3 (Inheritance)
- Every CSS property MUST have a value
- After checking for specified value it checks for inheritance
- If inheritance is enabled then the specified value is the computed value of parent element

**IMPORTANT NOTES**:
- Inheritance passes the values for some specific properties from parents to children - more maintainable code
- Properties related to text are inherited: font-family, font-size, color, etc;
- The computed value of a property is what gets inherited, not the declared value
- Inheritance of a property only works if no one declares a value for that property
- The inherit keyword forces inheritance on a certain property
- The initial keyword resets a property to its initial value


# WEBSITE RENDERING PHASE (The visual formatting model)
- It is an algorithm that calculates boxes and determines the layout of these boxes, for each element in the render tree, in order to determine the final layout of the page

Factors taken into consideration:
- Dimensions of boxes: the box model
- Box type: inline, block, inline-block
- Positioning scheme: floats and Positioning
- Stacking contexts
- Other elements in the render tree
- Viewport size, dimensions of images, etc

**Box Model**:
Content: text, images, etc
Padding: transparent area around the content, inside of the box
Border: goes around the padding and the content
Margin: space between boxes
Fill area: area that gets filled with background color or background image

- By adding box-sizing: border-box; it causes the width and height to stretch the entire fill area which means adding padding or border won't cause the final width/height to increase, just what you specified

*Box types*:
Block-level boxes (display: block)
- Elements formatted visually as blocks 
- 100% of parent's width
- Vertically, one after another

Inline boxes (display: inline)
- Content is distributed in lines
- Occupies only content's space
- No line-breaks
- No height and widths
- Padding and margins only horizontal

Inline-block (display: inline-block)
- A mix of block and inline
- Occupies only content's space
- No line-breaks
- Box-model applies

*Positioning schemes*:
Normal flow (position: relative)
- Default positioning scheme
- NOT floated
- NOT absolutely positioned
- Elements laid out according to their source order

Floats (float: left/right)
- Element is removed from the normal flow
- Text and inline elements will wrap around the floated element
- The container will not adjust its height to the element

Absolute positioning (position: absolute/fixed)
- Element is removed from the normal flow
- No impact on surrounding content or elements
- We use top, bottom, left, and eirhgt to offset the element from its relatively positioned container

*Stacking contexts*:
- Layers of css elements that create a stack
- z-index with the highest number gets shown on top


# CSS ARCHITECTURE, COMPONENTS, AND BEM
*Think*
- Think about the layout of your webpage or web ape before writing code
Component-Driven Design:
- Modular building blocks that make up interfaces
- Held together by the layout of the page
- Re-usable across a project, and between different projects
- Independent, allowing us to use them anywhere on the page

*Build*
- Build your layout in HTML and CSS with a consistent structure for naming classes
BEM (Block Element Modifier):
- BLOCK: standalone component that is meaningful on its own
- ELEMENT: part of a block that has no standalone meaning
- MODIFIER: a different version of a block or an element
e.g. block__element--modifier

*Architect*
- Create a logical architecture for your CSS with files and folders
The 7-1 Pattern:
- 7 different folders for partial Sass files, and 1 main Sass file to import all other files into a complied CSS stylesheet
7 Folders:
base/
components/
layout/
pages/
themes/
abstracts/
vendors/