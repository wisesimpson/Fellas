fellows
=======
<pre><code>
/*
ENUMS

AppId:
id:10	"Fellows"

Operations :
id:1	"SEND_MESSAGE"
id:2	"READ_RECEIPT"
id:3	"INVITE"
id:4	"GET_USER_INFO"


*/

//------------Send Message
//**request
{
	appid:AppId,
	opuid:client_generate_unique_in_current_client,
	op:OP.SEND_MESSAGE,
	to:[userids],
	content:"Message Content",
	settings:{
		backup:0|1,
		require_read_back:0|1
	}
}
//** respond
{
	opuid:client_generate_unique_in_current_client,
	sended:1|0
}
//** server to client(s)
{
	op:OP.SEND_MESSAGE,
	to:[userids],
	messageID:messageID(server_generate_message_id_unique_in_global),
	content:"Message Content",
	settings:{
		backup:0|1,
		require_read_back:0|1
	}
}


//-------------Send Read Receipt
//**request
{
	appid:AppId,
	op:OP.READ_RECEIPT,
	to:[userids],
	messageID:messageID
}
//** server to client(s)
{
	op:OP.READ_RECEIPT,
	to:[userids],
	messageID:messageID
}


//-------------Get User Info
//**request
{
	appid:AppId,
	opuid:client_generate_unique_in_current_client,
	op:OP.GET_USER_INFO,
	userids:[userids]
}
//** respond
{
	opuid:client_generate_unique_in_current_client,
	userinfo:[
		{
			name:'Yulin Chen',
			small_avatar:'small_avatar_address',
			avatar:'avatar_address'
		},
		{
			name:'Zijia Wang',
			small_avatar:'small_avatar_address',
			avatar:'avatar_address'
		},
		{
			name:'Song Lin',
			small_avatar:'small_avatar_address',
			avatar:'avatar_address'
		}
	]
}

//-------------Invite
{
	appid:AppId,
	opuid:client_generate_unique_in_current_client,
	op:OP.INVITE,
	userids:[userids]
}
</code></pre>