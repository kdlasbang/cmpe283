# CMPE283-assignment3
## Group Member
### just myself Weibang He 014630603

## Implement Method->
### Continue with assignment2 (https://github.com/kdlasbang/cmpe283-assignment2)
### Clone this repo
### replace the new vmx.c with linux/arch/x86/kvm/vmx/vmx.c
### replace the new cpuid.c with linux/arch/x86/kvm/cpuid.c
### Rebuild the kernal as assignment 2 ->
### Pro way to rebuild->(as we only modify the file inside kvm filedir)
### sudo rmmod kvm_intel
### sudo rmmod kvm
### sudo make -j 3 modules M=arch/x86/kvm
### sudo insmod arch/x86/kvm/kvm.ko
### sudo insmod arch/x86/kvm/kvm-intel.ko
### normal way to rebuild -> [#sudo bash
### make -j 3 modules && make -j 3 && sudo make modules_install && sudo make install]
### reboot and test in the nested VM

## Modification and Test Result
0x4FFFFFFE, if %ecx (on input) contains a value not defined by the SDM, return 0 in all %eax, %ebx, %ecx registers and return 0xFFFFFFFF in %edx. 

For exit types not enabled in KVM, return 0s in all four registers

cpuid.c->
![](https://github.com/kdlasbang/cmpe283/blob/main/assignment3/%E6%88%AA%E5%B1%8F2021-05-06%E4%B8%8B%E5%8D%881.30.15.png)

Count the time for all exit relate to KVM

### Result->
![](https://github.com/kdlasbang/cmpe283/blob/main/assignment3/IMG_6073.jpg)
![](https://github.com/kdlasbang/cmpe283/blob/main/assignment3/IMG_6074.jpg)
![](https://github.com/kdlasbang/cmpe283/blob/main/assignment3/IMG_6075.jpg)
![](https://github.com/kdlasbang/cmpe283/blob/main/assignment3/IMG_6076.jpg)

## Response to question ->
### Comment on the frequency of exits – 1. does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail? 2.Of the exit types defined in the SDM, which are the most frequent? Least? 

#### 1. Yes. I tried twice. There is no difference between the first one and the second one.  The approximate exit number is 300.
#### 2. The most frequent type is External interrupt, WRMSR and the least type is MOV DR
