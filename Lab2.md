# Lab Report 2

## Part 1: ChatServer Interactions

Welcome to Lab Report 2, where we dive into the intricacies of our `ChatServer`'s interactions, tracking the flow of messages and observing the underlying mechanics of our Java server in action.

### Code 

![Image](Code.png)
![Image](1.png)
![Image](2.png)


### Interaction 1: jpolitz's Greeting
After I launched my ChatServer on port 4000, the first user, jpolitz, sent a greeting:
![Image](3.png)

- **URL Accessed**: `/add-message?s=Hello&user=jpolitz`
- **Method Called**: My `handleRequest(URI url)` method in the `Handler` class got to work.
- **Arguments I Handled**: I passed the `handleRequest` method a `URI url` with the value `new URI("/add-message?s=Hello&user=jpolitz")`.
- **Changes in My Fields**: My `chatMessages` string, initially an empty canvas, now captured "jpolitz: Hello\n".

### Interaction 2: yash's Question
Not long after, yash joined the chat, adding to the conversation:
![Image](4.png)

- **URL Accessed**: `/add-message?s=How are you&user=yash`
- **Method Called**: Once more, `handleRequest(URI url)` in my `Handler` class was up for the task.
- **Arguments I Handled**: The `URI url` was provided with `new URI("/add-message?s=How are you&user=yash")`.
- **Changes in My Fields**: My `chatMessages` string now included "jpolitz: Hello\nyash: How are you\n".

### Interaction 3: Joseph Introduces Himself
Then I, Joseph, decided to join my own server:
![Image](5.png)

- **URL Accessed**: `/add-message?s=Hello, my name is Joseph!&user=Joseph`
- **Method Called**: My `handleRequest(URI url)` method was consistently reliable.
- **Arguments I Handled**: I provided the `URI url` with `new URI("/add-message?s=Hello, my name is Joseph!&user=Joseph")`.
- **Changes in My Fields**: My `chatMessages` string was updated to include "Joseph: Hello, my name is Joseph!\n".

### Interaction 4: FactBot's Fun Fact
Finally, FactBot shared an interesting fact with everyone:]
![Image](6.png)

- **URL Accessed**: `/add-message?s=Did you know the Moon moves away from Earth by 4cm every year?&user=FactBot`
- **Method Called**: Again, `handleRequest(URI url)` in `Handler` was called into service.
- **Arguments I Handled**: I took the `URI url` argument with `new URI("/add-message?s=Did you know the Moon moves away from Earth by 4cm every year?&user=FactBot")`.
- **Changes in My Fields**: My `chatMessages` string expanded to include "FactBot: Did you know the Moon moves away from Earth by 4cm every year?\n".


In each of these exchanges, the `handleRequest` method diligently parses the incoming request's URL, teases apart the user and message details, and meticulously updates the `chatMessages` field to reflect the ongoing conversation. This field acts as a living record, charting the ebb and flow of our server's dialogues.

## Part 2: SSH Key Management and Remote Access

In this part of my lab journey, I focused on understanding and utilizing SSH keys for secure remote access to servers. Here's a step-by-step account of how I generated, located, and used SSH keys for logging into a remote server without needing a password.

### Generating SSH Keys

- I started by opening a terminal on my system and running the `ssh-keygen` command to generate a new pair of SSH keys.
- During the process, I was prompted to specify the file location for the keys. I chose to save them in the default location (`~/.ssh/id_rsa` for the private key and `~/.ssh/id_rsa.pub` for the public key).
- I decided to skip setting a passphrase for simplicity, though it's an option for additional security.
- The command successfully created my identification and public key, displaying the key's fingerprint and a randomart image for visual identification of the key.
![Image](Part2pic1.png)

### Locating the SSH Keys

- Next, I wanted to confirm the existence and location of my newly generated SSH keys.
- I used the `ls -l ~/.ssh/id_rsa` command to display details about my private key, confirming its presence in my `.ssh` directory.
- I also ran `ls -l ~/.ssh/` to list all files in my `.ssh` directory, where I found the `id_rsa` (private key), `id_rsa.pub` (public key), and the `known_hosts` file.
![Image](Part2pic2.png)

### Copying Public Key to Remote Server

- With my public key ready, I used the `scp` command to securely copy it to the `authorized_keys` file on the remote server (ieng6 in this case).
- After entering my password, the public key was successfully transferred to the remote server's `~/.ssh/authorized_keys` file.
![Image](Part2pic3.png)

### SSH into Remote Server Without a Password

- Finally, I tested SSH access to the ieng6 server using my newly set up SSH keys.
- I ran `ssh Jwhiteman@ieng6.ucsd.edu` and was able to log in without being prompted for a password, thanks to the SSH key authentication.
- Upon logging in, I was greeted with the server's welcome message and some system status information.
![Image](Part2pic4.png)

## Part 3: Learning Outcomes from Recent Labs

In these last labs, I learned how to deploy and manage a Java-based chat server on a remote server. This includes comprehending how numerous users can communicate with the server concurrently. I also acquired actual experience using SSH keys for secure and convenient remote server access, which eliminates the need for password authentication. This knowledge is useful for efficiently and securely managing remote servers and applications.
