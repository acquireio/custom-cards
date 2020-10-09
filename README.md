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

