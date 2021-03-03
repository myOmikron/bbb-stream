# Specification of Chat Bridges' API

## Authentication

See [Random Checksum Protocol](https://github.com/myOmikron/rcp)

## Endpoints

The common parameter `chat_id` is a string and its format depends on the used chat bridge.

- On **BBB** it's the **internal meeting id**
- On **XMPP** it's the **room's jid**

### runningChats

- Method: `GET`

Get a list of all running chats.

### startChat

- Method: `POST`

Parameters      | Required | Type | Description
----------------|----------|------|------------
chat_id         | Yes      | str  | Id of the chat to be started
chat_user       | Only BBB | str  | Name of user to send messages with. The user has to join itself.
callback_uri    | No       | str  | Only required when callbacks should be enabled. Specifies the base uri of another chat bridge to forward messages to.
callback_secret | No       | str  | Only required when callbacks should be enabled. Specifies the shared secret to use for a specific callback uri.
callback_id     | No       | str  | Only required when callbacks should be enabled. Specifies the other chat bridge's chat id

Register a chat and start its listener/ handler.

### sendMessage

- Method: `POST`

Parameters | Required | Type | Description
-----------|----------|------|------------
chat_id    | Yes      | str  | Id of the chat the message should be sent to
message    | Yes      | str  | Message to send
user_name  | Yes      | str  | Username from which the message was sent

Send a user's message to the chat.

### endChat

- Method: `POST`

Parameters | Required | Type | Description
-----------|----------|------|------------
chat_id    | Yes      | str  | Id of the chat to be ended

Stop a chat's listener/ handler and delete it's entry.
