# SSH Tripwire

I've been thinking about ways to setup a notification if someone logs into one
of my servers. After some googling I found this article that was an excellent
[guide](https://ittavern.com/ssh-run-script-or-command-at-login/)

Based on that, I came up with the following script:

```
#!/bin/bash

# Set your Gotify URL and token
Gotify_URL='https://<GOTIFY_SERVER_URL'
Gotify_Token=<GOTIFY_TOKEN>

notify() {
    local user=$(whoami)
		local hostname=$(hostname)
		local original_user=$(logname)  # Get the original user who logged in
    local ip=$(echo $SSH_CONNECTION | awk '{print $1}')
    local title="SSH Login Alert - $hostname"
    local message="User: $original_user logged in from IP: $ip"

    curl -X POST "${Gotify_URL}/message?token=${Gotify_Token}" \
         -F "title=${title}" \
         -F "message=${message}" \
         -F "priority=5"
}

notify &> /dev/null # Run in background
```

Just replace the `GOTIFY_SERVER_URL` and `GOTIFY_TOKEN` with your own values.

Next, in order to execute the script I prefer to use PAM.

Open `/etc/pam.d/sshd` and add the following line:

```
session optional pam_exec.so type=open_session /path/to/your/script.sh
```

This will execute your script whenever an ssh connection is opened to the server
and it will only run when the session is opened. If you don't use the
`type=open_session` option, the script runs twice when the ssh connection is
closed also.
