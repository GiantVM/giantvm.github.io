
## GiantVM

![https://github.com/GiantVM/homepage/blob/master/images/arch.png](https://github.com/GiantVM/homepage/blob/master/images/arch.png)

GiantVM is a distributed hypervisor that aggregates resources from multiple physical machines, providing the guest OS with a uniform hardware abstraction. A QEMU-KVM instance runs on each node of a cluster.

This work is supported by the National Key Research & Development Program of China 2016YFB1000502.

### About distributed QEMU
In QEMU-KVM virtualization, QEMU simluates guest or device I/O requests and interrupts by interception. GiantVM is equipped IPI forwarding, interrupt forwarding and I/O forwarding techniques, which overcome the difficulties of sharing CPU and I/O devices across machines.

### About distributed KVM
KVM manages memory virtualization. At the heart of GiantVM is a distributed shared memory (DSM) based on [Ivy](https://dl.acm.org/citation.cfm?id=10610), which enables the sharing of memory across multiple machines. GiantVM implements various techniques to overcome the challenges of integrating the DSM into virtualization environments.

### Code

#### QEMU
BASE QEMU branch stable-2.8

[https://github.com/GiantVM/QEMU.git](https://github.com/GiantVM/QEMU.git) (To be uploaded)


#### KVM
BASE Linux Kernel branch 4.8.10

[https://github.com/GiantVM/Linux-DSM.git](https://github.com/GiantVM/Linux-DSM.git) (To be uploaded)

#### sv6
BASE [https://github.com/aclements/sv6](https://github.com/aclements/sv6)

[https://github.com/GiantVM/sv6.git](https://github.com/GiantVM/sv6.git) (To be uploaded)


### Command line

For example, run sv6 OS in GiantVM on two machines:

1. On machine 1 (ip 10.0.0.2), run:

    ```
    sudo qemu-system-x86_64 -smp 2 -m 20480 -machine q35,kernel-irqchip=off -serial mon:stdio -nographic -net user -net nic,model=e1000 -device ahci,id=ahci0 -drive if=none,file=o.qemu/fs.img,format=raw,id=drive-sata0-0-0 -device ide-drive,bus=ahci0.0,drive=drive-sata0-0-0,id=sata0-0-0 -kernel o.qemu/kernel.elf --enable-kvm -local-cpu 16,start=0,iplist="10.0.0.1 10.0.0.2"
    ```

2. On machine 0 (ip 10.0.0.1), run:

    ```
    sudo qemu-system-x86_64 -smp 2 -m 20480 -machine q35,kernel-irqchip=off -serial mon:stdio -nographic -net user -net nic,model=e1000 -device ahci,id=ahci0 -drive if=none,file=o.qemu/fs.img,format=raw,id=drive-sata0-0-0 -device ide-drive,bus=ahci0.0,drive=drive-sata0-0-0,id=sata0-0-0 -kernel o.qemu/kernel.elf --enable-kvm -local-cpu 16,start=16,iplist="10.0.0.1 10.0.0.2"
    ```

3. Wait for guest OS booting

### Publication

<a href ="https://doi.org/10.1145/3381052.3381324">GiantVM: A Type-II Hypervisor Implementing Many-to-one Virtualization</a>


Jin Zhang, Zhuocheng Ding, Yubin Chen, Xingguo Jia, Boshi Yu, Zhengwei Qi, Haibing Guan

VEE '20: Proceedings of the 16th ACM SIGPLAN/SIGOPS International Conference on Virtual Execution Environments
· March 2020 · Pages 30–44
                        

### Demo

[kvm_forum_v4.mp4](video/kvm_forum_v4.mp4)

### Slides
[Distributed QEMU](slides/giantvm-turing.pdf) - KVM forum 2018

### About Us
#### [Trusted Cloud Group](http://tcloud.sjtu.edu.cn/), Shanghai Jiaotong University
Zhengwei Qi \<[qizhwei@sjtu.edu.cn](mailto:qizhwei@sjtu.edu.cn)\>

Zhuocheng Ding \<[tcbbd@sjtu.edu.cn](mailto:tcbbd@sjtu.edu.cn)\>

Yubin Chen \<[binsschen@sjtu.edu.cn](mailto:binsschen@sjtu.edu.cn)\>

Jin Zhang \<[jzhang3002@sjtu.edu.cn](mailto:jzhang3002@sjtu.edu.cn)\>

Yun Wang \<[yunwang94@sjtu.edu.cn](mailto:yunwang94@sjtu.edu.cn)\>

Jiacheng Ma \<[jcma@umich.edu](mailto:jcma@umich.edu)\>

Boshi Yu \<[201608ybs@sjtu.edu.cn](mailto:201608ybs@sjtu.edu.cn)>

Xingguo Jia \<[jiaxg1998@sjtu.edu.cn](mailto:jiaxg1998@sjtu.edu.cn)>

Weiye Chen \<[](mailto:)>

Chenggang Wu \<[](mailto:)>

Yuxin Xiang \<[xiangyuxin@sjtu.edu.cn](mailto:xiangyuxin@sjtu.edu.cn)\>