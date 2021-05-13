# Assignment4
## Group member Weibang He 014630603 Just myself

1.Run your assignment 3 code and boot a test VM using that code. 

2.Once the VM has booted, record total exit count information (total count for each type of exit handled by KVM). You should do this via a sequence of queries of CPUID leaf function 0x4FFFFFFE.

3.Shutdown your test (inner) VM. 

4.Remove the ‘kvm-intel’ module from your running kernel: ◦rmmod kvm-intel 

5.Reload the kvm-intel module with the parameter ept=0 (this will disable nested paging and force KVM to use shadow paging instead)◦The module you want is usually found in /lib/modules/XXX/kernel/arch/x86/kvm  , where XXX is the version of the kernel you build for assignment 3 – don’t make a mistake and use the one that came with the stock Linux installation.◦insmod  /lib/modules/XXX/kernel/arch/x86/kvm/kvm-intel.ko ept=0
![](https://github.com/kdlasbang/cmpe283/blob/main/assignment4/IMG_6147.jpg)

6.Boot the same test VM again, and capture the same output as you did in step 2. 

## 7.Answer the questions below. 

 ## 2.Include a sample of your print of exit count output from dmesg from “with ept” and “without ept”. 
 ### with ept: (https://github.com/kdlasbang/cmpe283/blob/main/assignment4/nested.txt)
 
 ![](https://github.com/kdlasbang/cmpe283/blob/main/assignment4/IMG_6154.jpg)
 ![](https://github.com/kdlasbang/cmpe283/blob/main/assignment4/IMG_6155.jpg)
 ![](https://github.com/kdlasbang/cmpe283/blob/main/assignment4/IMG_6156.jpg)

 
 ### without ept:(https://github.com/kdlasbang/cmpe283/blob/main/assignment4/shadow.txt)
  ![](https://github.com/kdlasbang/cmpe283/blob/main/assignment4/IMG_6158.jpg)
  ![](https://github.com/kdlasbang/cmpe283/blob/main/assignment4/IMG_6159.jpg)
  ![](https://github.com/kdlasbang/cmpe283/blob/main/assignment4/IMG_6160.jpg)
 
 
 ## 3.What did you learn from the count of exits? Was the count what you expected? If not, why not? 

The count with ept is much less than the count without ept. And the count is what I expected. The count with ept is counting the exit in nested paging, and the count without ept is counting the shadow paging. The shadow paging expect more exit than the nested paging.  
 
In nested paging, it has more memory locations need to be accessed and has fewer number of exits. 

While in shadow paging, CR3 exits, Page Fault Exits and TLB Flush exits are ensure to be executed. Thus, shadow paging should have more counts of exits than the nested paging. 

 
 ## 4.What changed between the two runs (ept vs no-ept)?
 
The count of exits in no-ept(shadow paging) one obviously larger than in ept(nested paging) one. 
 
 
