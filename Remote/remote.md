remote Connect To type commands in a distant shell, you can use your peripherals (keyboard, monitor) or **SSH**.

It is more comfortable to use **SSH** because you can use your usual terminal, with the right keymap, theme, etc.

To do this exercise you will need to add this VM:

For VirtualBox 01_remote

For **UTM** 01_remote

Because the VM is behind the virtualization software router, you can't access it directly unless you add a port forwarding rule in the VM settings that maps a host port to a guest port.

Host refers to your physical machine.

Guest refers to the VM.

Initial Setup:

In your VM settings (Network), add a rule:

Host Port: **2222** (or any free port on your machine).

Guest Port: 22.

Connect via **SSH**:

Bash ssh -p **2222** root@localhost (Credentials: root / password is a single space)

Configure It is recommended to change the default **SSH** port (22) to prevent bots from trying to connect to it. Since we are pretending that the guest VM is a server, change the **SSH** service port and make sure the port forwarding still works! In addition, you will need to allow the new port in the firewall ufw.

Solution To successfully change the port without losing access, follow these steps:

## Modify the SSH Configuration

Open the **SSH** daemon configuration file:

Bash nano /etc/ssh/sshd_config Locate the line #Port 22. Remove the # and change the number to your chosen port (e.g., **4242**):

Plaintext Port **4242** Save and exit (Ctrl+O, Enter, Ctrl+X).

## Update the Firewall (ufw)

Before restarting the service, you must allow the new port through the firewall, or you will be locked out:

Bash ufw allow **4242**/tcp ufw reload ## Update VM Port Forwarding You must now update your VirtualBox/**UTM** settings to point to the new internal port:

Go to Network Settings -> Advanced -> Port Forwarding.

Change the Guest Port from 22 to **4242**.

(Note: You can leave the Host Port as **2222**).

## Restart SSH and Reconnect

Apply the changes inside the VM:

Bash systemctl restart ssh Now, exit your current session and reconnect using the updated mapping:

Bash ssh -p **2222** root@localhost