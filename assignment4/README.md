# Assignment4
## Group member Weibang He 014630603 Just myself

1.Run your assignment 3 code and boot a test VM using that code. 

2.Once the VM has booted, record total exit count information (total count for each type of exit handled by KVM). You should do this via a sequence of queries of CPUID leaf function 0x4FFFFFFE.
 ![](https://github.com/kdlasbang/cmpe283/blob/main/assignment3/IMG_6074.jpg)

3.Shutdown your test (inner) VM. 

4.Remove the ‘kvm-intel’ module from your running kernel: ◦rmmod kvm-intel 

5.Reload the kvm-intel module with the parameter ept=0 (this will disable nested paging and force KVM to use shadow paging instead)◦The module you want is usually found in /lib/modules/XXX/kernel/arch/x86/kvm  , where XXX is the version of the kernel you build for assignment 3 – don’t make a mistake and use the one that came with the stock Linux installation.◦insmod  /lib/modules/XXX/kernel/arch/x86/kvm/kvm-intel.ko ept=0
![](https://github.com/kdlasbang/cmpe283/blob/main/assignment4/IMG_6147.jpg)

6.Boot the same test VM again, and capture the same output as you did in step 2. 

## 7.Answer the questions below. 

 ## 2.Include a sample of your print of exit count output from dmesg from “with ept” and “without ept”. 
 with ept:
 
 ![](https://github.com/kdlasbang/cmpe283/blob/main/assignment3/IMG_6074.jpg)
 
 without ept:
 
 ![](https://github.com/kdlasbang/cmpe283/blob/main/assignment4/IMG_6150.jpg)
 
 
 ## 3.What did you learn from the count of exits? Was the count what you expected? If not, why not? 

No as my expected. The shadow paging should expected more exit than the nested paging. While they are the same. It is very wierd for my case. 
 
 Because in nested paging, nested table would have more memory locations to be accessed and the number of exits should be minimized. 

While in shadow paging, we need to enable the TLB refresh exit function, to solve the problem of memory release and let the shadow table can be synchronized and updated. Thus shadow paging should have more number of exits than the nested one.

 For my case, I think there is some problem about building the kernel with assignment 3 's code, or maybe some hardware or system configuration issue. I have tried too many attempts, and the result still the same. 
 
 ## 4.What changed between the two runs (ept vs no-ept)?
 
 Just go through my result there, there is no difference between ept and no-ept here. Just that when I run the no-ept version, the nested VM report a system problem.  
 
 
