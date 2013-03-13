Consistent Network Updates
===============
***
CS244 Final Project  
3/12/2013  
Dan Cocuzzo	<dcocuzzo@stanford.edu>  
Nick Shelly <nshelly@stanford.edu>
***

Traditionally, it has been a difficult for network operators to guarantee consistent policies to in-flight packets during configuration transitions, leading to potentially insecure or undefined network behavior during the transition period. It is possible that the transition process briefly allows propagation of malicious traffic, causes packets to be dropped, or incurs bandwidth degradation. For example, a flow of packets through a network would be disrupted during the transition if one switch using an older configuration forwarded packets to another switch with a conflicting, newer configuration.

Here we reproduce the results originally published in M. Reitblatt et al. "Abstractions for Network Update" [^1] presented at SIGCOMM'12. The results table summarizes many experiments, reporting the number of modified switch rules, or operations (Ops), and maximum switch overhead for each individual run. In addition, we investigate the number of required update operations over a range of network sizes to examine the scalability of this framework. The results can be found in the accompanying text files and plots.
<br><br>

This work is part of [CS244 Advanced Topics in Networking](http://www.stanford.edu/class/cs244/2013/) at Stanford University. This and other student projects can be found on the course blog, [Reproducing Network Research](http://reproducingnetworkresearch.wordpress.com/).
<br><br>
***************************************************

##Instructions to Replicate This Experiment:

1. Sign up for Amazon EC2

2. Create a new instance of the AMI on region US – West (Oregon) with ID “ami-xxxxxxxx″. (We recommend using a c1.medium or c1.xlarge instance for better performance.

3. SSH into this AMI using the ‘-A’ option to enable forwarding of the authentication agent connection. This will allow you to clone our Github repository from your instance.

4. In the home directory, run: git clone git://github.com/cocushio/cs244_pa3.git

5. Navigate into cs244_pa3/updates and run: sudo ./run.sh

6. Examine the produced .png images for the results. They are located in the generated “latency-<timestamp>-<experiment>” subdirectories.

###Additional Notes 
When troubleshooting, make sure to kill any rogue processes using the following commands:
  
	sudo ps -ef  
	sudo killall ofdatapath 
	sudo killall ofprotocol
	sudo killall python

###Sample Experiment Output:

| Switch | (+) | (-) | (~) | Total| Overhead |
|:------:|:---:|:---:|:---:|:----:|:--------:|
|  s101  | 550 | 390 |  0  | 940  |    42%   |
|  s102  | 426 | 294 |  0  | 720  |    62%   |
|  s103  | 580 | 420 |  0  | 1000 |    48%   |
|  s104  | 550 | 390 |  0  | 940  |    42%   |
|  s105  | 742 | 522 |  0  | 1264 |    97%   |
|  s106  | 182 | 132 |  0  | 314  |   100%   |
|  Total | 3030| 2148|  0  | 3030 |   100%   |

[^1]: M. Reitblatt et al. "Abstractions for Network Update" in SIGCOMM'12, Copyright 2012 ACM. doi: 978-1-4503-1419-0/12/08 
