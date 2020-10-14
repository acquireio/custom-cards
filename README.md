![Acquire](https://acquire.io/wp-content/themes/acquire/assets/images/common/acquire-logo.svg "Acquire")


# Acquire-cards

## Introduction
Acquire cards are used to place containers around the respective set of information. The cards allow data display of external systems to be shown within the unified view of the Acquire. 
Acquire cards appear within the middle and right hand positions of the dashboard.

Acquire has 2 types of cards <strong>app-custom-cards</strong> and <strong>manual-cards</strong>.
Once the Acquire card is configured correctly, your external system information will appear in the Acquire Agent's dashboard.

Acquire card designs are fully customizable. This document explains how to customize the design using Acquire components templates or custom HTML.

#### Use case:
You use the Acquire and manage orders on an external system but the agent wants to see the status of the particular contact's order, then the agent can view, change the information in the Acquire dashboard without switching through the card.

#### Example of Card:
![dashboard](screenshots/dashboard.png)

At the time of sending data through these cards, customer name, email, phone and other fields will be received from the Acquire, you can get that customer data from external systems.
<br>

### There are currently two types of custom card making:
* [App Custom Card](#app-custom-card) 
* [Manual Card](#manual-card)

### Theme options
* Default template
* Custom HTML

### Card Location
* Interaction-cards (Middle of agent dashboard)
* General-cards (Right-side of agent dashboard)

<br>

## App Custom Card
### Procedure:

#### Your side: 
You must add an API endpoint that responds to GET requests with a query and returns a JSON payload. In return, you can send a default template or custom HTML. Examples of default templates are given below.
#### Create App Custom Card: 
 * Go to AppStore.
 * Click on Custom Card App & Install.
 * Add your API endpoint URL in the app settings to get the information on the card. Apart from this, you can also add an optional Authorization Header(Basic Auth or Bearer). 
 `Example: https://example.com/user?email={{contact.email}}&field={{contact.custom_field_key}}`
 this endpoint URL Acquire will call for dynamic data and It can return the default template or custom HTML.
 * Add the default template or custom HTML, that will provide information from external systems.
 
![appstore](screenshots/app-custom-card.png)

![appstore1](screenshots/app-custom-card-1.png)

![appstore2](screenshots/sample-card-return.png)

![appstore3](screenshots/card-view.png)
 
 
 ### Example endpoint URL code:
 ```
app.post("/card-initialize", (req, res, next) => {
    console.log('contact-information', req.body);
    res.send({
        "canvas": {
            "content": {
                "components": [
                    {
                        "type": "card",
                        "style": "single",
                        "items": [
                            {
                                "type": "item",
                                "title": "Judi Colton",
                                "subtitle": "Tech Head, California",
                                "bordered": true,
                                "align": "center",
                                "image": {
                                    "url": "https://cdn.pixabay.com/photo/2015/03/03/18/58/girl-657753_960_720.jpg",
                                    "height": 300
                                },
                                "action": {
                                    "type": "url",
                                    "url": "https://google.com/0"
                                },
                                "text": [
                                    {
                                        "type": "text",
                                        "text": "This is paragraph text. Here's a [link](https://developers.intercom.io/). Here's some *bold text*. Lorem ipsum.",
                                        "displayStyle": "paragraph"
                                    },
                                    {
                                        "type": "text",
                                        "text": "This is muted text. Here's a [link](https://developers.intercom.io/). Here's some *bold text*. Lorem ipsum.",
                                        "style": "muted"
                                    },
                                    {
                                        "type": "text",
                                        "text": "This is error text. Here's a [link](https://developers.intercom.io/). Here's some *bold text*. Lorem ipsum.",
                                        "style": "error"
                                    },
                                    {
                                        "type": "text",
                                        "text": "This is error text. Here's a [link](https://developers.intercom.io/). Here's some *bold text*. Lorem ipsum.",
                                        "style": "success"
                                    }
                                ],
                                "buttons": [
                                    {
                                        "type": "button",
                                        "label": "Muted button",
                                        "style": "muted",
                                        "action": {
                                            "type": "url",
                                            "url": "https://google.com/5"
                                        }
                                    },
                                    {
                                        "type": "button",
                                        "label": "Error button",
                                        "style": "error",
                                        "action": {
                                            "type": "url",
                                            "url": "https://google.com/6"
                                        }
                                    },
                                    {
                                        "type": "button",
                                        "label": "Success button",
                                        "style": "success",
                                        "action": {
                                            "type": "url",
                                            "url": "https://google.com/7"
                                        }
                                    }
                                ]
                            }
                        ]
                    }
                ]
            }
        }
    });
});
```

## Manual Card

### Procedure

To create manual cards:
 1. First of all, you have to configure the Acquire Card space & location. It can be done by using [create card API](https://apidocs.acquire.io/#03597018-51dc-4e3f-9dc2-401ca5422b68). 
 Make sure that you have added the <code>initialize_url</code> endpoint URL properly. At this endpoint you will get contact data and you can return a customized template or HTML with the data.
 
 2. Test card
 
  
 ##### Sample code to create ard space & location: 
  ```
 var request = require('request');
 
 var options = {
 'method': 'POST',
 'url': 'https://{{YOUR_ACQUIRE_ACCOUNT_URL}}/api/v1/crm/ui-component',
 'headers': {
 'Authorization': 'Bearer {{YOUR_API_KEY}}',
 'Content-Type': 'application/json'
 },
 
 body: JSON.stringify({"type":"tab","config":{"label":"Sample Card","canvas":{"content_url":true},"action_key":"test-json","action_type":"initialize_tab","iconImageUrl":"./assets/app-store/acquire_saml.svg","initialize_url":"https://226069089919.ngrok.io/mix2-initialize"},"displayScope":"contact_action","area":"backend"})
 };
 
 request(options, function (error, response) {
 if (error) throw new Error(error);
 console.log(response.body);
 });
 
 ```




#### Supported Types & default template components schema

When creating a card, there is a collection of supported types that can be included in the schema. These types are essentially UI controls that interact to provide content or data to the user card.

<strong>Available JSON key for templating:</strong>

|Name|description| Notes |
|---|---|---|
|<code>Text</code>|<strong>type</strong> - text<br><strong>text</strong> - this is demo text<br> <strong>displayStyle</strong> - header/paragraph <br> <strong>style</strong> - error/muted/success/normal <br><strong>align</strong> - right/left/center|Represents a paragraph|
|<code>Image</code>|<strong>type</strong> - image<br><strong>url</strong> - https://acquire.io<br> <strong>height </strong> - number [default 100%] <br> <strong>width</strong> - number [default 100%]<br><strong>align</strong> - right/left/center<br><strong>rounded</strong> - true/false (default -> false)|Embed an image|
|<code>Link</code>|<strong>type</strong> - link<br><strong>url</strong> - https://acquire.io<br> <strong>visibleText</strong> - text of redirect url<br> <strong>showLink</strong> - true/false (default -> false)|Define external resource|
|<code>List</code>|<strong>type</strong> - list<br><strong>items[]</strong> - array of items - <code><br>[<br><strong>type</strong> - item_list<br><strong>title</strong> - header text of list<br><strong>style</strong> - text<br><strong>title</strong> - text<br><strong>action</strong> - not required, if given (same as individual items action)<br> ]</code>|Defines the item in the list|
|<code>Data Table</code>|<strong>type</strong> - data-table<br><strong>title</strong> - any text<br> <strong>verticalAlign</strong> - top/middle/bottom (default-> top)<br> <strong>bordered</strong> - true/false (default -> false)<br> <strong>items</strong> - array of text to display<code><br>[<br><strong>type</strong> - item (required)<br><strong>key </strong> - text to display(required)<br><strong>value</strong> - text to display(required)<br><strong>style</strong> - same/dark/light/inverted (for formatting of both text-> diff color/dark color/light color)<br> ]</code><br><strong>style</strong> - list/table (default ->list)<br><strong>column</strong> - no of number (default 1) (only used when style is list)<br><strong>space</strong> - non-linear or none (default is linear)<br><strong>subTextAlign</strong> - left/right -> (default is left)|Tabular data entry|
|<code>Cards</code>|<strong>type</strong> - card<br><strong>style</strong> - single/vertical/horizontal (default horizontal)<br> <strong>items</strong> - array of item - <code><br>[<br><strong>type</strong> - item<br><strong>title</strong> - header text<br><strong>subtitle </strong> - paragraph text<br><strong>image</strong> - object <br>{<br><strong>url</strong> - img url<br><strong>width</strong> - number (default 100%)<br><strong>height</strong> - number (default 100%)<br><strong>rounded</strong> - true/false (default -> false)<br>}<br><strong>align </strong> - left/center/right (default-> left)<br><strong>action</strong> - same as other individual item<br><strong>text</strong> - array of text and style(same single object as text<br><strong>buttons </strong> - array of buttons same single object as button<br>]</code>| Content container |
|<code>Divider</code>|<strong>type</strong> - divider<br><strong>style</strong> - dotted/solid (default solid)<br> <strong>size</strong> - xs/x/m/l/xl (top bottom spaces)(default is m)<br> <strong>fullWidth</strong> - true/false (default false)|Divides a whole into parts vertical.|
|<code>spacer</code>|<strong>type</strong> - spacer<br><strong>size</strong> - dxs/s/m/l/xl|Create space|
|<code>Button</code>|<strong>type</strong> - button<br><strong>label</strong> - text to display<br> <strong>style</strong> - primary/secondary/link/muted/error/success/outlined  (default primary)<br> <strong>size</strong> - xs/s/m/l/xl (default m)<br> <strong>action</strong> - same as other individual item|Defines a clickable|
|<code>Feedback</code>|<strong>type</strong> - feedback<br><strong>label</strong> - string text to display<br> <strong>style</strong> - star/ thumbs<br> <strong>ratings</strong> - number (if style is star > if >5 then it will show max 5) (default is 5)|Rating picker|
|<code>Section</code>|<strong>type</strong> - section<br><strong>Items</strong> - array of components||
|<code>Json-to-html</code>|<strong>type</strong> - json-to-htm<br><strong>json</strong> - json object of html markdown||
|<code>Checkbox</code>|<strong>type</strong> - checkbox<br><strong>label</strong> - text to display<br><strong>value</strong> - <br><strong>items</strong> - array of checkbox item (label, value, checked)<br><strong>action</strong> - same as other individual item|Checkbox item list|
|<code>Input</code>|<strong>type</strong> - input/textarea<br><strong>label</strong> - text to display<br><strong>value</strong> - <br><strong>placeholder</strong> - <br><strong>action</strong> - same as other individual item|Specifies an input field where the user can enter data|
|<code>Radio</code>|<strong>type</strong> - radio<br><strong>label</strong> - text to display<br><strong>value</strong> - <br><strong>id</strong> - <br><strong>action</strong> - same as other individual item<br><strong>Items</strong> - array of radio item (label, value, checked)|Radio option list|
|<code>Single Select</code>|<strong>type</strong> - single-select<br><strong>label</strong> - text to display<br><strong>Items</strong> - array of item  to display in dropdown (label, value, id)|Single select dropdown list|
|<code>Badge</code>|<strong>type</strong> - badge<br><strong>text</strong> - text to display<br><strong>style </strong> - primary/success/error/warning/muted (default primary)<br><strong>bordered</strong> - true/false<br><strong>rounded</strong> -  true/false<br><strong>displayType</strong> - primary/secondary/advanced/advanced-secondary|Badges are used to add additional information to any content|
|<code>Grid</code>|<strong>type</strong> - grid<br><strong>header</strong> - array of header data<br><code>[{<br><strong>key </strong> -unique key for data (must be same for body data)<br><strong>text</strong> - text to display(required)<br><strong>width</strong> - to uniquely give width to columns (not required)<br>}]</code><br><strong>data</strong> - <code>[{array of body data}]</code><br><strong>title</strong> - title of the grid (not required)<br><strong>emptyChar</strong> - text to display when there is no data (not required)<br><strong>columnsWidth</strong> - same (for same width of columns ) (not required)|A grid consists of a parent element, with one or more child elements|

#### Text
![dashboard](screenshots/text-sample.png)
```
app.post("/text-initialize", (req, res, next) => {
    console.log('contact-information', req.body);
    res.send({
        "canvas": {
            "content": {
                "components": [
                    {
                        "type": "text",
                        "text": "This is a header",
                        "displayStyle": "header"
                    },
                    {
                        "type": "text",
                        "text": "This is a header",
                        "displayStyle": "header",
                        "style": "error",
                        "align": "right"
                    },
                    {
                        "type": "text",
                        "text": "This is a header",
                        "displayStyle": "header",
                        "style": "success",
                        "align": "right"
                    },
                    {
                        "type": "text",
                        "text": "This is a header",
                        "displayStyle": "header",
                        "style": "muted",
                        "align": "center"
                    },
                    {
                        "type": "text",
                        "text": "This is paragraph text. Here's a [link](https://developers.intercom.io/). Here's some *bold text*. Lorem ipsum.",
                        "displayStyle": "paragraph"
                    },
                    {
                        "type": "text",
                        "text": "This is muted text. Here's a [link](https://developers.intercom.io/). Here's some *bold text*. Lorem ipsum.",
                        "style": "muted"
                    },
                    {
                        "type": "text",
                        "text": "This is error text. Here's a [link](https://developers.intercom.io/). Here's some *bold text*. Lorem ipsum.",
                        "style": "error"
                    },
                    {
                        "type": "text",
                        "text": "This is error text. Here's a [link](https://developers.intercom.io/). Here's some *bold text*. Lorem ipsum.",
                        "style": "success"
                    },
                    {
                        "type": "text",
                        "text": "Left aligned",
                        "align": "left"
                    },
                    {
                        "type": "text",
                        "text": "Center aligned",
                        "align": "center"
                    },
                    {
                        "type": "text",
                        "text": "Right aligned",
                        "align": "right"
                    }
                ]
            }
        }
    });
});
```

#### Image
![dashboard](screenshots/image-sample.png)
```
app.post("/image-initialize", (req, res, next) => {
    console.log('contact-information', req.body);
    res.send({
        "canvas": {
            "content": {
                "components": [
                    {
                        "type": "image",
                        "url": "https://i.picsum.photos/id/1025/4951/3301.jpg"
                    },
                    {
                        "type": "image",
                        "width": 200,
                        "url": "https://i.picsum.photos/id/1025/4951/3301.jpg"
                    },
                    {
                        "type": "image",
                        "height": 200,
                        "url": "https://i.picsum.photos/id/1025/4951/3301.jpg"
                    },
                    {
                        "type": "image",
                        "width": 200,
                        "height": 200,
                        "align": "right",
                        "url": "https://i.picsum.photos/id/1025/4951/3301.jpg"
                    },
                    {
                        "type": "image",
                        "width": 200,
                        "height": 200,
                        "align": "center",
                        "url": "https://i.picsum.photos/id/1025/4951/3301.jpg"
                    },
                    {
                        "type": "image",
                        "rounded": true,
                        "url": "https://i.picsum.photos/id/1025/4951/3301.jpg"
                    },
                    {
                        "type": "image",
                        "width": 200,
                        "height": 200,
                        "rounded": true,
                        "url": "https://i.picsum.photos/id/1025/4951/3301.jpg"
                    }
                ]
            }
        }
    });
});
```

#### Link
![dashboard](screenshots/link-sample.png)
```
app.post("/link-initialize", (req, res, next) => {
    console.log('body==initialize=', req.body);
    res.send({
        "canvas": {
            "content": {
                "components": [
                    {
                        "type": "link",
                        "visibleText": "Click Click Click",
                        "url": "https://google.com"
                    },
                    {
                        "type": "link",
                        "visibleText": "Click Click Click",
                        "url": "https://google.com",
                        "showLink": false
                    },
                    {
                        "type": "link",
                        "visibleText": "Click Click Click",
                        "url": "https://google.com",
                        "showLink": true
                    },
                    {
                        "type": "link",
                        "url": "https://google.com",
                        "showLink": false
                    },
                    {
                        "type": "link",
                        "url": "https://google.com",
                        "showLink": true
                    }
                ]
            }
        }
    });
});
```

#### list
![dashboard](screenshots/list-sample.png)
```$xslt
app.post("/list-initialize", (req, res, next) => {
    console.log('contact-information', req.body);
    res.send({
        "canvas": {
            "content": {
                "components": [
                    {
                        "type": "list",
                        "items": [
                            {
                                "type": "item",
                                "id": "selected_article",
                                "title": "**WeChat**",
                                "subtitle": "WeChat is a Chinese multi-purp...",
                                "image": {
                                    "url": "https://picsum.photos/id/0/5616/3744",
                                    "width": 30,
                                    "rounded": true,
                                    "height": 30
                                },
                                "value": "https://5d03c.lml.io/help/wechat",
                                "action": {
                                    "type": "submit"
                                }
                            },
                            {
                                "type": "item",
                                "id": "selected_article",
                                "title": "**Missed Chats**",
                                "subtitle": "You can use the &amp;quot;Filters&amp;...",
                                "image": {
                                    "url": "https://picsum.photos/id/0/5616/3744",
                                    "width": 30,
                                    "height": 30
                                },
                                "value": "https://5d03c.lml.io/help/missed-chats",
                                "action": {
                                    "type": "submit"
                                }
                            },
                            {
                                "type": "item",
                                "id": "selected_article",
                                "title": "**Live Chat Profiles**",
                                "subtitle": "The chat profile provides a de...",
                                "image": {
                                    "url": "https://picsum.photos/id/0/5616/3744",
                                    "width": 30,
                                    "height": 30
                                },
                                "value": "https://5d03c.lml.io/help/chat-profile",
                                "action": {
                                    "type": "submit"
                                }
                            },
                            {
                                "type": "item",
                                "id": "selected_article",
                                "title": "**Dialog Flow Chatbot **",
                                "subtitle": "As you may now know Acquire ha...",
                                "image": {
                                    "url": "https://picsum.photos/id/0/5616/3744",
                                    "width": 30,
                                    "height": 30
                                },
                                "value": "https://5d03c.lml.io/help/dialog-flow-chatbot-integration",
                                "action": {
                                    "type": "submit"
                                }
                            },
                            {
                                "type": "item",
                                "id": "selected_article",
                                "title": "**How to use Live Chat in Acquire**",
                                "subtitle": "This article is a basic overview...",
                                "image": {
                                    "url": "https://picsum.photos/id/0/5616/3744",
                                    "width": 30,
                                    "height": 30
                                },
                                "value": "https://5d03c.lml.io/help/how-to-use-live-chat-in-acquire",
                                "action": {
                                    "type": "submit"
                                }
                            }
                        ]
                    }
                ]
            }
        }

    });
});
```

#### Data Table
![dashboard](screenshots/table-sample.png)
```
app.post("/table-initialize", (req, res, next) => {
    console.log('contact-information', req.body);
    res.send({
        "canvas": {
            "content": {
                "components": [
                    {
                        "type": "data-table",
                        "title": "Order details",
                        "verticalAlign": "middle",
                        "style": "list",
                        "column": "2",
                        "items": [
                            {
                                "type": "item",
                                "key": "Order ID",
                                "value": "AMA#12062020"
                            },
                            {
                                "type": "item",
                                "key": "Order Created Date",
                                "value": "Thursday, 12 March 2020"
                            },
                            {
                                "type": "item",
                                "key": "Order Updated Date",
                                "value": "Thursday, 12 March 2020"
                            },
                            {
                                "type": "item",
                                "key": "Order Status",
                                "value": "Processing"
                            },
                            {
                                "type": "item",
                                "key": "Payment Method",
                                "value": "Gpay"
                            },
                            {
                                "type": "item",
                                "key": "Amount",
                                "value": "10000"
                            },
                            {
                                "type": "item",
                                "key": "Discount Amount",
                                "value": "1000"
                            },
                            {
                                "type": "item",
                                "key": "Offer Applied",
                                "value": "YES"
                            },
                            {
                                "type": "item",
                                "key": "Coupon Applied",
                                "value": "YES"
                            },
                            {
                                "type": "item",
                                "key": "Coupon Amount",
                                "value": "500"
                            },
                            {
                                "type": "item",
                                "key": "TAX",
                                "value": "200"
                            },
                            {
                                "type": "item",
                                "key": "Final Amount",
                                "value": "8700"
                            }
                        ]
                    }
                ]
            }
        }
    });
});
```

#### Cards
![dashboard](screenshots/card-sample.png)
```
app.post("/card-initialize", (req, res, next) => {
    console.log('contact-information', req.body);
    res.send({
        "canvas": {
            "content": {
                "components": [
                    {
                        "type": "card",
                        "style": "single",
                        "items": [
                            {
                                "type": "item",
                                "title": "Judi Colton",
                                "subtitle": "Tech Head, California",
                                "bordered": true,
                                "align": "center",
                                "image": {
                                    "url": "https://cdn.pixabay.com/photo/2015/03/03/18/58/girl-657753_960_720.jpg",
                                    "height": 300
                                },
                                "action": {
                                    "type": "url",
                                    "url": "https://google.com/0"
                                },
                                "text": [
                                    {
                                        "type": "text",
                                        "text": "This is paragraph text. Here's a [link](https://developers.intercom.io/). Here's some *bold text*. Lorem ipsum.",
                                        "displayStyle": "paragraph"
                                    },
                                    {
                                        "type": "text",
                                        "text": "This is muted text. Here's a [link](https://developers.intercom.io/). Here's some *bold text*. Lorem ipsum.",
                                        "style": "muted"
                                    },
                                    {
                                        "type": "text",
                                        "text": "This is error text. Here's a [link](https://developers.intercom.io/). Here's some *bold text*. Lorem ipsum.",
                                        "style": "error"
                                    },
                                    {
                                        "type": "text",
                                        "text": "This is error text. Here's a [link](https://developers.intercom.io/). Here's some *bold text*. Lorem ipsum.",
                                        "style": "success"
                                    }
                                ],
                                "buttons": [
                                    {
                                        "type": "button",
                                        "label": "Muted button",
                                        "style": "muted",
                                        "action": {
                                            "type": "url",
                                            "url": "https://google.com/5"
                                        }
                                    },
                                    {
                                        "type": "button",
                                        "label": "Error button",
                                        "style": "error",
                                        "action": {
                                            "type": "url",
                                            "url": "https://google.com/6"
                                        }
                                    },
                                    {
                                        "type": "button",
                                        "label": "Success button",
                                        "style": "success",
                                        "action": {
                                            "type": "url",
                                            "url": "https://google.com/7"
                                        }
                                    }
                                ]
                            }
                        ]
                    }
                ]
            }
        }
    });
});
```

#### [divider | button | spacer | feedback]
![dashboard](screenshots/mix-sample1.png)
```
app.post("/multi-initialize", (req, res, next) => {
          console.log('contact-information', req.body);
          res.send({
              "canvas": {
                  "content": {
                      "components": [
                          {
                              "type": "divider",
                              "style": "dotted", //dotted/solid (default solid)
                          },
                          {
                              "type": "spacer",
                              "size": "xl" // xs/x/m/l/xl (top bottom spaces)(default is m),
                              "fullWidth" : false //true/false (default false)
                          },
                          {
                              "type": "button",
                              "label": "Normal Button"
                          },
                          {
                              "type": "button",
                              "label": "Normal Button",
                              "style": "primary" //primary/secondary/link/muted/error/success/outlined  (default primary)
                          },
                          {
                              "type": "button",
                              "label": "Secondary button",
                              "style": "secondary"
                          },
                          {
                              "type": "spacer",
                              "size": "xl" // xs/s/m/l/xl (default m)
                          },
                          {
                              "type": "button",
                              "label": "Outlined button",
                              "style": "outlined"
                          },
                          {
                              "type": "button",
                              "label": "Link button",
                              "style": "link"
                          },
                          {
                              "type": "button",
                              "label": "Muted button",
                              "style": "muted"
                          },
                          {
                              "type": "button",
                              "label": "Error button",
                              "style": "error"
                          },
                          {
                              "type": "button",
                              "label": "Success button",
                              "style": "success"
                          },
                          {
                              "type": "spacer",
                              "size": "xl"
                          },
                          {
                              "type": "feedback",
                              "style": "star", //star/ thumbs
                              "label": "How good are you in frontend technologies",
                              "rating": 9 //number (if style is star > if >5 then it will show max 5) (default is 5)
                          },
                          {
                              "type": "feedback",
                              "style": "thumbs",
                              "label": "How good are you in backend technologies"
                          },
                          {
                              "type": "feedback",
                              "style": "thumbs",
                              "size": "l",
                              "label": "Thumbs rating variation"
                          }
                      ]
                  }
              }
          });
      });
```

#### Section
![dashboard](screenshots/section-sample.png)
```app.post("/section-initialize", (req, res, next) => {
       console.log('contact-information', req.body);
       res.send({
           "canvas": {
               "content": {
                   "components": [
                       {
                           "type": "section",
                           "verticalAlign": "middle",
                           "align": "separate",
                           "items": [
                               {
                                   "type": "card",
                                   "style": "horizontal",
                                   "items": [
                                       {
                                           "type": "item",
                                           "title": "Delivery Order #LP01206",
                                           "subtitle": "Pizza can makes anyone happy.",
                                           "image": {
                                               "url": "https://cdn.pixabay.com/photo/2016/05/30/14/10/delivery-guy-1424808_960_720.png",
                                               "width": 50,
                                               "height": 50,
                                               "rounded": true
                                           }
                                       }
                                   ]
                               },
                               {
                                   "type": "list",
                                   "align": "right",
                                   "items": [
                                       {
                                           "type": "item_list",
                                           "style": "button",
                                           "items": [
                                               {
                                                   "type": "button",
                                                   "style": "secondary",
                                                   "label": "Call Restaurant"
                                               },
                                               {
                                                   "type": "button",
                                                   "label": "Support",
                                                   "style": "secondary"
                                               }
                                           ]
                                       }
                                   ]
                               }
                           ]
                       },
                       {
                           "type": "divider"
                       },
                       {
                           "type": "section",
                           "verticalAlign": "top",
                           "align": "separate",
                           "items": [
                               {
                                   "type": "data-table",
                                   "title": "Order Summary",
                                   "verticalAlign": "top",
                                   "style": "table",
                                   "items": [
                                       {
                                           "type": "item",
                                           "key": "Cheezy-7 Pizza",
                                           "value": "3"
                                       },
                                       {
                                           "type": "item",
                                           "key": "Burn to Hell Pizza",
                                           "value": "2"
                                       },
                                       {
                                           "type": "item",
                                           "key": "Veg Red Sauce Pasta",
                                           "value": "1"
                                       },
                                       {
                                           "type": "item",
                                           "key": "Cheese Garlic Bread",
                                           "value": "3"
                                       },
                                       {
                                           "type": "item",
                                           "key": "Total",
                                           "value": "5500",
                                           "style": "same"
                                       }
                                   ]
                               },
                               {
                                   "type": "data-table",
                                   "title": "Order details",
                                   "verticalAlign": "middle",
                                   "style": "list",
                                   "action": {
                                       "type": "button",
                                       "label": "Delivered By"
                                   },
                                   "items": [
                                       {
                                           "type": "item",
                                           "key": "Address",
                                           "value": "1201, Times Square I Thaltej,\nShilaj Rd, opposite Rambag,\nThaltej, Ahmedabad,\nGujarat 380059"
                                       }
                                   ]
                               },
                               {
                                   "type": "image",
                                   "width": 200,
                                   "height": 200,
                                   "align": "right",
                                   "verticalAlign": "middle",
                                   "url": "https://cdn.pixabay.com/photo/2017/12/09/08/18/pizza-3007395_960_720.jpg"
                               }
                           ]
                       },
                       {
                           "type": "divider"
                       },
                       {
                           "type": "list",
                           "items": [
                               {
                                   "type": "item_list",
                                   "style": "button",
                                   "items": [
                                       {
                                           "type": "button",
                                           "label": "Order Again"
                                       },
                                       {
                                           "type": "button",
                                           "label": "Report",
                                           "style": "error"
                                       },
                                       {
                                           "type": "button",
                                           "label": "Rate Us",
                                           "style": "success"
                                       }
                                   ]
                               }
                           ]
                       }
                   ]
               }
           }
       });
   });
```

#### Json-to-html
![dashboard](screenshots/json-sample.png)
```
app.post("/json-initialize", (req, res, next) => {
    console.log('contact-information', req.body);
    res.send({
        "canvas": {
            "content": {
                "components": [
                    {
                        "type": "json-to-html",
                        "json": [
                            {
                                "attributes": [],
                                "children": [
                                    {
                                        "textContent": "hello from",
                                        "type": "text"
                                    },
                                    {
                                        "attributes": [],
                                        "children": [
                                            {
                                                "textContent": "bot.",
                                                "type": "text"
                                            }
                                        ],
                                        "tagName": "strong",
                                        "type": "element"
                                    },
                                    {
                                        "attributes": [],
                                        "children": [
                                            {
                                                "textContent": "this text will show in italic format.",
                                                "type": "text"
                                            }
                                        ],
                                        "tagName": "em",
                                        "type": "element"
                                    },
                                    {
                                        "attributes": [],
                                        "children": [
                                            {
                                                "textContent": "underline.",
                                                "type": "text"
                                            }
                                        ],
                                        "tagName": "u",
                                        "type": "element"
                                    }
                                ],
                                "tagName": "p",
                                "type": "element"
                            }
                        ]
                    }
                ]
            }
        }
    });
});
```

#### Checkbox | input/textarea | radio | single-select |
![dashboard](screenshots/mix-sample2.png)
```
app.post("/mix1-initialize", (req, res, next) => {
    console.log('contact-information', req.body);
    res.send({
        "canvas": {
            "content": {
                "components": [
                    {
                        "_comment1": "this is checkbox",
                        "type": "checkbox",
                        "label": "Sample checkbox example",
                        "value": "",
                        "items": [
                            {
                                "label": "Choice - 1",
                                "value": "1",
                                "checked": ""
                            },
                            {
                                "label": "Choice - 2",
                                "value": "2",
                                "checked": ""
                            },
                            {
                                "label": "Choice - 3",
                                "value": "3",
                                "checked": ""
                            },
                            {
                                "label": "Choice - 4",
                                "value": "4",
                                "checked": ""
                            }
                        ]
                    },
                    {
                        "_comment2": "this is input/textarea",
                        "type": "input", //input/textarea
                        "label": "Sample normal input field",
                        "value": "",
                        "placeholder": "Type here.."
                    },
                    {
                        "type": "input", //input/textarea
                        "label": "Sample input with action button",
                        "value": "",
                        "placeholder": "Type here..",
                        "action": {
                            "type": "event",
                            "value": "acquireIO.trigger('setInputValue','Hi', true)"
                        }
                    },
                    {
                        "type": "textarea", //input/textarea
                        "label": "Sample textarea",
                        "value": "",
                        "placeholder": "Type here.."
                    },
                    {
                        "type": "textarea", //input/textarea
                        "label": "Sample textarea with action button",
                        "value": "",
                        "placeholder": "Type here..",
                        "action": {
                            "type": "event",
                            "value": "acquireIO.trigger('setInputValue','Hello', true)"
                        }
                    },
                    {
                        "_comment3": "this is radio button",
                        "id": "chkb",
                        "type": "radio",
                        "label": "Sample radio button example",
                        "value": "",
                        "items": [
                            {
                                "label": "Choice - 1",
                                "value": "`",
                                "checked": ""
                            },
                            {
                                "label": "Choice - 2",
                                "value": "2",
                                "checked": ""
                            },
                            {
                                "label": "Choice - 3",
                                "value": "3",
                                "checked": ""
                            }

                        ]
                    },
                    {
                        "_comment4": "this is single-select",
                        "type": "single-select",
                        "label": "Sample single select",
                        "items": [
                            {
                                "label": "Select 1",
                                "value": "1",
                                "id": "1"
                            },
                            {
                                "label": "Select 2",
                                "value": "2",
                                "id": "2"
                            },
                            {
                                "label": "Select 3",
                                "value": "3",
                                "id": "3"
                            }
                        ]
                    }
                ]
            }
        }
    });
});
```

#### badge | grid
![dashboard](screenshots/mix-sample3.png)
```
app.post("/mix2-initialize", (req, res, next) => {
    console.log('contact-information', req.body);
    res.send({
        "canvas": {
            "content": {
                "components": [
                    {
                        "type": "badge",
                        "text": "Normal Badge"
                    },
                    {
                        "type": "badge",
                        "text": "Error Badge",
                        "style": "error"
                    },
                    {
                        "type": "badge",
                        "text": "Success Badge",
                        "style": "success"
                    },
                    {
                        "type": "badge",
                        "text": "Warning Badge",
                        "style": "warning"
                    },
                    {
                        "type": "badge",
                        "text": "Mute Badge",
                        "style": "muted"
                    },
                    {
                        "_comment2": "this is a grid",
                        "type": "grid",
                        "header": [
                            {
                                "key": "name",
                                "text": "Name"
                            },
                            {
                                "key": "email",
                                "text": "Email Id"
                            }
                        ],
                        "data": [
                            {
                                "name": "Ellan",
                                "email": "ellan@ellan.com",
                            },
                            {
                                "name": "Jonas",
                                "email": "Mike@Mike.com"
                            },
                            {

                                "name": "Mike",
                                "email": "Mike@Mike.com"
                            },
                            {
                                "name": "Janet",
                                "email": "janet@janet.com",
                            },
                            {
                                "name": "Sheldon",
                                "email": "sheldon@sheldon.com",
                            }
                        ]
                    }
                ]
            }
        }
    });
});
```

