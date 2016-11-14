# 1a. Check vm.swappiness on all your nodes: http://askubuntu.com/questions/103915/how-do-i-configure-swappiness
cat /proc/sys/vm/swappiness
-> 60
# 1b. Set the value to 1 if necessary
sudo sysctl vm.swappiness=1
cat /proc/sys/vm/swappiness
-> 1

# 2. Show the mount attributes of all volumes


Show the reserve space of any non-root, ext-based volumes
Show that transparent hugepages is disabled
Report the network interface attributes
Show forward and reverse host lookups using getent and nslookup
Verify the nscd service is running
Verify the ntpd service is running


