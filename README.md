fellows
=======
```
/*
ENUMS

AppId:
id:10	"Fellows"

Operations :
id:1	"SEND_MESSAGE"
id:2	"READ_RECEIPT"
id:3	"INVITE"
id:4	"GET_USER_INFO"
id:5	"GET_SESSIONS"
id:6	"GET_HISTORY"
id:7	"LEAVE"
id:8	"RENAME"
id:9	"GROUP_INFO"

*/

//------------Send Message
//**request
{
	appid:AppId,
	opuid:client_generate_unique_in_current_client,
	op:OP.SEND_MESSAGE,
	to:[userids],
	*or*
	to_group:{groupid}
	content:"Message Content",
	timestamp:{long time}
	settings:{
		backup:0|1,
		require_read_back:0|1
	}
}
//** respond
{
	opuid:client_generate_unique_in_current_client,
	(@optional) groupid:{groupId_generate_by_server_unique_in_global}  // it might be newly created
	sended:1|0
}
//** server to client(s)
{
	op:OP.SEND_MESSAGE,
	to:[userids](except sender),
	from:{group_id},
	sender:{user_id},
	messageID:messageID(server_generate_message_id_unique_in_global),
	content:"Message Content",
	timestamp:{long time}
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
	messageID:messageID,
	timestamp:{long time}
}
//** server to client(s)
{
	op:OP.READ_RECEIPT,
	to:[userids],
	messageID:messageID,
	timestamp:{long time}
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
//**request
{
	appid:AppId,
	opuid:client_generate_unique_in_current_client,
	op:OP.INVITE,
	userids:[userids],
	to_group:{group_id}
}
//** respond
{
	opuid:client_generate_unique_in_current_client,
	status:1|0
}

//-------------Get Sessions
//**request
{
	appid:AppId,
	opuid:client_generate_unique_in_current_client,
	op:OP.GET_SESSIONS
}
//** respond
{
	opuid:client_generate_unique_in_current_client,
	sessions:[{
			groupid:{groupid},
			histories:[{
					from:{userid},
					message_id:{messageid},
					content:"Message Content",
					timestamp:{long time}
				},{
					from:{userid},
					message_id:{messageid},
					content:"Message Content",
					timestamp:{long time}
				}
			]
		},{
			groupid:{groupid},
			histories:[{
					from:{userid},
					message_id:{messageid},
					content:"Message Content",
					timestamp:{long time}
				},{
					from:{userid},
					message_id:{messageid},
					content:"Message Content",
					timestamp:{long time}
				}
			]
		}
		...
	]
}

//-------------Get History
//**request
{
	appid:AppId,
	opuid:client_generate_unique_in_current_client,
	op:OP.GET_HISTORY,
	groupid:{groupid},
	before_message:{message_id},
	*or* *both*
	after_message:{message_id}
}
//**respond
{
	opuid:client_generate_unique_in_current_client,
	histories:[{
		from:{userid},
		message_id:{messageid},
		content:"Message Content",
		timestamp:{long time}
	},{
		from:{userid},
		message_id:{messageid},
		content:"Message Content",
		timestamp:{long time}
	}]
}

//-------------Leave Group
//**request
{
	appid:AppId,
	opuid:client_generate_unique_in_current_client,
	op:OP.LEAVE,
	groupid:{groupid},
	timestamp:{long time}
}
//**respond
{
	opuid:client_generate_unique_in_current_client,
	leave:0|1
}
//** server to client(s)
{
	op:OP.LEAVE,
	userid:{userid},
	groupid:{groupid},
	timestamp:{long time}
}


//-------------Rename Group
//**request
{
	appid:AppId,
	opuid:client_generate_unique_in_current_client,
	op:OP.RENAME,
	groupid:{groupid},
	new_name:"new_name",
	timestamp:{long time}
}
//**respond
{
	opuid:client_generate_unique_in_current_client,
	rename:0|1
}
//** server to client(s)
{
	op:OP.RENAME,
	userid:{userid},
	groupid:{groupid},
	new_name:"new group name",
	timestamp:{long time}
}


//-------------Get Group Infomation
//**request
{
	appid:AppId,
	opuid:client_generate_unique_in_current_client,
	op:OP.GROUP_INFO,
	groupid:{groupid}
}
//**respond
{
	opuid:client_generate_unique_in_current_client,
	name:"Group Name",
	users:[{
		id:{userid},
		name:{username}
	},{
		id:{userid},
		name:{username}
	}],
	group_settings:{}
}

```