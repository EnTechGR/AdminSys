Start the VM to boot the previously installed Debian system.

Do the following for both a user and the [superuser](https://en.wikipedia.org/wiki/Superuser) (`root`) :

- Start the console.
  - Press: Ctrl + Alt + F3 to enter terminal

- Login in the console
  - At the login prompt, type your username and hit Enter.
  - Type your password (it will be invisible) and hit Enter.
- Clear the console using the keyboard shortcut
  - Press Ctrl + L
- Change the password to this : `michelle`
  - Type the command passwd and hit Enter.
  - It will ask for your current password first.
  - Enter the new password: michelle
  - Retype it to confirm.
- Show the command history using five keystrokes or less (using autocompletion)
  - Type hi (2 keystrokes)
  - Press Tab (1 keystroke) — This autocompletes "hi" to "history"
  - Press Enter (1 keystroke)

- Log out using the keyboard shortcut
  - Press Ctrl + D

### Just numbers

Login as [`root`](https://en.wikipedia.org/wiki/Superuser) on the third [Linux console](https://en.wikipedia.org/wiki/Linux_console).

Check the Internet connectivity with the command `ping google.com`.
After a few hops, interrupt the program with : <kbd>Ctrl</kbd> + <kbd>C</kbd>.

Behind every name in a computer system there is a number (ID, index, address, etc) :

- User identifier
  - `root` → `0`
  - `student` → `1000`
- IP address
  - google.com → 216.58.214.14 (quad-dotted notation) → `3627734542`
  - tencent.com → 117.169.101.44 (quad-dotted notation) → `1974035756`
- File inode
  - `/etc/fstab` → `44696029`
  - `.profile` → `59639363`
- Port
  - `HTTP` → `80`
  - `HTTPS` → `443`
- Process identifier
  - `cron` → `254`

Names exist because they are human readable, but behind the scenes they are converted into numbers, unique in their namespace :

- A domain name can map to several IP addresses (for load balancing), and a single IP address can host many different domain names (via Virtual Hosting).
- Several processes may have the same name, but a PID identifies a single process

Find the commands to get :

- the inode of a specific file
  - ls -i /etc/fstab
  - stat /etc/fstab
- the current user ID
  - id -u
  - id
- the PID of a program, for example `bash`
  - pidof bash
  - pgrep bash
  - ps aux | grep bash