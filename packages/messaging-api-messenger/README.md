# messaging-api-messenger

> Messaging API client for Messenger

<img src="https://static.xx.fbcdn.net/rsrc.php/v3/y8/r/R_1BAhxMP5I.png" alt="Messenger" width="150" />

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [API Reference](#api-reference)
  * [Send API](#send-api)
    * [Content Types](#content-types)
    * [Templates](#templates)
    * [Quick Replies](#quick-replies)
    * [Sender Actions](#sender-actions)
    * [Attachment Upload API](#attachment-upload-api)
    * [Tags](#tags)
  * [User Profile API](#user-profile-api)
  * [Messenger Profile API](#messenger-profile-api)
    * [Persistent Menu](#persistent-menu)
    * [Get Started Button](#get-started-button)
    * [Greeting Text](#greeting-text)
    * [Domain Whitelist](#domain-whitelist)
    * [Account Linking URL](#account-linking-url)
    * [Payment Settings](#payment-settings)
    * [Target Audience](#target-audience)
    * [Chat Extension Home URL](#chat-extension-home-url)
  * [Messenger Code API](#messenger-code-api)
  * [Handover Protocol API](#handover-protocol-api)
  * [Page Messaging Insights API](#page-messaging-insights-api)
  * [Built-in NLP API](#built-in-nlp-api)

## Installation

```sh
npm i --save messaging-api-messenger
```
or
```sh
yarn add messaging-api-messenger
```

## Usage

### Initialize

```js
const { MessengerClient } = require('messaging-api-messenger');

// get accessToken from facebook developers website
const client = MessengerClient.connect(accessToken);
```

You can specify version of Facebook Graph API using second argument:

```js
const client = MessengerClient.connect(accessToken, 'v2.9');
```

If it is not specified, version `v2.10` will be used as default.

## API Reference

All methods return a Promise.

<a id="send-api" />

### Send API - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference)  

#### sendRawBody(body)

###### body

Type: `Object`

```js
client.sendRawBody({
  recipient: {
    id: USER_ID,
  },
  message: {
    text: 'Hello!',
  },
});
```

#### send(userId, message)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### message

Type: `Object`

```js
client.send(USER_ID, {
  text: 'Hello!',
});
```

<a id="content-types" />

### Content Types - [Content types](https://developers.facebook.com/docs/messenger-platform/send-api-reference/contenttypes)

#### sendText(userId, text [, options])

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### text

Type: `String`

###### options

Type: `Object`

```js
client.sendText(USER_ID, 'Hello!');
```

#### sendIssueResolutionText(userId, text)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### text

Type: `String`

```js
client.sendIssueResolutionText(USER_ID, 'Hello!');
```

#### sendAttachment(userId, attachment)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### attachment

Type: `Object`

```js
client.sendAttachment(USER_ID, {
  type: 'image',
  payload: {
    url: 'https://example.com/pic.png',
  },
});
```

#### sendAudio(userId, audio)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/13503473_1584526905179825_88080075_n.png?oh=085ef554f12d061090677b89f3275d64&oe=59EB29D3" alt="sendAudio" width="250" />

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### audio

Type: `String | Buffer | ReadStream`

Send audio using url string:

```js
client.sendAudio(USER_ID, 'https://example.com/audio.mp3');
```

or using `ReadStream` created from local file:

```js
const fs = require('fs');

client.sendAudio(USER_ID, fs.createReadStream('audio.mp3'));
```

#### sendImage(userId, image)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/13466577_1753800631570799_2129488873_n.png?oh=5904aadb6aa82cd2287d777359bd3cd2&oe=59F32D6A" alt="sendImage" width="250" />

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### image

Type: `String | Buffer | ReadStream`

Send image using url string:

```js
client.sendImage(USER_ID, 'https://example.com/vr.jpg');
```

or using `ReadStream` created from local file:

```js
const fs = require('fs');

client.sendImage(USER_ID, fs.createReadStream('vr.jpg'));
```

#### sendVideo(userId, video)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/13509239_1608341092811398_289173120_n.png?oh=160ea165834203bae79c24c8e07137de&oe=5A350DB4" alt="sendVideo" width="250" />

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### video

Type: `String | Buffer | ReadStream`

Send video using url string:

```js
client.sendVideo(USER_ID, 'https://example.com/video.mp4');
```

or using `ReadStream` created from local file:

```js
const fs = require('fs');

client.sendVideo(USER_ID, fs.createReadStream('video.mp4'));
```

#### sendFile(userId, file)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/13480153_1115020735225077_1305291896_n.png?oh=a972010ea3edd1ea967885b06317efab&oe=59F63578" alt="sendVideo" width="250" />

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### file

Type: `String | Buffer | ReadStream`

Send file using url string:

```js
client.sendFile(USER_ID, 'https://example.com/receipt.pdf');
```

or using `ReadStream` created from local file:

```js
const fs = require('fs');

client.sendFile(USER_ID, fs.createReadStream('receipt.pdf'));
```

<a id="templates" />

### Templates - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/templates)

#### sendTemplate(userId, template)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### template

Type: `Object`

```js
client.sendTemplate(USER_ID, {
  template_type: 'button',
  text: 'title',
  buttons: [
    {
      type: 'postback',
      title: 'Start Chatting',
      payload: 'USER_DEFINED_PAYLOAD',
    },
  ],
});
```

#### sendButtonTemplate(userId, title, buttons) - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/button-template)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/13509162_1732711383655205_1306472501_n.png?oh=0e2409226bc50b23207bf37bf6e2edb6&oe=5A377CAC" alt="sendButtonTemplate" width="250" />

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### title

Type: `String`

###### buttons

Type: `Array<Object>`

```js
client.sendButtonTemplate(USER_ID, 'What do you want to do next?', [
  {
    type: 'web_url',
    url: 'https://petersapparel.parseapp.com',
    title: 'Show Website',
  },
  {
    type: 'postback',
    title: 'Start Chatting',
    payload: 'USER_DEFINED_PAYLOAD',
  },
]);
```

#### sendGenericTemplate(userId, elements) - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/generic-template)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/13509251_1026555627430343_1803381600_n.png?oh=e9fadd445090a4743bfd20fda487be5f&oe=59EE4571" alt="sendGenericTemplate" width="250" />

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### elements

Type: `Array<Object>`

```js
client.sendGenericTemplate(USER_ID, [
  {
    title: "Welcome to Peter's Hats",
    image_url: 'https://petersfancybrownhats.com/company_image.png',
    subtitle: "We've got the right hat for everyone.",
    default_action: {
      type: 'web_url',
      url: 'https://peterssendreceiveapp.ngrok.io/view?item=103',
      messenger_extensions: true,
      webview_height_ratio: 'tall',
      fallback_url: 'https://peterssendreceiveapp.ngrok.io/',
    },
    buttons: [
      {
        type: 'postback',
        title: 'Start Chatting',
        payload: 'DEVELOPER_DEFINED_PAYLOAD',
      },
    ],
  },
]);
```

#### sendTaggedTemplate(userId, elements, tag)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### elements

Type: `Array<Object>`

###### tag - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/tags/)

Type: `String`

```js
client.sendTaggedTemplate(
  USER_ID,
  [
    {
      title: "Welcome to Peter's Hats",
      image_url: 'https://petersfancybrownhats.com/company_image.png',
      subtitle: "We've got the right hat for everyone.",
      default_action: {
        type: 'web_url',
        url: 'https://peterssendreceiveapp.ngrok.io/view?item=103',
        messenger_extensions: true,
        webview_height_ratio: 'tall',
        fallback_url: 'https://peterssendreceiveapp.ngrok.io/',
      },
      buttons: [
        {
          type: 'postback',
          title: 'Start Chatting',
          payload: 'DEVELOPER_DEFINED_PAYLOAD',
        },
      ],
    },
  ],
  'GAME_EVENT'
);
```

#### sendShippingUpdateTemplate(userId, elements)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### elements

Type: `Array<Object>`

```js
client.sendShippingUpdateTemplate(USER_ID, [
  {
    title: "Welcome to Peter's Hats",
    image_url: 'https://petersfancybrownhats.com/company_image.png',
    subtitle: "We've got the right hat for everyone.",
    default_action: {
      type: 'web_url',
      url: 'https://peterssendreceiveapp.ngrok.io/view?item=103',
      messenger_extensions: true,
      webview_height_ratio: 'tall',
      fallback_url: 'https://peterssendreceiveapp.ngrok.io/',
    },
    buttons: [
      {
        type: 'postback',
        title: 'Start Chatting',
        payload: 'DEVELOPER_DEFINED_PAYLOAD',
      },
    ],
  },
]);
```

#### sendReservationUpdateTemplate(userId, elements)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### elements

Type: `Array<Object>`

```js
client.sendReservationUpdateTemplate(USER_ID, [
  {
    title: "Welcome to Peter's Hats",
    image_url: 'https://petersfancybrownhats.com/company_image.png',
    subtitle: "We've got the right hat for everyone.",
    default_action: {
      type: 'web_url',
      url: 'https://peterssendreceiveapp.ngrok.io/view?item=103',
      messenger_extensions: true,
      webview_height_ratio: 'tall',
      fallback_url: 'https://peterssendreceiveapp.ngrok.io/',
    },
    buttons: [
      {
        type: 'postback',
        title: 'Start Chatting',
        payload: 'DEVELOPER_DEFINED_PAYLOAD',
      },
    ],
  },
]);
```

#### sendIssueResolutionTemplate(userId, elements)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### elements

Type: `Array<Object>`

```js
client.sendIssueResolutionTemplate(USER_ID, [
  {
    title: "Welcome to Peter's Hats",
    image_url: 'https://petersfancybrownhats.com/company_image.png',
    subtitle: "We've got the right hat for everyone.",
    default_action: {
      type: 'web_url',
      url: 'https://peterssendreceiveapp.ngrok.io/view?item=103',
      messenger_extensions: true,
      webview_height_ratio: 'tall',
      fallback_url: 'https://peterssendreceiveapp.ngrok.io/',
    },
    buttons: [
      {
        type: 'postback',
        title: 'Start Chatting',
        payload: 'DEVELOPER_DEFINED_PAYLOAD',
      },
    ],
  },
]);
```

#### sendAppointmentUpdateTemplate(userId, elements)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### elements

Type: `Array<Object>`

```js
client.sendAppointmentUpdateTemplate(USER_ID, [
  {
    title: "Welcome to Peter's Hats",
    image_url: 'https://petersfancybrownhats.com/company_image.png',
    subtitle: "We've got the right hat for everyone.",
    default_action: {
      type: 'web_url',
      url: 'https://peterssendreceiveapp.ngrok.io/view?item=103',
      messenger_extensions: true,
      webview_height_ratio: 'tall',
      fallback_url: 'https://peterssendreceiveapp.ngrok.io/',
    },
    buttons: [
      {
        type: 'postback',
        title: 'Start Chatting',
        payload: 'DEVELOPER_DEFINED_PAYLOAD',
      },
    ],
  },
]);
```

#### sendGameEventTemplate(userId, elements)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### elements

Type: `Array<Object>`

```js
client.sendGameEventTemplate(USER_ID, [
  {
    title: "Welcome to Peter's Hats",
    image_url: 'https://petersfancybrownhats.com/company_image.png',
    subtitle: "We've got the right hat for everyone.",
    default_action: {
      type: 'web_url',
      url: 'https://peterssendreceiveapp.ngrok.io/view?item=103',
      messenger_extensions: true,
      webview_height_ratio: 'tall',
      fallback_url: 'https://peterssendreceiveapp.ngrok.io/',
    },
    buttons: [
      {
        type: 'postback',
        title: 'Start Chatting',
        payload: 'DEVELOPER_DEFINED_PAYLOAD',
      },
    ],
  },
]);
```

#### sendTransportationUpdateTemplate(userId, elements)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### elements

Type: `Array<Object>`

```js
client.sendTransportationUpdateTemplate(USER_ID, [
  {
    title: "Welcome to Peter's Hats",
    image_url: 'https://petersfancybrownhats.com/company_image.png',
    subtitle: "We've got the right hat for everyone.",
    default_action: {
      type: 'web_url',
      url: 'https://peterssendreceiveapp.ngrok.io/view?item=103',
      messenger_extensions: true,
      webview_height_ratio: 'tall',
      fallback_url: 'https://peterssendreceiveapp.ngrok.io/',
    },
    buttons: [
      {
        type: 'postback',
        title: 'Start Chatting',
        payload: 'DEVELOPER_DEFINED_PAYLOAD',
      },
    ],
  },
]);
```

#### sendFeatureFunctionalityUpdateTemplate(userId, elements)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### elements

Type: `Array<Object>`

```js
client.sendFeatureFunctionalityUpdateTemplate(USER_ID, [
  {
    title: "Welcome to Peter's Hats",
    image_url: 'https://petersfancybrownhats.com/company_image.png',
    subtitle: "We've got the right hat for everyone.",
    default_action: {
      type: 'web_url',
      url: 'https://peterssendreceiveapp.ngrok.io/view?item=103',
      messenger_extensions: true,
      webview_height_ratio: 'tall',
      fallback_url: 'https://peterssendreceiveapp.ngrok.io/',
    },
    buttons: [
      {
        type: 'postback',
        title: 'Start Chatting',
        payload: 'DEVELOPER_DEFINED_PAYLOAD',
      },
    ],
  },
]);
```

#### sendTicketUpdateTemplate(userId, elements)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### elements

Type: `Array<Object>`

```js
client.sendTicketUpdateTemplate(USER_ID, [
  {
    title: "Welcome to Peter's Hats",
    image_url: 'https://petersfancybrownhats.com/company_image.png',
    subtitle: "We've got the right hat for everyone.",
    default_action: {
      type: 'web_url',
      url: 'https://peterssendreceiveapp.ngrok.io/view?item=103',
      messenger_extensions: true,
      webview_height_ratio: 'tall',
      fallback_url: 'https://peterssendreceiveapp.ngrok.io/',
    },
    buttons: [
      {
        type: 'postback',
        title: 'Start Chatting',
        payload: 'DEVELOPER_DEFINED_PAYLOAD',
      },
    ],
  },
]);
```

#### sendListTemplate(userId, items, buttons, topElementStyle) - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/list-template)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/14858155_1136082199802015_362293724211838976_n.png?oh=46900eb955ff8ea1040fc5353d9be2fa&oe=59F245DD" alt="sendListTemplate" width="500" />

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### items

Type: `Array<Object>`

###### buttons

Type: `Array<Object>`

###### topElementStyle

Type: `String`

```js
client.sendListTemplate(
  USER_ID,
  [
    {
      title: 'Classic T-Shirt Collection',
      image_url: 'https://peterssendreceiveapp.ngrok.io/img/collection.png',
      subtitle: 'See all our colors',
      default_action: {
        type: 'web_url',
        url: 'https://peterssendreceiveapp.ngrok.io/shop_collection',
        messenger_extensions: true,
        webview_height_ratio: 'tall',
        fallback_url: 'https://peterssendreceiveapp.ngrok.io/',
      },
      buttons: [
        {
          title: 'View',
          type: 'web_url',
          url: 'https://peterssendreceiveapp.ngrok.io/collection',
          messenger_extensions: true,
          webview_height_ratio: 'tall',
          fallback_url: 'https://peterssendreceiveapp.ngrok.io/',
        },
      ],
    },
  ],
  [
    {
      type: 'postback',
      title: 'Start Chatting',
      payload: 'USER_DEFINED_PAYLOAD',
    },
  ],
  'compact'
);
```

#### sendOpenGraphTemplate(userId, elements) - [Official Docs](https://developers.facebook.com/docs/messenger-platform/open-graph-template)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### elements

Type: `Array<Object>`

```js
client.sendOpenGraphTemplate(USER_ID, [
  {
    url: 'https://open.spotify.com/track/7GhIk7Il098yCjg4BQjzvb',
    buttons: [
      {
        type: 'web_url',
        url: 'https://en.wikipedia.org/wiki/Rickrolling',
        title: 'View More',
      },
    ],
  },
]);
```

#### sendReceiptTemplate(userId, receipt)  - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/receipt-template)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/13466939_915325738590743_1056699384_n.png?oh=bd6869385dee4c2cfaef1329fc660a01&oe=5A0331D4" alt="sendReceiptTemplate" width="250" />

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### receipt

Type: `Object`

```js
client.sendReceiptTemplate(USER_ID, {
  recipient_name: 'Stephane Crozatier',
  order_number: '12345678902',
  currency: 'USD',
  payment_method: 'Visa 2345',
  order_url: 'http://petersapparel.parseapp.com/order?order_id=123456',
  timestamp: '1428444852',
  elements: [
    {
      title: 'Classic White T-Shirt',
      subtitle: '100% Soft and Luxurious Cotton',
      quantity: 2,
      price: 50,
      currency: 'USD',
      image_url: 'http://petersapparel.parseapp.com/img/whiteshirt.png',
    },
    {
      title: 'Classic Gray T-Shirt',
      subtitle: '100% Soft and Luxurious Cotton',
      quantity: 1,
      price: 25,
      currency: 'USD',
      image_url: 'http://petersapparel.parseapp.com/img/grayshirt.png',
    },
  ],
  address: {
    street_1: '1 Hacker Way',
    street_2: '',
    city: 'Menlo Park',
    postal_code: '94025',
    state: 'CA',
    country: 'US',
  },
  summary: {
    subtotal: 75.0,
    shipping_cost: 4.95,
    total_tax: 6.19,
    total_cost: 56.14,
  },
  adjustments: [
    {
      name: 'New Customer Discount',
      amount: 20,
    },
    {
      name: '$10 Off Coupon',
      amount: 10,
    },
  ],
});
```

#### sendAirlineBoardingPassTemplate(userId, attributes) - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/airline-boardingpass-template)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/13466921_1408414619175015_4955822_n.png?oh=3136f1ef03e482bda03f433b18745033&oe=5A316E63" alt="sendAirlineBoardingPassTemplate" width="600" />

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### attributes

Type: `Object`

```js
client.sendAirlineBoardingPassTemplate(RECIPIENT_ID, {
  intro_message: 'You are checked in.',
  locale: 'en_US',
  boarding_pass: [
    {
      passenger_name: 'SMITH/NICOLAS',
      pnr_number: 'CG4X7U',
      travel_class: 'business',
      seat: '74J',
      auxiliary_fields: [
        {
          label: 'Terminal',
          value: 'T1',
        },
        {
          label: 'Departure',
          value: '30OCT 19:05',
        },
      ],
      secondary_fields: [
        {
          label: 'Boarding',
          value: '18:30',
        },
        {
          label: 'Gate',
          value: 'D57',
        },
        {
          label: 'Seat',
          value: '74J',
        },
        {
          label: 'Sec.Nr.',
          value: '003',
        },
      ],
      logo_image_url: 'https://www.example.com/en/logo.png',
      header_image_url: 'https://www.example.com/en/fb/header.png',
      qr_code: 'M1SMITH/NICOLAS  CG4X7U nawouehgawgnapwi3jfa0wfh',
      above_bar_code_image_url: 'https://www.example.com/en/PLAT.png',
      flight_info: {
        flight_number: 'KL0642',
        departure_airport: {
          airport_code: 'JFK',
          city: 'New York',
          terminal: 'T1',
          gate: 'D57',
        },
        arrival_airport: {
          airport_code: 'AMS',
          city: 'Amsterdam',
        },
        flight_schedule: {
          departure_time: '2016-01-02T19:05',
          arrival_time: '2016-01-05T17:30',
        },
      },
    },
    {
      passenger_name: 'JONES/FARBOUND',
      pnr_number: 'CG4X7U',
      travel_class: 'business',
      seat: '74K',
      auxiliary_fields: [
        {
          label: 'Terminal',
          value: 'T1',
        },
        {
          label: 'Departure',
          value: '30OCT 19:05',
        },
      ],
      secondary_fields: [
        {
          label: 'Boarding',
          value: '18:30',
        },
        {
          label: 'Gate',
          value: 'D57',
        },
        {
          label: 'Seat',
          value: '74K',
        },
        {
          label: 'Sec.Nr.',
          value: '004',
        },
      ],
      logo_image_url: 'https://www.example.com/en/logo.png',
      header_image_url: 'https://www.example.com/en/fb/header.png',
      qr_code: 'M1JONES/FARBOUND  CG4X7U nawouehgawgnapwi3jfa0wfh',
      above_bar_code_image_url: 'https://www.example.com/en/PLAT.png',
      flight_info: {
        flight_number: 'KL0642',
        departure_airport: {
          airport_code: 'JFK',
          city: 'New York',
          terminal: 'T1',
          gate: 'D57',
        },
        arrival_airport: {
          airport_code: 'AMS',
          city: 'Amsterdam',
        },
        flight_schedule: {
          departure_time: '2016-01-02T19:05',
          arrival_time: '2016-01-05T17:30',
        },
      },
    },
  ],
});
```

#### sendAirlineCheckinTemplate(userId, attributes) - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/airline-checkin-template)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/13466944_1156144061116360_549622536_n.png?oh=1aa077176a59f346abf8d199e133d2d2&oe=59F2476C" alt="sendAirlineCheckinTemplate" width="250" />

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### attributes

Type: `Object`

```js
client.sendAirlineCheckinTemplate(USER_ID, {
  intro_message: 'Check-in is available now.',
  locale: 'en_US',
  pnr_number: 'ABCDEF',
  flight_info: [
    {
      flight_number: 'f001',
      departure_airport: {
        airport_code: 'SFO',
        city: 'San Francisco',
        terminal: 'T4',
        gate: 'G8',
      },
      arrival_airport: {
        airport_code: 'SEA',
        city: 'Seattle',
        terminal: 'T4',
        gate: 'G8',
      },
      flight_schedule: {
        boarding_time: '2016-01-05T15:05',
        departure_time: '2016-01-05T15:45',
        arrival_time: '2016-01-05T17:30',
      },
    },
  ],
  checkin_url: 'https://www.airline.com/check-in',
});
```

#### sendAirlineItineraryTemplate(userId, attributes) - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/airline-itinerary-template)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/13466573_979516348832909_515976570_n.png?oh=1eb97bf63d3a9f5c333ba28184085950&oe=59FB8738" alt="sendAirlineItineraryTemplate" width="600" />

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### attributes

Type: `Object`

```js
client.sendAirlineItineraryTemplate(USER_ID, {
  intro_message: "Here's your flight itinerary.",
  locale: 'en_US',
  pnr_number: 'ABCDEF',
  passenger_info: [
    {
      name: 'Farbound Smith Jr',
      ticket_number: '0741234567890',
      passenger_id: 'p001',
    },
    {
      name: 'Nick Jones',
      ticket_number: '0741234567891',
      passenger_id: 'p002',
    },
  ],
  flight_info: [
    {
      connection_id: 'c001',
      segment_id: 's001',
      flight_number: 'KL9123',
      aircraft_type: 'Boeing 737',
      departure_airport: {
        airport_code: 'SFO',
        city: 'San Francisco',
        terminal: 'T4',
        gate: 'G8',
      },
      arrival_airport: {
        airport_code: 'SLC',
        city: 'Salt Lake City',
        terminal: 'T4',
        gate: 'G8',
      },
      flight_schedule: {
        departure_time: '2016-01-02T19:45',
        arrival_time: '2016-01-02T21:20',
      },
      travel_class: 'business',
    },
    {
      connection_id: 'c002',
      segment_id: 's002',
      flight_number: 'KL321',
      aircraft_type: 'Boeing 747-200',
      travel_class: 'business',
      departure_airport: {
        airport_code: 'SLC',
        city: 'Salt Lake City',
        terminal: 'T1',
        gate: 'G33',
      },
      arrival_airport: {
        airport_code: 'AMS',
        city: 'Amsterdam',
        terminal: 'T1',
        gate: 'G33',
      },
      flight_schedule: {
        departure_time: '2016-01-02T22:45',
        arrival_time: '2016-01-03T17:20',
      },
    },
  ],
  passenger_segment_info: [
    {
      segment_id: 's001',
      passenger_id: 'p001',
      seat: '12A',
      seat_type: 'Business',
    },
    {
      segment_id: 's001',
      passenger_id: 'p002',
      seat: '12B',
      seat_type: 'Business',
    },
    {
      segment_id: 's002',
      passenger_id: 'p001',
      seat: '73A',
      seat_type: 'World Business',
      product_info: [
        {
          title: 'Lounge',
          value: 'Complimentary lounge access',
        },
        {
          title: 'Baggage',
          value: '1 extra bag 50lbs',
        },
      ],
    },
    {
      segment_id: 's002',
      passenger_id: 'p002',
      seat: '73B',
      seat_type: 'World Business',
      product_info: [
        {
          title: 'Lounge',
          value: 'Complimentary lounge access',
        },
        {
          title: 'Baggage',
          value: '1 extra bag 50lbs',
        },
      ],
    },
  ],
  price_info: [
    {
      title: 'Fuel surcharge',
      amount: '1597',
      currency: 'USD',
    },
  ],
  base_price: '12206',
  tax: '200',
  total_price: '14003',
  currency: 'USD',
});
```

#### sendAirlineFlightUpdateTemplate(userId, attributes) - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/airline-update-template)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/13503467_502166346641834_1768260104_n.png?oh=141fe3238aa6f04d413705860eb52ede&oe=59F5C6BC" alt="sendAirlineFlightUpdateTemplate" width="250" />

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### attributes

Type: `Object`

```js
client.sendAirlineFlightUpdateTemplate(USER_ID, {
  intro_message: 'Your flight is delayed',
  update_type: 'delay',
  locale: 'en_US',
  pnr_number: 'CF23G2',
  update_flight_info: {
    flight_number: 'KL123',
    departure_airport: {
      airport_code: 'SFO',
      city: 'San Francisco',
      terminal: 'T4',
      gate: 'G8',
    },
    arrival_airport: {
      airport_code: 'AMS',
      city: 'Amsterdam',
      terminal: 'T4',
      gate: 'G8',
    },
    flight_schedule: {
      boarding_time: '2015-12-26T10:30',
      departure_time: '2015-12-26T11:30',
      arrival_time: '2015-12-27T07:30',
    },
  },
});
```

<a id="quick-replies" />

### Quick Replies - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/quick-replies)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/14175277_1582251242076612_248078259_n.png?oh=f87f9d3ea0f9902686f21a105e6fe9eb&oe=59F265D6" alt="Sender Actions" width="750" />

#### sendQuickReplies(userId, message, items)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### message

Type: `Object`

###### items

Type: `Array<Object>`

```js
client.sendQuickReplies(USER_ID, { text: 'Pick a color:' }, [
  {
    content_type: 'text',
    title: 'Red',
    payload: 'DEVELOPER_DEFINED_PAYLOAD_FOR_PICKING_RED',
  },
]);
```

<a id="sender-actions" />

### Sender Actions - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/sender-actions)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/13480169_570751053131489_689799179_n.png?oh=e0a04cc8a7bdc05b39f9fd4262a6be04&oe=59F7E61C" alt="Sender Actions" width="250" />

#### sendSenderAction(userId, action)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

###### action

Type: `String`

Name of the action.

```js
client.sendSenderAction(USER_ID, 'typing_on');
```

#### turnTypingIndicatorsOn(userId)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

```js
client.turnTypingIndicatorsOn(USER_ID);
```

#### turnTypingIndicatorsOff(userId)

###### userId

Type: `String | Object`

Page-scoped user ID of the recipient or [recipient](https://developers.facebook.com/docs/messenger-platform/send-api-reference#recipient) object.

```js
client.turnTypingIndicatorsOff(USER_ID);
```

<a id="attachment-upload-api" />

### Attachment Upload API - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/attachment-upload)

#### uploadAttachment(type, url)

###### type

Type: `String`

###### url

Type: `String`

URL address of the attachment.

```js
client.uploadAttachment('image', 'http://www.example.com/image.jpg');
```

#### uploadAudio(url)

###### url

Type: `String`

URL address of the audio.

```js
client.uploadAudio('http://www.example.com/audio.mp3');
```

#### uploadImage(url)

###### url

Type: `String`

URL address of the image.

```js
client.uploadImage('http://www.example.com/image.jpg');
```

#### uploadVideo(url)

###### url

Type: `String`

URL address of the video.

```js
client.uploadVideo('http://www.example.com/video.mp4');
```

#### uploadFile(url)

###### url

Type: `String`

URL address of the file.

```js
client.uploadFile('http://www.example.com/file.pdf');
```
<a id="tags" />

### Tags - [Official Docs](https://developers.facebook.com/docs/messenger-platform/send-api-reference/tags/)

#### getMessageTags

```js
client.getMessageTags().then(tags => {
  console.log(tags);
  // [
  //   {
  //     tag: 'SHIPPING_UPDATE',
  //     description:
  //       'The shipping_update tag may only be used to provide a shipping status notification for a product that has already been purchased. For example, when the product is shipped, in-transit, delivered, or delayed. This tag cannot be used for use cases beyond those listed above or for promotional content (ex: daily deals, coupons and discounts, or sale announcements).',
  //   },
  //   {
  //     tag: 'RESERVATION_UPDATE',
  //     description:
  //       'The reservation_update tag may only be used to confirm updates to an existing reservation. For example, when there is a change in itinerary, location, or a cancellation (such as when a hotel booking is canceled, a car rental pick-up time changes, or a room upgrade is confirmed). This tag cannot be used for use cases beyond those listed above or for promotional content (ex: daily deals, coupons and discounts, or sale announcements).',
  //   },
  //   {
  //     tag: 'ISSUE_RESOLUTION',
  //     description:
  //       'The issue_resolution tag may only be used to respond to a customer service issue surfaced in a Messenger conversation after a transaction has taken place. This tag is intended for use cases where the business requires more than 24 hours to resolve an issue and needs to give someone a status update and/or gather additional information. This tag cannot be used for use cases beyond those listed above or for promotional content (ex: daily deals, coupons and discounts, or sale announcements, nor can businesses use the tag to proactively message people to solicit feedback).',
  //   },
  //   {
  //     tag: 'APPOINTMENT_UPDATE',
  //     description:
  //       'The appointment_update tag may only be used to provide updates about an existing appointment. For example, when there is a change in time, a location update or a cancellation (such as when a spa treatment is canceled, a real estate agent needs to meet you at a new location or a dental office proposes a new appointment time). This tag cannot be used for use cases beyond those listed above or for promotional content (ex: daily deals, coupons and discounts, or sale announcements).',
  //   },
  //   {
  //     tag: 'GAME_EVENT',
  //     description:
  //       'The game_event tag may only be used to provide an update on user progression, a global event in a game or a live sporting event. For example, when a person’s crops are ready to be collected, their building is finished, their daily tournament is about to start or their favorite soccer team is about to play. This tag cannot be used for use cases beyond those listed above or for promotional content (ex: daily deals, coupons and discounts, or sale announcements).',
  //   },
  //   {
  //     tag: 'TRANSPORTATION_UPDATE',
  //     description:
  //       'The transportation_update tag may only be used to confirm updates to an existing reservation. For example, when there is a change in status of any flight, train or ferry reservation (such as “ride canceled”, “trip started” or “ferry arrived”). This tag cannot be used for use cases beyond those listed above or for promotional content (ex: daily deals, coupons and discounts, or sale announcements).',
  //   },
  //   {
  //     tag: 'FEATURE_FUNCTIONALITY_UPDATE',
  //     description:
  //       'The feature_functionality_update tag may only be used to provide an update on new features or functionality that become available in a bot. For example, announcing the ability to talk to a live agent in a bot, or that the bot has a new skill. This tag cannot be used for use cases beyond those listed above or for promotional content (ex: daily deals, coupons and discounts, or sale announcements).',
  //   },
  //   {
  //     tag: 'TICKET_UPDATE',
  //     description:
  //       'The ticket_update tag may only be used to provide updates pertaining to an event for which a person already has a ticket. For example, when there is a change in time, a location update or a cancellation (such as when a concert is canceled, the venue has changed or a refund opportunity is available). This tag cannot be used for use cases beyond those listed above or for promotional content (ex: daily deals, coupons and discounts, or sale announcements).',
  //   },
  // ]
});
```

<a id="user-profile-api" />

### User Profile API - [Official Docs](https://developers.facebook.com/docs/messenger-platform/user-profile)

#### getUserProfile(userId)

###### userId

Type: `String`

Page-scoped user ID of the recipient.

```js
client.getUserProfile(USER_ID).then(user => {
  console.log(user);
  // {
  //   first_name: 'Johnathan',
  //   last_name: 'Jackson',
  //   profile_pic: 'https://example.com/pic.png',
  //   locale: 'en_US',
  //   timezone: 8,
  //   gender: 'male',
  // }
});
```

<a id="messenger-profile-api" />

### Messenger Profile API - [Official Docs](https://developers.facebook.com/docs/messenger-platform/messenger-profile)

#### getMessengerProfile(fields)

###### fields

Type: `Array<String>`

```js
client.getMessengerProfile(['get_started', 'persistent_menu']).then(profile => {
  console.log(profile);
  // [
  //   {
  //     get_started: {
  //       payload: 'GET_STARTED',
  //     },
  //   },
  //   {
  //     persistent_menu: [
  //       {
  //         locale: 'default',
  //         composer_input_disabled: true,
  //         call_to_actions: [
  //           {
  //             type: 'postback',
  //             title: 'Restart Conversation',
  //             payload: 'RESTART',
  //           },
  //         ],
  //       },
  //     ],
  //   },
  // ]
});
```

#### setMessengerProfile(profile)

###### profile

Type: `Object`

```js
client.setMessengerProfile({
  get_started: {
    payload: 'GET_STARTED',
  },
  persistent_menu: [
    {
      locale: 'default',
      composer_input_disabled: true,
      call_to_actions: [
        {
          type: 'postback',
          title: 'Restart Conversation',
          payload: 'RESTART',
        },
      ],
    },
  ],
});
```

#### deleteMessengerProfile(fields)

###### fields

Type: `Array<String>`

```js
client.deleteMessengerProfile(['get_started', 'persistent_menu']);
```

<a id="persistent-menu" />

### Persistent Menu - [Official Docs](https://developers.facebook.com/docs/messenger-platform/messenger-profile/persistent-menu)

![](https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/16686128_804279846389859_443648268883197952_n.png?oh=adde03b0bc7dd524a58cf46016e0267d&oe=59FC90D6)

#### getPersistentMenu

```js
client.getPersistentMenu().then(menu => {
  console.log(menu);
  // [
  //   {
  //     locale: 'default',
  //     composer_input_disabled: true,
  //     call_to_actions: [
  //       {
  //         type: 'postback',
  //         title: 'Restart Conversation',
  //         payload: 'RESTART',
  //       },
  //       {
  //         type: 'web_url',
  //         title: 'Powered by ALOHA.AI, Yoctol',
  //         url: 'https://www.yoctol.com/',
  //       },
  //     ],
  //   },
  // ]
});
```

#### setPersistentMenu(menu)

###### menu

Type: `Array<Object>`

```js
client.setPersistentMenu([
  {
    locale: 'default',
    call_to_actions: [
      {
        title: 'Play Again',
        type: 'postback',
        payload: 'RESTART',
      },
      {
        title: 'Language Setting',
        type: 'nested',
        call_to_actions: [
          {
            title: '中文',
            type: 'postback',
            payload: 'CHINESE',
          },
          {
            title: 'English',
            type: 'postback',
            payload: 'ENGLISH',
          },
        ],
      },
      {
        title: 'Explore D',
        type: 'nested',
        call_to_actions: [
          {
            title: 'Explore',
            type: 'web_url',
            url: 'https://www.youtube.com/watch?v=v',
            webview_height_ratio: 'tall',
          },
          {
            title: 'W',
            type: 'web_url',
            url: 'https://www.facebook.com/w',
            webview_height_ratio: 'tall',
          },
          {
            title: 'Powered by YOCTOL',
            type: 'web_url',
            url: 'https://www.yoctol.com/',
            webview_height_ratio: 'tall',
          },
        ],
      },
    ],
  },
]);
```

#### deletePersistentMenu

```js
client.deletePersistentMenu();
```

<a id="get-started-button" />

### Get Started Button - [Official Docs](https://developers.facebook.com/docs/messenger-platform/messenger-profile/get-started-button)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/14302685_243106819419381_1314180151_n.png?oh=9487042d8c0067eb2fda1efa45d0e17b&oe=59F7185C" alt="Get Started Button" width="500" />

#### getGetStartedButton

```js
client.getGetStartedButton().then(getStarted => {
  console.log(getStarted);
  // {
  //   payload: 'GET_STARTED',
  // }
});
```

#### setGetStartedButton(payload)

###### payload

Type: `String`

```js
client.setGetStartedButton('GET_STARTED');
```

#### deleteGetStartedButton

```js
client.deleteGetStartedButton();
```

<a id="greeting-text" />

### Greeting Text - [Officail docs](https://developers.facebook.com/docs/messenger-platform/messenger-profile/greeting-text)

<img src="https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/14287888_188235318253964_1078929636_n.png?oh=a1171ab50f04d3a244ed703eafd2dbef&oe=59F01AF5" alt="Greeting Text" width="250" />

#### getGreetingText

```js
client.getGreetingText().then(greeting => {
  console.log(greeting);
  // [
  //   {
  //     locale: 'default',
  //     text: 'Hello!',
  //   },
  // ]
});
```

#### setGreetingText(greeting)

###### greeting

Type: `Array<Object>`

```js
client.setGreetingText([
  {
    locale: 'default',
    text: 'Hello!',
  },
]);
```

#### deleteGreetingText

```js
client.deleteGreetingText();
```

<a id="domain-whitelist" />

### Domain Whitelist - [Official Docs](https://developers.facebook.com/docs/messenger-platform/messenger-profile/domain-whitelisting)

#### getDomainWhitelist

```js
client.getDomainWhitelist().then(domains => {
  console.log(domains);
  // ['http://www.example.com/']
});
```

#### setDomainWhitelist(domains)

###### domains

Type: `Array<String>`

```js
client.setDomainWhitelist(['www.example.com']);
```

#### deleteDomainWhitelist

```js
client.deleteDomainWhitelist();
```

<a id="account-linking-url" />

### Account Linking URL - [Official Docs](https://developers.facebook.com/docs/messenger-platform/messenger-profile/account-linking-url)

#### getAccountLinkingURL

```js
client.getAccountLinkingURL().then(accountLinking => {
  console.log(accountLinking);
  // {
  //   account_linking_url:
  //     'https://www.example.com/oauth?response_type=code&client_id=1234567890&scope=basic',
  // }
});
```

#### setAccountLinkingURL(url)

###### url

Type: `String`

```js
client.setAccountLinkingURL(
  'https://www.example.com/oauth?response_type=code&client_id=1234567890&scope=basic'
);
```

#### deleteAccountLinkingURL

```js
client.deleteAccountLinkingURL();
```

<a id="payment-settings" />

### Payment Settings - [Official Docs](https://developers.facebook.com/docs/messenger-platform/messenger-profile/payment-settings)

#### getPaymentSettings

```js
client.getPaymentSettings().then(settings => {
  console.log(settings);
  // {
  //   privacy_url: 'www.facebook.com',
  //   public_key: 'YOUR_PUBLIC_KEY',
  //   test_users: ['12345678'],
  // }
});
```

#### setPaymentPrivacyPolicyURL(url)

###### url

Type: `String`

```js
client.setPaymentPrivacyPolicyURL('https://www.example.com');
```

#### setPaymentPublicKey(key)

###### key

Type: `String`

```js
client.setPaymentPublicKey('YOUR_PUBLIC_KEY');
```

#### setPaymentTestUsers(users)

###### users

Type: `Array<String>`

```js
client.setPaymentTestUsers(['12345678']);
```

#### deletePaymentSettings

```js
client.deletePaymentSettings();
```

<a id="target-audience" />

### Target Audience - [Official Docs](https://developers.facebook.com/docs/messenger-platform/messenger-profile/target-audience)

#### getTargetAudience

```js
client.getTargetAudience().then(targetAudience => {
  console.log(targetAudience);
  // {
  //   audience_type: 'custom',
  //   countries: {
  //     whitelist: ['US', 'CA'],
  //   },
  // }
});
```

#### setTargetAudience(type, whitelist, blacklist)

###### type

Type: `String`

##### whitelist

Type: `Array<String>`

##### blacklist

Type: `Array<String>`

```js
client.setTargetAudience('custom', ['US', 'CA'], ['UK']);
```

#### deleteTargetAudience

```js
client.deleteTargetAudience();
```

<a id="chat-extension-home-url" />

### Chat Extension Home URL - [Official Docs](https://developers.facebook.com/docs/messenger-platform/messenger-profile/home-url)

#### getChatExtensionHomeURL

```js
client.getChatExtensionHomeURL().then(chatExtension => {
  console.log(chatExtension);
  // {
  //   url: 'http://petershats.com/send-a-hat',
  //   webview_height_ratio: 'tall',
  //   in_test: true,
  // }
});
```

#### setChatExtensionHomeURL(url, attributes)

###### url

Type: `String`

##### attributes

Type: `Object`

```js
client.setChatExtensionHomeURL('http://petershats.com/send-a-hat', {
  webview_height_ratio: 'tall',
  in_test: true,
});
```

#### deleteChatExtensionHomeURL

```js
client.deleteChatExtensionHomeURL();
```

<a id="messenger-code-api" />

### Messenger Code API - [Official Docs](https://developers.facebook.com/docs/messenger-platform/messenger-code)

![](https://scontent-tpe1-1.xx.fbcdn.net/v/t39.2365-6/16685647_261975084241469_2329165888516784128_n.png?oh=61941dc020355f5c8fe88035d33f1503&oe=59F612D6)

#### generateMessengerCode(options)

###### options

Type: `Object`

###### options.image_size

Type: `Number`

###### options.data

Type: `Object`

```js
client
  .generateMessengerCode({
    data: {
      ref: 'billboard-ad',
    },
    image_size: 1000,
  })
  .then(code => {
    console.log(code);
    // {
    //   "uri": "YOUR_CODE_URL_HERE"
    // }
  });
```

### Handover Protocol API

#### passThreadControl(userId, targetAppId, metadata) - [Official Docs](https://developers.facebook.com/docs/messenger-platform/pass-thread-control)

###### userId

Type: `String`

Page-scoped user ID of the recipient.

###### targetAppId

Type: `Number`

###### metadata

Type: `String`

```js
client.passThreadControl(USER_ID, APP_ID, 'free formed text for another app');
```

#### takeThreadControl(userId, metadata) - [Official Docs](https://developers.facebook.com/docs/messenger-platform/take-thread-control)

###### userId

Type: `String`

Page-scoped user ID of the recipient.

###### metadata

Type: `String`

```js
client.passThreadControl(USER_ID, 'free formed text for another app');
```

#### getSecondaryReceivers  - [Official Docs](https://developers.facebook.com/docs/messenger-platform/secondary-receivers)

```js
client.getSecondaryReceivers().then(receivers => {
  console.log(receivers);
  // [
  //   {
  //     "id": "12345678910",
  //     "name": "David's Composer"
  //   },
  //   {
  //     "id": "23456789101",
  //     "name": "Messenger Rocks"
  //   }
  // ]
});
```

<a id="page-messaging-insights-api" />

### Page Messaging Insights API - [Official Docs](https://developers.facebook.com/docs/messenger-platform/insights/page-messaging)

#### getDailyUniqueActiveThreadCounts

```js
client.getDailyUniqueActiveThreadCounts().then(counts => {
  console.log(counts);
  // [
  //   {
  //     "name": "page_messages_active_threads_unique",
  //     "period": "day",
  //     "values": [
  //       {
  //         "value": 83111,
  //         "end_time": "2017-02-02T08:00:00+0000"
  //       },
  //       {
  //         "value": 85215,
  //         "end_time": "2017-02-03T08:00:00+0000"
  //       },
  //       {
  //         "value": 87175,
  //         "end_time": "2017-02-04T08:00:00+0000"
  //       }
  //    ],
  //    "title": "Daily unique active threads count by thread fbid",
  //    "description": "Daily: total unique active threads created between users and page.",
  //    "id": "1234567/insights/page_messages_active_threads_unique/day"
  //   }
  // ]
});
```

#### getDailyUniqueConversationCounts

```js
client.getDailyUniqueConversationCounts().then(counts => {
  console.log(counts);
  // [
  //   {
  //     "name": "page_messages_feedback_by_action_unique",
  //     "period": "day",
  //     "values": [
  //       {
  //         "value": {
  //           "TURN_ON": 40,
  //           "TURN_OFF": 167,
  //           "DELETE": 720,
  //           "OTHER": 0,
  //           "REPORT_SPAM": 0
  //         },
  //         "end_time": "2017-02-02T08:00:00+0000"
  //       },
  //       {
  //         "value": {
  //           "TURN_ON": 38,
  //           "DELETE": 654,
  //           "TURN_OFF": 155,
  //           "REPORT_SPAM": 1,
  //           "OTHER": 0
  //         },
  //         "end_time": "2017-02-03T08:00:00+0000"
  //       }
  //     ],
  //     "title": "Daily unique conversation count broken down by user feedback actions",
  //     "description": "Daily: total unique active threads created between users and page.",
  //     "id": "1234567/insights/page_messages_active_threads_unique/day"
  //   }
  // ],
});
```

<a id="built-in-nlp-api" />

### Built-in NLP API - [Official Docs](https://developers.facebook.com/docs/messenger-platform/built-in-nlp)

#### setNLPConfigs(config)

###### config

Type: `Object`

###### config.nlp_enabled

Type: `Boolean`

###### config.custom_token

Type: `String`

```js
client.setNLPConfigs({
  nlp_enabled: true,
});
```

#### enableNLP

```js
client.enableNLP();
```

#### disableNLP

```js
client.disableNLP();
```
