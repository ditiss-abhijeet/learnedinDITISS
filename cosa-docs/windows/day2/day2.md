

1. **Disk Manager** - It tell which utility is installed on the computer and therefore you check check which hardware, say a network card, device manager will tell who is the network card manufracturer. Whe it is about the **server** upgrade, you need to know what it is.

2. **User Management** - Administrator has all the user management access. You need to add users and manage users. OS gives you default users and therefore all the permissions are already given, if you need to change ther permission, administrator does that.
  - **User meta data** - There are policies for users, the permissions, all of these are saved on **database**, another if **SQL**, then **Excel**, and therefore it is called **flat databases**.
  - **`windows/system32/config`** - This file holds the username passowrds groups etc., it is called **SAM (Security Accounts Manager)** file, similarly in linux there is `/etc/passwd` where everything users password and information is stored.

# How do you add Users?

1. **Create a User** - Go to run and run command `compmgmt.conf`, from where yo can create a user and manage it.

2. **Change Password on Next Logon**
  - You can select the option that will *change the password on the next logon*, when the user will log in another time, the OS will ask user to change the passwords.
  - Then there is *Password never expires*, it is for s/w which has paswwords, then the username for that account is created. 
  
THough mostly you'd be looking at **Command Lines** for the same.

- `net user /`
- `net /?`
- `cls`

- `net user hacker * /add` - this will add a user 


### Windows WORKGROUP Mode

Remember that each computer follows its own security database and that is stored in **SAM** file, storing passwords and usernames and other details. Therefore, every system works independently, hence it is called **Workgroup** Mode, only those users created within the system will be available to use on the same system system only. Thus the user created on one coputer ca log on from that computer only, that user cannot log on to other computer.

- **Shared Folders**
    - Now if you need to give access to specific user, but the user isn't using the same Machine and therefore if he needs to access the file, he needs to run down to that machine only then he can, but there is solution to this problem, i.e., **Shared Folders**, **File Sharing service**.

    - The shared folders will be available to the machines on the same network. And thus, you can access the file, *if they are sharing the same network*.

    - **How to make sure the network is same**
        - First you need to check whether the networks are on the same subnet.
        - You would need to share the data.
    
    - **How to make sure that there is no password sharing problem**
        - So you need to create one user on all the sytems having same name and same password, such that **SAM** can recognise the same user trying to access the **shared file** from differnt machine without authentication.

- **Central Security Database**
    - Instead of working in **Workgroup** mode, you will have only one account, through which you'll be able to manage all the users within the organisation.


# ADDS (Active Directory Domain Service)

It is the service that allows you to create a centralised security database. You need a plan that you need to execute because here you are not going to configure **AD** on all 1000 machines, but only one.

1. Therefore, **Domain**
  - It is logical group of computers or devicees which follow a comman security database, such that these logical groups are not fixed and can be changed as per requirements.
  - These domain names can be given in **internet** format, such as, ***sunbeam.com***, ***ditiss.lab***.

2. **Domain Tree**
  - It is collection of domanis which share a comman namespace and are bind with parent and child realationship.
  - If you create a name with *cdac.com* and *param.cdac.com*, then *cdac.com* becomes the parent of *param.cdac.com* and therefore it follows the tree structure, hierarchical structure.



    


