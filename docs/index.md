

# Services

### ChannelService
ChannelService exposes endpoints pertaining
to channel management.

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| OpenChannel | OpenChannelRequest | [OpenChannelResponse](#services.OpenChannelResponse) | Opens a channel to a node.<br /><br />Returns immediately after the funding transaction has been published,<br />but does not wait for the channel to be considered open. |


### ContactService
ContactService exposes endpoints pertaining to handling
nodes of the Lightning network and contacts.

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| GetContacts | GetContactsRequest | [GetContactsResponse](#services.GetContactsResponse) | Lists all current contacts.<br /><br />Returns a list of all contacts currently in the database. |
| AddContact | AddContactRequest | [AddContactResponse](#services.AddContactResponse) | Adds a node as a contact.<br /><br />Accepts a node and adds them as a contact in the database. |
| RemoveContactByID | RemoveContactByIDRequest | [RemoveContactResponse](#services.RemoveContactResponse) | Removes a contact.<br /><br />Accepts a contact id and removes it from the database. |
| RemoveContactByAddress | RemoveContactByAddressRequest | [RemoveContactResponse](#services.RemoveContactResponse) | Removes a contact.<br /><br />Accepts a contact address and removes it from the database. |


### DiscussionService
DiscussionService exposes functionality pertaining
to discussion creation, deletion and history.

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| GetDiscussions | GetDiscussionsRequest | [GetDiscussionsResponse](#services.GetDiscussionsResponse) stream | Creates a unidirectional stream from server to client<br />over which all discussions' info are sent.<br /><br />The stream terminates when all discussions' info is transmitted. |
| GetDiscussionHistoryByID | GetDiscussionHistoryByIDRequest | [GetDiscussionHistoryResponse](#services.GetDiscussionHistoryResponse) stream | Creates a unidirectional stream from server to client<br />over which all previously exchanged messages belonging to<br />a specific discussion are sent.<br /><br />The stream terminates when all discussion history is transmitted. |
| GetDiscussionStatistics | GetDiscussionStatisticsRequest | [GetDiscussionStatisticsResponse](#services.GetDiscussionStatisticsResponse) | Calculates statistics about the requested discussion. |
| AddDiscussion | AddDiscussionRequest | [AddDiscussionResponse](#services.AddDiscussionResponse) | Adds a discussion to the database. |
| UpdateDiscussionLastRead | UpdateDiscussionLastReadRequest | [UpdateDiscussionResponse](#services.UpdateDiscussionResponse) | Updates a discussion's last read message. |
| RemoveDiscussion | RemoveDiscussionRequest | [RemoveDiscussionResponse](#services.RemoveDiscussionResponse) | Remove a discussion from the database. |


### MessageService
MessageService exposes functionality pertaining
to message creation and exchange.

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| EstimateMessage | EstimateMessageRequest | [EstimateMessageResponse](#services.EstimateMessageResponse) | Estimates the route and fees for the requested message.<br /><br />In case of failure (payment amount too large or small, payload too large),<br />an empty response is returned. |
| SendMessage | SendMessageRequest | [SendMessageResponse](#services.SendMessageResponse) | Sends a message<br /><br />In case of failure (payment amount too large or small, payload too large),<br />an empty response is returned. |
| SubscribeMessages | SubscribeMessageRequest | [SubscribeMessageResponse](#services.SubscribeMessageResponse) stream | Creates a unidirectional stream from server to client<br />over which all received messages are sent.<br /><br />The stream does not terminate until the client stops it. |


### NodeInfoService
NodeInfoService exposes functionality
pertaining to queries about node information.

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| GetVersion | VersionRequest | [Version](#services.Version) | Returns version information about the current daemon. |
| GetSelfInfo | SelfInfoRequest | [SelfInfoResponse](#services.SelfInfoResponse) | Returns info about the current underlying node. |
| GetSelfBalance | SelfBalanceRequest | [SelfBalanceResponse](#services.SelfBalanceResponse) | Returns the balance of the current underlying node. |
| GetNodes | GetNodesRequest | [NodeInfoResponse](#services.NodeInfoResponse) | Lists all nodes on the Lightning network.<br /><br />Returns a list of all nodes visible to the underlying Lightning node,<br />including the address of the current node.<br />Nodes with private channels are not visible if not directly connected to<br />the underlying node. |
| SearchNodeByAddress | SearchNodeByAddressRequest | [NodeInfoResponse](#services.NodeInfoResponse) | Searches for a Lighting node based on their Lightning address.<br /><br />Returns a list of all nodes with that address, which will be at most 1.<br />The node must be visible from the underlying node. |
| SearchNodeByAlias | SearchNodeByAliasRequest | [NodeInfoResponse](#services.NodeInfoResponse) | Searches for a Lightning node based on their Lightning alias.<br /><br />Returns a list of all nodes with that alias visible from the underlying node. |
| ConnectNode | ConnectNodeRequest | [ConnectNodeResponse](#services.ConnectNodeResponse) | Connects a node as a peer. |


# Messages

### AddContactRequest

Corresponds to a request to add a node as a contact.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| contact | [ContactInfo](#services.ContactInfo) |  | The node to add as a contact. |




### AddContactResponse

A AddContactResponse is received in response to an AddContact rpc call.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| contact | [ContactInfo](#services.ContactInfo) |  | The newly added contact's information. |




### AddDiscussionRequest

Corresponds to a request to add a discussion to database.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| discussion | [DiscussionInfo](#services.DiscussionInfo) |  |  |




### AddDiscussionResponse

An AddDiscussionResponse is received in response to an AddDiscussion rpc call.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| discussion | [DiscussionInfo](#services.DiscussionInfo) |  |  |




### Chain

Represents a blockchain and network for a Lightning node.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| chain | [string](#string) |  | The blockchain in use. |
| network | [string](#string) |  | The network a node is operating on. |




### ConnectNodeRequest

Corresponds to a request to create a peer connection with a node.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| address | [string](#string) |  | The address of the node to connect. |
| hostport | [string](#string) |  | The network location of the node. |




### ConnectNodeResponse

A ConnectNodeResponse is received in response to a ConnectNode request.



### ContactInfo

A message representing a contact of the application.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| node | [NodeInfo](#services.NodeInfo) |  | The node corresponding to the contact. |
| id | [uint64](#uint64) |  | The contact id. |
| display_name | [string](#string) |  | A contact's chat nickname. |




### DiscussionInfo

Represents the information for a specific discussion.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| id | [uint64](#uint64) |  | The discussion id. |
| participants | [string](#string) | repeated | The list of participants in the discussion. |
| options | [DiscussionOptions](#services.DiscussionOptions) |  |  |
| last_read_msg_id | [uint64](#uint64) |  | The id of the last read message in the discussion. |
| last_msg_id | [uint64](#uint64) |  | The id of the last discussion message. |




### DiscussionOptions

DiscussionOptions represents the per-discussion options.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| fee_limit_msat | [int64](#int64) |  | The maximum fee allowed for sending a message (in millisatoshi).<br /><br />If not set, the default fee limit, as defined in the app package, is used. |
| anonymous | [bool](#bool) |  | Whether to send as anonymous on this discussion. |




### EstimateMessageRequest

Corresponds to a request to estimate a message.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| discussion_id | [uint64](#uint64) |  | The discussion id where the message is to be sent. |
| payload | [string](#string) |  | The message payload (as a string). |
| amt_msat | [int64](#int64) |  | The intended payment amount to the recipient of the message (in millisatoshi). |
| options | [MessageOptions](#services.MessageOptions) |  | The message option overrides for the current message. |




### EstimateMessageResponse

A EstimateMessageResponse is received in response to a EstimateMessage rpc call.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| success_prob | [double](#double) |  | The probability of successful arrival of the message,<br />as reported by the Lightning daemon's mission control. |
| message | [Message](#services.Message) |  | Contains the estimated route and fees for the requested message. |




### GetContactsRequest

Corresponds to a request to list all contacts.



### GetContactsResponse

A GetContactsResponse is received in response to a GetContacts rpc call.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| contacts | [ContactInfo](#services.ContactInfo) | repeated | The list of contacts in the database. |




### GetDiscussionHistoryByIDRequest

Corresponds to a request to create a stream over which to receive
previously exchanged messages of the identified discussion.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| id | [uint64](#uint64) |  | The discussion id of interest. |
| page_options | [KeySetPageOptions](#services.KeySetPageOptions) |  |  |




### GetDiscussionHistoryResponse

A GetDiscussionHistoryResponse is received in response to
a GetHistory rpc call, and represents an exchanged message.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| message | [Message](#services.Message) |  | The exchanged message. |




### GetDiscussionStatisticsRequest

Corresponds to a request for statistics about the requested
discussion, identified by its id.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| id | [uint64](#uint64) |  | The discussion id. |




### GetDiscussionStatisticsResponse

A GetDiscussionStatisticsResponse is received in response to
a GetDiscussionStatistics rpc call.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| amt_msat_sent | [uint64](#uint64) |  | The total amount sent in the discussion (in millisatoshi). |
| amt_msat_received | [uint64](#uint64) |  | The total amount received in the discussion (in millisatoshi). |
| amt_msat_fees | [uint64](#uint64) |  | The total amount of fees for sent messages in the discussion (in millisatoshi). |
| messages_sent | [uint64](#uint64) |  | The total amount of sent messages in the discussion. |
| messages_received | [uint64](#uint64) |  | The total amount of received messages in the discussion. |




### GetDiscussionsRequest

Corresponds to a request to receive all discussion info.



### GetDiscussionsResponse

A GetDiscussionsResponse is received in the stream returned in response
to a GetDiscussions rpc call, and represents a discussion.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| discussion | [DiscussionInfo](#services.DiscussionInfo) |  |  |




### GetNodesRequest

Corresponds to a request to list all nodes on the Lightning Network.



### KeySetPageOptions

Corresponds to pagination parameters for requests.
Represents a request for page_size elements,
terminating with the element with id last_id.
If reverse is true, the returned elements end with last_id.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| last_id | [uint64](#uint64) |  | The id of the first element of the requested range. |
| page_size | [int64](#int64) |  | The number of elements to return. |
| reverse | [bool](#bool) |  | Whether the range starts or ends with last_id element. |




### Message

A message representing a message of the application.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| id | [uint64](#uint64) |  | The unique id of the message. |
| discussion_id | [uint64](#uint64) |  | The discussion id this message is associated with. |
| sender | [string](#string) |  | The Lightning address of the sender node. |
| receiver | [string](#string) |  | The Lightning address of the receiver node. |
| sender_verified | [bool](#bool) |  | Whether the message sender was verified. |
| payload | [string](#string) |  | The message payload. |
| amt_msat | [int64](#int64) |  | The amount paid over this message (in millisatoshi). |
| total_fees_msat | [int64](#int64) |  | The total routing fees paid for this message across all routes (in millisatoshi).<br /><br />This field is meaningful only for sent and estimated messages. |
| sent_timestamp | [google.protobuf.Timestamp](#google.protobuf.Timestamp) |  | The time the message was sent. |
| received_timestamp | [google.protobuf.Timestamp](#google.protobuf.Timestamp) |  | The time the message was received. |
| payment_routes | [PaymentRoute](#services.PaymentRoute) | repeated | The routes that fulfilled this message.<br /><br />This field is meaningful only for sent and estimated messages. |
| preimage | [string](#string) |  | The preimage belonging to the associated payment.<br /><br />This field is only meaningful for received messages and<br />messages sent successfully to non-group discussions. |
| pay_req | [string](#string) |  | The payment request this message was paid to.<br /><br />If empty, corresponds to a spontaneous payment. |




### MessageOptions

MessageOptions represents messaging options.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| fee_limit_msat | [int64](#int64) |  | The maximum fee allowed for a message (in millisatoshi). |
| anonymous | [bool](#bool) |  | Whether to include the sender address when sending a message. |




### NodeInfo

A message representing a node on the Lightning network.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| alias | [string](#string) |  | A node's Lightning alias. |
| address | [string](#string) |  | A node's Lightning address. |




### NodeInfoResponse

A NodeInfoResponse is received in response to a node query.

It contains all visible nodes corresponding to the query.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| nodes | [NodeInfo](#services.NodeInfo) | repeated | The list of Lightning nodes matching the query. |




### OpenChannelRequest

Corresponds to a request to open a channel.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| address | [string](#string) |  | The address of the node to open a channel to. |
| amt_msat | [uint64](#uint64) |  | The total amount to be committed to the channel (in millisatoshi). |
| push_amt_msat | [uint64](#uint64) |  | The amount to be sent to the other party (in millisatoshi). |
| min_input_confs | [int32](#int32) |  | The minimum number of confirmations each input<br />of the channel funding transaction must have.<br /><br />In case of a negative value being provided, unconfirmed funds can be used. |
| target_confirmation_block | [uint32](#uint32) |  | The number of blocks the funding transaction should confirm by.<br />This is used for fee estimation. |
| sat_per_vbyte | [uint64](#uint64) |  | The fee rate (satoshis per virtual byte) the funding transaction should cost. |




### OpenChannelResponse

An OpenChannelResponse is received in response to an OpenChannel call.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| funding_txid | [string](#string) |  | The channel funding transaction. |
| output_index | [uint32](#uint32) |  | The output index of the funding transaction. |




### PageOptions

Corresponds to pagination parameters for requests.
Represents a request for page_size elements,
skipping the most recent skip_recent elements (reverse order).


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| skip_recent | [int64](#int64) |  | The number of most recent elements to skip. |
| page_size | [int64](#int64) |  | The number of elements to return. |




### PaymentHop

A message representing a hop of the route for sending a message.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| chan_id | [uint64](#uint64) |  | The channel id. |
| hop_address | [string](#string) |  | The address of the hop node. |
| amt_to_forward_msat | [int64](#int64) |  | The amount to be forwarded by the hop (in millisatoshi). |
| fee_msat | [int64](#int64) |  | The fee to be paid to the hop for forwarding the message (in millisatoshi). |




### PaymentRoute

A message representing a route fulfilling a payment HTLC.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| hops | [PaymentHop](#services.PaymentHop) | repeated | The list of hops for this route. |
| total_timelock | [uint32](#uint32) |  | The total timelock of the route. |
| route_amt_msat | [int64](#int64) |  | The amount sent via this route, disregarding the route fees (in millisatoshi). |
| route_fees_msat | [int64](#int64) |  | The fees paid for this route (in millisatoshi). |




### RemoveContactByAddressRequest

Corresponds to a request to remove a contact.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| address | [string](#string) |  | The Lightning address of the contact to remove. |




### RemoveContactByIDRequest

Corresponds to a request to remove a contact.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| id | [uint64](#uint64) |  | The id of the contact to remove. |




### RemoveContactResponse

A RemoveContactResponse is received in response to a RemoveContactBy* rpc call.



### RemoveDiscussionRequest

Corresponds to a request to remove a discussion.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| id | [uint64](#uint64) |  | The id of the discussion to remove. |




### RemoveDiscussionResponse

A RemoveDiscussionResponse is received in response to a RemoveDiscussion rpc call.



### SearchNodeByAddressRequest

Corresponds to a node query based on the node address.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| address | [string](#string) |  | The node address to search. |




### SearchNodeByAliasRequest

Corresponds to a node query based on the node alias.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| alias | [string](#string) |  | The node alias substring to search. |




### SelfBalanceRequest

Corresponds to a query to retrieve the balance of the underlying lightning node.



### SelfBalanceResponse

A SelfBalanceResponse is received in response to a GetSelfBalance rpc call.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| wallet_confirmed_sat | [int64](#int64) |  | The confirmed balance of the node's wallet (in satoshi). |
| wallet_unconfirmed_sat | [int64](#int64) |  | The unconfirmed balance of the node's wallet (in satoshi). |
| channel_local_msat | [uint64](#uint64) |  | The local balance available across all open channels (in millisatoshi). |
| channel_remote_msat | [uint64](#uint64) |  | The remote balance available across all open channels (in millisatoshi). |
| pending_open_local_msat | [uint64](#uint64) |  | The local balance in pending open channels (in millisatoshi). |
| pending_open_remote_msat | [uint64](#uint64) |  | The remote balance in pending open channels (in millisatoshi). |
| unsettled_local_msat | [uint64](#uint64) |  | The local balance unsettled across all open channels (in millisatoshi). |
| unsettled_remote_msat | [uint64](#uint64) |  | The remote balance unsettled across all open channels (in millisatoshi). |




### SelfInfoRequest

Correponds to a query to retrieve the information of the underlying lightning node.



### SelfInfoResponse

A SelfInfoResponse is received in response to a GetSelfInfo rpc call.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| info | [NodeInfo](#services.NodeInfo) |  | General node information about the current node. |
| chains | [Chain](#services.Chain) | repeated | A list of chain networks the node is operating on. |




### SendMessageRequest

Corresponds to a request to send a message.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| discussion_id | [uint64](#uint64) |  | The discussion id where the message is to be sent. |
| payload | [string](#string) |  | The message payload (as a string). |
| amt_msat | [int64](#int64) |  | The intended payment amount to the recipient of the message (in millisatoshi). |
| pay_req | [string](#string) |  | A payment request (invoice) to pay to.<br /><br />If empty, a spontaneous message is sent.<br />If specified, discussion_id is not used and should not be specified.<br />Instead, the message will be sent to the discussion associated with<br />the recipient specified by the the payment request (which will be<br />created if it does not exist).<br />The discussion_id will be returned in the response. |
| options | [MessageOptions](#services.MessageOptions) |  | The message option overrides for the current message. |




### SendMessageResponse

A SendMessageResponse is received in response to a SendMessage rpc call.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| sent_message | [Message](#services.Message) |  | The sent message. |




### SubscribeMessageRequest

Corresponds to a request to create a stream
over which to be notified of received messages.



### SubscribeMessageResponse

A SubscribeMessageResponse is received in the stream returned in response to
a SubscribeMessages rpc call, and represents a received message.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| received_message | [Message](#services.Message) |  | The received message. |




### UpdateDiscussionLastReadRequest

Represents a request to update the last read discussion message.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| discussion_id | [uint64](#uint64) |  | The discussion id. |
| last_read_msg_id | [uint64](#uint64) |  | The message id to mark as the last read. |




### UpdateDiscussionResponse

An UpdateDiscussionResponse is returned in reponse
to an UpdateDiscussionLastRead request.



### Version

A message containing the current c13n version and build information.


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| version | [string](#string) |  | The semantic version of c13n. |
| commit | [string](#string) |  | The commit descriptor of the build. |
| commit_hash | [string](#string) |  | The commit hash of the build. |




### VersionRequest




 <!-- end Messages -->

# Scalar Value Types
| .proto Type | Notes | C++ | Java | Python | Go | C# | PHP | Ruby |
| ----------- | ----- | --- | ---- | ------ | -- | -- | --- | ---- |
| <a name="double" /> double |  | double | double | float | float64 | double | float | Float |
| <a name="float" /> float |  | float | float | float | float32 | float | float | Float |
| <a name="int32" /> int32 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint32 instead. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="int64" /> int64 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint64 instead. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="uint32" /> uint32 | Uses variable-length encoding. | uint32 | int | int/long | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="uint64" /> uint64 | Uses variable-length encoding. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum or Fixnum (as required) |
| <a name="sint32" /> sint32 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int32s. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sint64" /> sint64 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int64s. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="fixed32" /> fixed32 | Always four bytes. More efficient than uint32 if values are often greater than 2^28. | uint32 | int | int | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="fixed64" /> fixed64 | Always eight bytes. More efficient than uint64 if values are often greater than 2^56. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum |
| <a name="sfixed32" /> sfixed32 | Always four bytes. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sfixed64" /> sfixed64 | Always eight bytes. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="bool" /> bool |  | bool | boolean | boolean | bool | bool | boolean | TrueClass/FalseClass |
| <a name="string" /> string | A string must always contain UTF-8 encoded or 7-bit ASCII text. | string | String | str/unicode | string | string | string | String (UTF-8) |
| <a name="bytes" /> bytes | May contain any arbitrary sequence of bytes. | string | ByteString | str | []byte | ByteString | string | String (ASCII-8BIT) |

