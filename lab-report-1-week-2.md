# Lab 1 REMOTE ACCESS

***Here is a tutorial on how to log into a cs 15l course-specific account on ieng6.***

## Step 1. Download Visual Studio Code

![lab1 1](https://user-images.githubusercontent.com/97600878/149136487-f3ce64e3-9c35-4ff7-bc74-b65f3e28d578.png)
Go to the Visual Studio Code website https://code.visualstudio.com, download and install.
After you finished install, run Visual Studio Code, you should see this:
![lab1 2](https://user-images.githubusercontent.com/97600878/149136788-28b656f0-d425-4064-8740-f3ba68e86279.png)

## Step 2. Remotely Connecting

>If you are using Windows, make should you set up OpenSSH first.

First open terminal, you can access from the top left, terminal -> new terminal.

Then command: `ssh (youraccount)@ieng6.ucsd.edu`
For example mine is:
- `ssh cs15lwi22awn@ieng6.ucsd.edu`
- Type Yes when first time connect to the server.
- Then you need to type the password you set for this course account (It won't show up, but don't worry).

Then you should see this page, which means you have connected to the remote server.

![lab1 3](https://user-images.githubusercontent.com/97600878/149138744-647938a5-bc25-4256-ab72-c471031ab26d.png)

## Step 3. Run Some Commands

Now your terminal is connected to the server, you can try out some commands. For example:

- `cd ~`
- `cd`
- `ls -lat`
- `ls -a`
- `ls <directory>` where <directory> is /home/linux/ieng6/cs15lwi22/cs15lwi22abc, where the abc is one of the other group members’ username
- `cp /home/linux/ieng6/cs15lwi22/public/hello.txt ~/`
- `cat /home/linux/ieng6/cs15lwi22/public/hello.txt`
- `Ctrl D (exit)`
  
  ![lab1 4](https://user-images.githubusercontent.com/97600878/149139644-b44b6c46-bd23-457d-a437-3e381c75e5e3.png)

  ## Step 4. Moving Files with scp
  
  The `scp` command can copy a file from your computer to the remote computer
  First, we create a file call `WhereAmI.java` to demonstrate how `scp` command work:

 ```
    class WhereAmI {
  
    public static void main(String[] args) {
  
    System.out.println(System.getProperty("os.name"));
  
    System.out.println(System.getProperty("user.name"));
  
    System.out.println(System.getProperty("user.home"));
  
    System.out.println(System.getProperty("user.dir"));
    }
  
   }
  ```
  
  Here is how `WhereAmI` will looks like when you run on your computer
  ![11](https://user-images.githubusercontent.com/97600878/149141050-5401e811-f830-4dd8-ab02-43e43d9b45d3.png)
  
  Now we use the scp command to copy it to the remote computer (use your course-specific account):
  
  `scp WhereAmI.java cs15lwi22awn@ieng6.ucsd.edu:~`
  
  then the terminal should prompt for password, type your password.
  
  ![lab1 5](https://user-images.githubusercontent.com/97600878/149144517-ca99b98d-e782-402f-afb2-291e70c79ca8.png)
  
  this means the file was copied successfully.
  
  - remember to run this command using your client not the remote server
  
  Then we can go back to the server using ssh command
  
  use ls to see if the file is copied
  
  ![lab1 6](https://user-images.githubusercontent.com/97600878/149144734-1d8d5858-9b43-408f-80b2-ed65ed7f0afe.png)
  
  now we see that `WhereAmI.java` is now copied to the remote server. 
  
  we can try to run it on the server:
  
  ![lab1 7](https://user-images.githubusercontent.com/97600878/149144995-a68e9737-873c-4335-bf62-b1231655c9fe.png)
  
  and we can tell that it runs correctly on the server by the information it shows.
 
  ## Step 5. Setting an SSH Key
  
  We can use SSH key so we don't need to type password every time we run `ssh` and `scp`. 
  We can use this command to do so:
  
  `ssh-keygen`
  
  In this command, we creates a pair of files called the public key and private key. You copy the public key to a particular location on the server, and the private key in a 
  particular location on the client. Then, the ssh command can use the pair of files in place of your password.
  
  Once you enter the command, the terminal is going to ask where to store the file and the passphrase.
  
  ![lab1 8](https://user-images.githubusercontent.com/97600878/149162125-7c13f247-9fb8-4d45-8c65-ee5f27f88302.png)

  now you have generate two files of public key and private key (`id_rsa` and `id_rsa.pub`)
  
  ![lab1 9](https://user-images.githubusercontent.com/97600878/149162308-5be050d0-26bf-4043-8035-d4d1c0d52150.png)
  
  and we `scp` them into the remote server
  
  ![WeChat Screenshot_20220112071019](https://user-images.githubusercontent.com/97600878/149166883-00a4bbc7-ad3b-4fea-adba-74a3308bec71.png)
  
  now you don't need to type password when you login the server with ssh and scp the file from your computer to the server.
  
  
  ## Step 6. Optimizing Remote Running
  
  You can run command in remote server directly with "" with ssh command. For example,if you want to run ls command diretly on the server：
  
  - `ssh cs15lwi22awn@ieng6.ucsd.edu "ls"`
  
  you can also run multiple command on the same line. For example:
  
  - `$ cp WhereAmI.java OtherMain.java; javac OtherMain.java; java WhereAmI`
  
 ![WeChat Screenshot_20220112071816](https://user-images.githubusercontent.com/97600878/149168375-e5517419-d287-41b5-b260-fcccfcf96ad1.png)
  
  In here, we use the command  `ssh cs15lwi22awn@ieng6.ucsd.edu "ls"` to access the remote directory directly.
  
  ![WeChat Screenshot_20220127023513](https://user-images.githubusercontent.com/97600878/151342135-aa380a22-0ecf-4974-8dbc-85a602244914.png)
  
  We can also run the file `WhereAmI.java` remotely directly from your desktop by using
  
  `ssh cs15lwi22awn@ieng6.ucsd.edu "javac WhereAmI.java; java WhereAmI"`
  

  All these are examples to optimize speed on remote server.
  
## End of Tutorial
  
