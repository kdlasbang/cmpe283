# CMPE283-assignment3
## Group Member
### just myself Weibang He 014630603

## Implement Method->
### Continue with assignment2 (https://github.com/kdlasbang/cmpe283-assignment2)
### Clone this repo
### replace the new vmx.c with linux/arch/x86/kvm/vmx/vmx.c
### replace the new cpuid.c with linux/arch/x86/kvm/cpuid.c
### Rebuild the kernal as assignment 2 ->
### #sudo bash
### make -j 3 modules && make -j 3 && sudo make modules_install && sudo make install
### reboot and test in the nested VM

## Modification and Test Result
0x4FFFFFFE, if %ecx (on input) contains a value not defined by the SDM, return 0 in all %eax, %ebx, %ecx registers and return 0xFFFFFFFF in %edx. 

For exit types not enabled in KVM, return 0s in all four registers

cpuid.c->
![](https://github.com/kdlasbang/cmpe283/blob/main/assignment3/%E6%88%AA%E5%B1%8F2021-05-06%E4%B8%8B%E5%8D%881.30.15.png)

Count the time for all exit relate to KVM

### Result->

document here-> first attempt-> https://github.com/kdlasbang/cmpe283/blob/main/assignment3/output.txt

   second attempt -> https://github.com/kdlasbang/cmpe283/blob/main/assignment3/output2.txt

![](https://github.com/kdlasbang/cmpe283/blob/main/assignment3/IMG_6154.jpg)
![](https://github.com/kdlasbang/cmpe283/blob/main/assignment3/IMG_6155.jpg)
![](https://github.com/kdlasbang/cmpe283/blob/main/assignment3/IMG_6156.jpg)
![](https://github.com/kdlasbang/cmpe283/blob/main/assignment3/IMG_6157.jpg)

## Response to question ->
### Comment on the frequency of exits – 1. does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail? 2.Of the exit types defined in the SDM, which are the most frequent? Least? 

#### 1. No, the number of exits do not increase at a stable rate, as some exit increase a lot while some are not. It depends on their exit reason. For example, in the output 1 and 2, exit number 0 and 10 do not have much increase. While exit number 32 and 48 increase a lot in the second output. Between first attempt and the second attempt, what I have done is only run the ./a.out file on terminal. Thus I/O instruction would have more exit perform. Approximately 750000 exits in a full VM boot entail. 

#### 2. The most frequent type:WRMSR, cpuid, I/O instrcution, WRMSR and the least type is MOV DR
