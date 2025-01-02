# Messaging case study

## Functional requirements (MVP)

- get list of conversations
- get messages of conversation with a user
- update account

## Design goals

highly consistent

- the conversation should show messages in order.

highly available

- messages sent to from source user to destination user should be instant received within seconds ( low latency)

the system must be idempotent

## Estiamations

### Assumptions

- facebook messenger generates around 20 Bilion of messages per day

### Calculate storage

a message can be 200 B. so 200 B * 20 Billion = 4 trillion bytes => 4 TB / day

### read-heavy /write heavy

read-heavy & write heavy

## API

sendMessage(destination_id,source_id, content, conversation_id)
getConversation(conversation_id, user_id)
getConversationList(user_id)

## Implementation approaches

### sharding methods

- sharding by user_id is ideal for implementing
  - getConversationList(user_id)
  - getConversation(user_id, conversation_id)

- sharding by conversation_id is ideal for implementing:
  - sendMessage(destination_id,source_id, content, conversation_id)
    - if it were sharded by user_id, then we would have to duplicate the message on both shards.

- when implementing group chats,it'll be ideal to shard by conversation_id

### messahge consistency

- it's ideal to initially insert the message inside the recipient's shard, then get a confirmation , then insert the message in the sender's shard.
- write through caching is necessary as it is write heavy

### the system must be idempotent

- the message must be unique such that the receiving end will know not to save it twice.
  - this happens because sometimes
