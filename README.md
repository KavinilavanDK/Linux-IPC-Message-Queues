#### NAME: KAVI NILAVAN DK
#### REG NO: 212223230103
# Linux-IPC-Message-Queues
Linux IPC-Message Queues

# AIM:
To write a C program that receives a message from message queue and display them

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux message queues API 

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## C program that receives a message from message queue and display them
 ```   
#include <stdio.h> 
#include <sys/ipc.h> 
#include <sys/msg.h> 
#include <string.h>
#include <stdlib.h>

struct mesg_buffer { 
	long mesg_type; 
	char mesg_text[100]; 
} message; 
int main() 
{ 	key_t key; 
	int msgid; 

	key = ftok("progfile", 65); 


	msgid = msgget(key, 0666 | IPC_CREAT); 
	message.mesg_type = 1; 
	printf("Write Data : "); 
scanf("%s",message.mesg_text);

	msgsnd(msgid, &message, sizeof(message), 0); 

	printf("Data send is : %s \n", message.mesg_text); 
	return 0; 
}

 

#include <stdio.h>
#include <sys/ipc.h>
#include <sys/msg.h>


struct mesg_buffer {
	long mesg_type;
	char mesg_text[100];
} message;
int main()
{
	key_t key;
	int msgid;
// ftok to generate unique key
	key = ftok("progfile", 65);
	// msgget creates a message queue
	// and returns identifier
	msgid = msgget(key, 0666 | IPC_CREAT);
	// msgrcv to receive message
	msgrcv(msgid, &message, sizeof(message), 1, 0);
	// display the message
	printf("Data Received is : %s \n",
			message.mesg_text);

	// to destroy the message queue
	msgctl(msgid, IPC_RMID, NULL);
	return 0;
}
```
 OUTPUT
##![Screenshot 2024-04-04 103715](https://github.com/KavinilavanDK/Linux-IPC-Message-Queues/assets/144870429/66e91574-2018-41f2-9f05-c2ebd707ff3a)
# RESULT:
The programs are executed successfully.
