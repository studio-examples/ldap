ldap
====

This example shows how to connect to LDAP and query for users. Further more, it demonstrates usage of routing components, i.e. Collection Splitter and Collection Aggregator.

Step 1: download openLDAP and apache directory studio for windows
Step 2: edit c:\OpenLDAP\etc\openldap\slapd.conf by setting rootpw value at the bottom of the file to:
rootpw		"root"
so that section should look like this:
#######################################################################
# BDB database definitions
#######################################################################


database	bdb
suffix		"dc=my-domain,dc=com"
rootdn		"cn=Manager,dc=my-domain,dc=com"
# Cleartext passwords, especially for the rootdn, should
# be avoid.  See slappasswd(8) and slapd.conf(5) for details.
# Use of strong authentication encouraged.
rootpw		"root"
# The database directory MUST exist prior to running slapd AND 
# should only be accessible by the slapd and slap tools.
# Mode 700 recommended.
directory       ../var/openldap-data
# Indices to maintain


run c:\OpenLDAP\libexec\StartLDAP.cmd to start ldap server
Step 3: run apache dir studio and create a connection using this:
name: whatever
hostname: localhost
port: 389
click Check network parameter. if the test is not succesful, your ldap server is not running, otherwise next
bind dn: cn=Manager,dc=my-domain,dc=com
bind pass: root
click finish
Step 4: click right mouse on localhost node in the left bottom panel to import LDIF import file (ldap.ldif) that is packaged in the project. if you click on ROOT DSE in the left upper panel called LDAP browser, you should see the imported structure.
Step 5: import and run mule project
Step 6: the console should contain logs that show functionality of Collection Splitter. for each user record there is one log such as:
INFO  2014-07-01 10:44:59,914 [[ldap].connector.http.mule.default.receiver.02] org.mule.api.processor.LoggerMessageProcessor: LDAP user: dn: cn=admin,ou=people
uid: admin
sn: admin
userPassword:: bW1jYWRtaW4=
cn: admin
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson

using Collection aggregator we get a log of all the records:

INFO  2014-07-01 10:44:59,922 [[ldap].connector.http.mule.default.receiver.02] org.mule.api.processor.LoggerMessageProcessor: all users: [dn: cn=admin,ou=people
uid: admin
sn: admin
userPassword:: bW1jYWRtaW4=
cn: admin
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson

, dn: cn=testuser1,ou=people
uid: testuser1
sn: testuser1
userPassword:: dGVzdHVzZXIxMTIz
cn: testuser1
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson

, dn: cn=mmc,ou=people
uid: mmc
sn: mmc
userPassword:: bW1jMTIz
cn: mmc
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson

]







