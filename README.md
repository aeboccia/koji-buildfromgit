What is Koji-BFG?

Koji-BFG (Koji Build From Git) is a simple service which can reside anywhere within the koji infrastructure, probably best to leave it on the hub. It listens for an incoming connection which is initiated by a git hook. The hook sends all info needed by the listener to initiate a build automatically in the koji build system for the recently committed code in GIT.

How do I set it up?

1) Eventually I will have some RPMS available but for now grab the code from github.

2) Create a system account on the machine you plan on running the listener

3) Create an account in Koji for the user you created a system account for

4) As root copy koji-bfg /usr/local/bin (You can change this location if you desire, but be sure to edit the service file if you do). Make sure it is executable by atleast your user created above

5) Copy kbfg.conf to /etc/koji-bfg/kbfg.conf make the necessary edits and ensure it is atleast readable by the user you created previously

6) Edit the koji-bfg.service and update User= with the name of the user you created previously

7) Install the post-receieve hook into the hooks dir of your git repo also ensure you make necessary edits to server_address

8) Start the listener, and test it is all working by committing and pushing code.

Usage:

For a scratch build commit with
git commit -m 'This is a test scratch build #kojibuild #scratch #tag'

For a Tracked build commit with
git commit -m 'This is a test REAL build #kojibuild #tag'
