
## How to install Splunk
## more info: https://docs.splunk.com/Splexicon
### SPL - Search Processing Language

```
root@splunk:~# cat /opt/splunk/etc/apps/search/local/inputs.conf
[monitor:///var/log/auth.log]
disabled = false
host = splunk.jnrlabs.com
sourcetype = OS-Auth

```



```
1. download splunk
2. untar and copy splunk folder to /opt
3. /opt/splunk/bin/splunk

root@splunk:/opt# ./splunk/bin/splunk start --accept-license

This appears to be your first time running this version of Splunk.

Splunk software must create an administrator account during startup. Otherwise, you cannot log in.
Create credentials for the administrator account.
Characters do not appear on the screen when you type in credentials.

Please enter an administrator username: administrator
Password must contain at least:
   * 8 total printable ASCII character(s).
Please enter a new password:
Please confirm new password:
Copying '/opt/splunk/etc/openldap/ldap.conf.default' to '/opt/splunk/etc/openldap/ldap.conf'.
Generating RSA private key, 2048 bit long modulus
............+++++
..............+++++
e is 65537 (0x10001)
writing RSA key

Generating RSA private key, 2048 bit long modulus
........+++++
.........+++++
e is 65537 (0x10001)
writing RSA key

Moving '/opt/splunk/share/splunk/search_mrsparkle/modules.new' to '/opt/splunk/share/splunk/search_mrsparkle/modules'.

Splunk> Be an IT superhero. Go home early.

Checking prerequisites...
        Checking http port [8000]: open
        Checking mgmt port [8089]: open
        Checking appserver port [127.0.0.1:8065]: open
        Checking kvstore port [8191]: open
        Checking configuration... Done.
                Creating: /opt/splunk/var/lib/splunk
                Creating: /opt/splunk/var/run/splunk
                Creating: /opt/splunk/var/run/splunk/appserver/i18n
                Creating: /opt/splunk/var/run/splunk/appserver/modules/static/css
                Creating: /opt/splunk/var/run/splunk/upload
                Creating: /opt/splunk/var/run/splunk/search_telemetry
                Creating: /opt/splunk/var/spool/splunk
                Creating: /opt/splunk/var/spool/dirmoncache
                Creating: /opt/splunk/var/lib/splunk/authDb
                Creating: /opt/splunk/var/lib/splunk/hashDb
New certs have been generated in '/opt/splunk/etc/auth'.
        Checking critical directories...        Done
        Checking indexes...
                Validated: _audit _configtracker _internal _introspection _metrics _metrics_rollup _telemetry _thefishbucket history main summary
        Done
        Checking filesystem compatibility...  Done
        Checking conf files for problems...
        Done
        Checking default conf files for edits...
        Validating installed files against hashes from '/opt/splunk/splunk-9.0.1-82c987350fde-linux-2.6-x86_64-manifest'
        All installed files intact.
        Done
All preliminary checks passed.

Starting splunk server daemon (splunkd)...
Generating a RSA private key
.........................................................................................+++++
......................................+++++
writing new private key to 'privKeySecure.pem'
-----
Signature ok
subject=/CN=splunk.jnrlabs.com/O=SplunkUser
Getting CA Private Key
writing RSA key
PYTHONHTTPSVERIFY is set to 0 in splunk-launch.conf disabling certificate validation for the httplib and urllib libraries shipped with the embedded Python interpreter; must be set to "1" for increased security
Done


Waiting for web server at http://127.0.0.1:8000 to be available.................. Done


If you get stuck, we're here to help.
Look for answers here: http://docs.splunk.com

The Splunk web interface is at http://splunk.jnrlabs.com:8000


```
```

Splunk - Used SPL - Search processing language.
Forwarders - Collecting the data and forwarding it to other Splunk Instances.
Indexes - Data is stored
Search Heads - Analyze, Visualize and report the Data
```
## Enable boot start
```
root@splunk:/opt# ./splunk/bin/splunk enable boot-start
Init script installed at /etc/init.d/splunk.
Init script is configured to run at boot.

```
## Splunk fundamentals.
```
1. Events
2. Search
3. Repoprt
4. Dashboard
5. SPL - Splunk Search Processing Language.
6. SourceType
7 Index
8. Field Extractions
9. Lookup Tables
```
# Splunk Infrastructure/Servers
## Indexer
## Search Head



```
root@splunk:/opt/splunk/bin# ./splunk btool inputs list --debug | grep -i auth
/opt/splunk/etc/system/default/inputs.conf                             [blacklist:/opt/splunk/etc/auth]
/opt/splunk/etc/apps/search/local/inputs.conf                          [monitor:///var/log/auth.log]
/opt/splunk/etc/apps/search/local/inputs.conf                          sourcetype = OS-Auth
/opt/splunk/etc/apps/python_upgrade_readiness_app/default/inputs.conf  passAuth = splunk-system-user
/opt/splunk/etc/apps/python_upgrade_readiness_app/default/inputs.conf  passAuth = splunk-system-user
/opt/splunk/etc/apps/python_upgrade_readiness_app/default/inputs.conf  passAuth = splunk-system-user



```
