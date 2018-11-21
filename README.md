## What this is
The two bash completion scripts provide two bash completion prefixes: 
* tm or tmuxmulti (aka "Connect in a split terminal to all hosts in the matched list(s)")
* tmh or tmuxmultihost ("Tmux Multi by Host", same but for matching against the hostnames rather than list aliases)

The system-of-record for both of these is your **~/.mssh_clusters**
Why is this based on mssh when it doesn't actually use mssh?  because I started with it, and then switched to tmux...

### Installation
1. Copy one or both scripts to your /etc/bash_completion.d/
2. Create a ~/.mssh_clusters with lists of your hosts (see below)
3. Re-login or run `. /etc/bash_completion` in your shell

### So, given this **~/.mssh_clusters** file:
    ldap: ldap-001.my.secret.domain ldap-002.my.secret.domain
    nfs: nfs-00.my.secret.domain nfs-01.my.secret.domain
    docker-test: docker-test-01.my.secret.domain docker-test-02.my.secret.domain
    docker-swarm: docker-swarm-01.my.secret.domain docker-swarm-02.my.secret.domain docker-swarm-03.my.secret.domain

### Completion examples that will work using this file:
```
tm lda<TAB>       # completes to "tm ldap" which connects to the two machines in that list (above)
tm docker.*       # connects to 5 machines (in docker-test and docker-smarm)

tmh ldap<TAB>     # interactive completion to one of the ldap full hostnames
tmh ldap-.*       # connects to both ldap machines
tmh docker-swarm-0[1-2].*  # connects to 01 and 02 (not 03).
```
