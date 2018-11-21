This is a sample ~/.mssh_clusters, it is simply a yaml-looking set of machine lists
Why mssh?  because I started with it, and then switched to tmux...

##### So, given this **~/.mssh_clusters** file:
    ldap: ldap-001.my.secret.domain ldap-002.my.secret.domain
    nfs: nfs-00.my.secret.domain nfs-01.my.secret.domain
    docker-test: docker-test-01.my.secret.domain docker-test-02.my.secret.domain
    docker-swarm: docker-swarm-01.my.secret.domain docker-swarm-02.my.secret.domain docker-swarm-03.my.secret.domain

##### Completion examples that will work using this file:
1 $ tm lda<TAB>       # completes to "tm ldap" which connects to the two machines in that list (above)
2 $ tm docker.*       # connects to 5 machines (in docker-test and docker-smarm)
3 $ tmh ldap<TAB>     # interactive completion to one of the ldap full hostnames
4 $ tmh ldap-.*       # connects to both ldap machines
5 $ tmh docker-swarm-0[1-2].*  # connects to 01 and 02 (not 03).

