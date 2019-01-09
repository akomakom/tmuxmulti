## What this is
The two bash completion scripts provide two bash completion prefixes: 
* **tm** or **tmuxmulti** ("Connect in a split terminal to all hosts in the matched list(s)")
* **tmh** or **tmuxmultihost** ("Tmux Multi by Host", same but for matching against the hostnames rather than list names)

The system-of-record for both of these is your **~/.tmux_clusters** file (see below).


## Installation
### Option 1 (static)
1. Copy one or both scripts to your /etc/bash_completion.d/
2. Create a ~/.tmux_clusters with lists of your hosts (see below)
3. Re-login or run `. /etc/bash_completion` in any shell you want to use this in.

### Option 2 (dynamic, you can just `git pull` to update to latest)
1. Check out this gist: 
    `git clone git@gist.github.com:2dab995b6a48899eee841cc0e4a3192e.git`
2. Symlink the two files: 
    ```
    ln -s /full/path/to/tmuxmulti /etc/bash_completion.d/
    ln -s /full/path/to/tmuxmultihost /etc/bash_completion.d/
3. Follow the **static** instructions from step 2.

## Usage

Given this **~/.tmux_clusters** file:

    ldap: ldap-001.my.secret.domain ldap-002.my.secret.domain
    nfs: nfs-00.my.secret.domain nfs-01.my.secret.domain
    docker-test: docker-test-01.my.secret.domain docker-test-02.my.secret.domain
    docker-swarm: docker-swarm-01.my.secret.domain docker-swarm-02.my.secret.domain docker-swarm-03.my.secret.domain

### Completion examples that will work using this file:
(All commands will only work from within tmux)
```
tm ldap           # connect to the two machines on the ldap: line
tm lda<TAB>       # completes to "tm ldap", same as previous
tm docker.*       # connects to 5 machines (in docker-test and docker-smarm)

tmh ldap<TAB>     # interactive completion to one of the ldap full hostnames
tmh ldap          # connects to both ldap machines (same as ldap-.* in this case)
tmh ldap-.*       # connects to both ldap machines 
tmh docker-swarm-0[1-2].*  # connects to 01 and 02 (not 03).
```
