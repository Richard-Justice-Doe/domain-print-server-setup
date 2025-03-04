# domain-print-server-setup
Step-by-step guide to configuring a Windows Domain Controller and Print Server.


Step 2: Test Printer Functionality
Try printing from a client PC.
If it fails, check Print Spooler Service (services.msc).
Step 3: Verify DNS and Login Issues
Ensure client DNS is set to 172.20.75.3.
Restart Netlogon and DNS services:

###   net stop netlogon && net start netlogon
###   net stop dns && net start DNS

# Conclusion
✅ Domain Authentication
✅ Group Policies Applied
✅ Centralized Printing
✅ Network Access Control Established

📌 Notes
Regularly back up Active Directory.
Monitor event logs for authentication or print server issues.
Ensure print server drivers are up-to-date.
🚀 Deployment Completed Successfully!
