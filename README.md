![Acquire](https://acquire.io/wp-content/themes/acquire/assets/images/common/acquire-logo.svg "Acquire")


# custom-cards

## Introduction
Custom cards allow data display of other systems to be shown within the unified view of the Acquire. Custom cards appear within the middle and right hand positions of the dashboard. Using this feature, custom apps can create a card to display data info on contact.

<br>

![dashboard](screenshots/dashboard.png)

* Interaction-cards (Middle of agent dashboard)
* General-cards (Right-side of agent dashboard)

Setting up cards
<br>
Details on the card reflected by component properties, and these properties can be linked to other system. On the agent dashboard 

<br>

### There are currently two types of custom card making:
* App Card - 
* Manual card - 

### Components
|Name|description|
|---|---|
|<code>Text</code>|<strong>type</strong> - text<br><strong>text</strong> - this is demo text<br> <strong>displayStyle</strong> - header/paragraph <br> <strong>style</strong> - error/muted/success/normal <br><strong>align</strong> - right/left/center|
|<code>Image</code>|<strong>type</strong> - image<br><strong>url</strong> - https://acquire.io<br> <strong>height </strong> - number [default 100%] <br> <strong>width</strong> - number [default 100%]<br><strong>align</strong> - right/left/center<br><strong>rounded</strong> - true/false (default -> false)|
|<code>Link</code>|<strong>type</strong> - link<br><strong>url</strong> - https://acquire.io<br> <strong>visibleText</strong> - text of redirect url<br> <strong>showLink</strong> - true/false (default -> false)|
|<code>List</code>|<strong>type</strong> - list<br><strong>items[]</strong> - array of items - <code><br>[<br><strong>type</strong> - item_list<br><strong>title</strong> - header text of list<br><strong>style</strong> - text<br><strong>title</strong> - text<br><strong>action</strong> - not required, if given (same as individual items action)<br> ]</code>|
|<code>Data Table</code>|<strong>type</strong> - data-table<br><strong>title</strong> - any text<br> <strong>verticalAlign</strong> - top/middle/bottom (default-> top)<br> <strong>bordered</strong> - true/false (default -> false)<br> <strong>items</strong> - array of text to display<code><br>[<br><strong>type</strong> - item (required)<br><strong>key </strong> - text to display(required)<br><strong>value</strong> - text to display(required)<br><strong>style</strong> - same/dark/light/inverted (for formatting of both text-> diff color/dark color/light color)<br> ]</code><br><strong>style</strong> - list/table (default ->list)<br><strong>column</strong> - no of number (default 1) (only used when style is list)<br><strong>space</strong> - non-linear or none (default is linear)<br><strong>subTextAlign</strong> - left/right -> (default is left)|
|<code>Cards</code>|<strong>type</strong> - card<br><strong>style</strong> - single/vertical/horizontal (default horizontal)<br> <strong>items</strong> - array of item - <code><br>[<br><strong>type</strong> - item<br><strong>title</strong> - header text<br><strong>subtitle </strong> - paragraph text<br><strong>image</strong> - object <br>{<br><strong>url</strong> - img url<br><strong>width</strong> - number (default 100%)<br><strong>height</strong> - number (default 100%)<br><strong>rounded</strong> - true/false (default -> false)<br>}<br><strong>align </strong> - left/center/right (default-> left)<br><strong>action</strong> - same as other individual item<br><strong>text</strong> - array of text and style(same single object as text<br><strong>buttons </strong> - array of buttons same single object as button<br>]</code>|
|<code>Divider</code>|backend - <br>frontend - |
|<code>Cards</code>|backend - <br>frontend - |
|<code>Button</code>|backend - <br>frontend - |
|<code>Feedback</code>|backend - <br>frontend - |
|<code>Section</code>|backend - <br>frontend - |
|<code>Json-to-html</code>|backend - <br>frontend - |
|<code>Checkbox</code>|backend - <br>frontend - |
|<code>Input</code>|backend - <br>frontend - |
|<code>Radio</code>|backend - <br>frontend - |
|<code>Single Select</code>|backend - <br>frontend - |
|<code>Badge</code>|backend - <br>frontend - |
|<code>Grid</code>|backend - <br>frontend - |

### Card JSON object schema:

|Key|Type|description|
|---|---|---|
|<code>type</code>|<code>string</code>|block - <br>action - <br><strong>tab</strong> - The tab renders a card on the right side of the dashboard as part of the app.<br>script_tags - <br>style -|
|<code>display_scope</code>|<code>string</code>|home - <br>contact_action - <br>case_action - <br>message_action - <br>picker - <br>main (for other) - |
|<code>config</code>|<code>json</code>|The config object is described in the table below.|
|<code>submit_sheet_url</code>|<code>json</code>|Success|
|<code>area</code>|<code>enum</code>|backend - <br>frontend - |

<br>

### Card Config JSON schema:
<br>

|Key|Type|description|
|---|---|---|
|<code>event</code>|<code>json</code>|desc goes here|
|<code>canvas</code>|<code>json</code>|label - <br>canvas - <br>action_key - <br>action_type - <br>iconImageUrl -|
|<code>action_key</code>|<code>string</code>|desc goes here|
|<code>action_type</code>|<code>string</code>|desc goes here|
|<code>iconImageUrl</code>|<code>string</code>|desc goes here|
|<code>appInfo</code>|<code>json</code>|Success|
|<code>availability</code>|<code>json</code>|Success|
|<code>can_edit</code>|<code>bool</code>|desc goes here|
|<code>can_initialize</code>|<code>bool</code>|desc goes here|
|<code>can_submit</code>|<code>bool</code>|desc goes here|
|<code>can_submit_sheet</code>|<code>bool</code>|desc goes here|
|<code>can_configure</code>|<code>bool</code>|desc goes here|
|<code>can_options</code>|<code>bool</code>|desc goes here|
|<code>order</code>|test|test|

