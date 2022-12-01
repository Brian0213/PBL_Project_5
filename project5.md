# Documentation for Project 5: AUX PROJECT 1: SHELL SCRIPTING

## Preparing prerequisites

- Create a new EC2 Instance of t2.nano family with Linux Server 20.04 LTS (HVM) image.

You have been learning about Linux for some time, and it is time to start getting a feel of how to automate some work using Shell Scripts.

In this project, you need to onboard 20 new Linux users onto a server. Create a shell script that reads a csv file that contains the first name of the users to be onboarded.

Create the project folder called Shell:

`mkdir Shell`

![Create Shell Directory](./image/create-shell-dir.PNG)

- Move into the Shell folder

`cd Shell`

![Cd Shell Directory](./image/cd-shell-output.PNG)

- Create a csv file name names.csv:

`touch names.csv`

![Names Csv File](./image/names-csv-output.PNG)

- Add create a group in the server:

`groupadd developers`

To check the group exists:

`sudo groupadd developers`

![Developers Group Add](./image/developers-group-create.PNG)

- Open the names.csv file:

`vim names.csv`

![Developers Group Add](./image/names-created-in-names-csv.PNG)

- To add users to the group use the command:

`sudo usermod -a -G groupname username`

- Always use the -a (append) option when adding a user to a new group. If you omit the -a option, the user will be removed from any groups not listed after the -G option

- How to Create a New User and Assign Groups in One Command:

`sudo useradd -g users -G developers Ibukun`

![Adding Users to the Developers Group](./image/users-added-to-developers-grp-output.PNG)

N.B.
The script you created should read the CSV file, create each user on the server, and add to an existing group called developers (You will need to manually create this group ahead).

Ensure that your script will first check for the existence of the user on the system, before it will attempt to create that it.

Ensure that the user that is being created also has a default home folder

Ensure that each user has a .ssh folder within its HOME folder. If it does not exist, then create it.

For each user’s SSH configuration, create an authorized_keys file and ensure it has the public key of your current user.

- Before Deploying your script, you will need to update your current user with the correct public key and private key.

In your current home directory change directo .ssh folder:

`cd .ssh`

![Cd .ssh](./image/cd-.ssh-output.PNG)

- create a file for the public key:

`touch id_rsa.pub`

![Create Public file](./image/id-rsa-pub-output.PNG)

- open the file using your favorite editor and paste in the public key:

`vi id_rsa.pub`

![Paste Public Key](./image/public-key-paste-output.PNG)

- create a file for your private key:

`touch id_rsa`

![Create Private file](./image/private-file-create-output.PNG)

- open the file using your favorite editor and paste in the private key:

`vi id_rsa`

![Paste Private Key](./image/private-key-paste-output.PNG)

- Onboarding new users on the server:

- Change the security context to the new_user account so that folders and files you create have the correct permissions:

`sudo su - Lucas`

- Create a .ssh directory in the new_user home directory:

`mkdir .ssh`

- Use the chmod command to change the .ssh directory's permissions to 700. Changing the permissions restricts access so that only the new_user can read, write, or open the .ssh directory:

`chmod 700 .ssh`

- Use the touch command to create the authorized_keys file in the .ssh directory:

`touch .ssh/authorized_keys`

- Use the chmod command to change the .ssh/authorized_keys file permissions to 600. Changing the file permissions restricts read or write access to the new_user:

`chmod 600 .ssh/authorized_keys`

- Run the Linux cat command in append mode:

`cat >> .ssh/authorized_keys`

- Paste the public key into the .ssh/authorized_keys file and then press Enter:

N.B.  For most Linux command line interfaces, the Ctrl+Shift+V key combination pastes the contents of the clipboard into the command line window.

- Press and hold Ctrl+d to exit cat and return to the command line session prompt:

- Run the id command from the instance's command line to view the user and group information created for the new_user account:

`id`

The id command returns information similar to the following:

![Onboard Output](./image/onboard-success-output.PNG)
