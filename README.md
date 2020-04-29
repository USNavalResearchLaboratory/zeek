**Zeek Statistics Framework Bug Correction**

_submitted by Brittany Donowho on April 29, 2020_ 

_source code located at https://github.com/zeek/zeek/blob/master/scripts/policy/misc/stats.zeek and in this repo under stats.zeek for reference_



This repository contains the correction made to a logic error in the Statistics framework of the Zeek open-source network security monitoring tool. 

The Statistics framework maintains counts on various data points, such as number of packets processed or dropped, number of bytes received, number of TCP connections, etc.
This information is all logged to stats.log in Zeek. However, when the Zeek engine is about to shut down, the original source code does not log the last round of counts.
Therefore, several numbers are missing from the final counts. 

To fix this issue, the code starting at line 102 of the _stats.zeek_ file :

```
if ( zeek_is_terminating() )
		# No more stats will be written or scheduled when Zeek is
		# shutting down.
		return;
    
```

is moved to execute _after_ the information is properly logged.


