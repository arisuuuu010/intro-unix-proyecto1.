1.**What is LUKS and what is its relationship to dm-crypt in the Linux kernel? Explain the role of the device mapper in the encryption process.**
When we want to store highly confidential information on a disk in Debian, what we should do is use LUKS, which helps us encrypt the information; that is, it helps us log in when we want to access the information on the disk. 
When we did the activity, we create a password, then put the password and you can watch the information that you have in your disk:
Here we have the password with 100 entropy bytes:
_YtkB$1IqGg9hV=+Hvvp
According to SYSDEV LABORATORIES (s.f) “LUKS (Linux Unified Key Setup) is by far the most common block device encryption method used on various Linux-based systems. It is completely open source, operates at the kernel level, and employs the device mapper subsystem via the dm-crypt module.”
Dm-crypt is a encrypt mechanics in the linux kernel, it helps to mount encrypt files and give the information when we need it 
According to Wikipedia (2024) “dm-crypt is implemented as a device mapper target and may be stacked on top of other device mapper transformations. It can thus encrypt whole disks (including removable media), partitions, software RAID volumes, logical volumes, as well as files.” , dm-crypt works with device mapper, device mapper helps to create virtual disks and it represents with dev/mapper.
According to Wikipedia (2024) “The device mapper is a framework provided by the Linux kernel for mapping physical block devices onto higher-level virtual block devices. It forms the foundation of the logical volume manager (LVM), software RAIDs and dm-crypt disk encryption, and offers additional features such as file system snapshots.” So the relationship between dm-crypt and LUKS it give more security to the user, because dm-crypt helps create crypt files to have information and luks put a password in the disk, in this way luks and dm-crypt, give more security and give you all the information that you need.
2. **What is the difference between full disk encryption (FDE) and filesystem-level encryption? Mention two advantages and two limitations of each.**
What is FDE?
According to Pure Storage (s.f) “Full disk encryption (FDE), commonly known as full disk encryption, is a security measure used to protect private data from unauthorized access. This technology addresses widespread threats while ensuring that all data stored on a device's hard drive is encrypted.
Once implemented on a computer system, it automatically encrypts all information on the drive. This includes system metadata, the operating system, configuration files, and even temporary files. This process converts all this vital information into complex algorithms that can only be decrypted with the correct key.”
So FDE do the full encryption around all the disk, when FDE create de encrypt, FDE mount all the information about the disk, such as, files, inodos, blocks and all the metadata that we have in the disk. 
All the information that we see in the questions like luks, or dm-encrypt are part of cybersecurity, it means everything encrypt need a password for sign in in the disk, it helps to the security and give
What is filesystem-level encryption?
How the name said “files encryption”, each file will be encrypted when we do this, we have a password that help us to decrypt the file, the file is in binary and random characters.
According to Everpure (s.f) “With file-level encryption, also known as file-based encryption or filesystem-level encryption, individual files and folders stored on a local device or network storage may be encrypted without needing to encrypt the entire storage medium itself. Encrypted files look like a long string of random characters, but the key used to encrypt files will translate the characters to the file’s original state.”
	FDE	FDI
**Advantages of FDE** Complete disk security.
Save all the information in the disk.
Protection Against Physical Theft
**Adventages of FDI**If you can encrypt each file, or customize each file with security you can use FDI, each file will be encrypted in binary and Different users can have different keys. User A cannot decrypt User B’s files even if the system is running and User A is logged in.
**1 limitation of FDE**	You can not customize each disk o file, is all the information or nothing.	
**2 limitation of FDE**	It requires user intervention (entering a passphrase) before the OS can even start, which can be problematic for remote servers that need to reboot automatically.
**1Limitation of FDI** While file contents are encrypted, some metadata (like file sizes, number of files, and sometimes directory structures) may remain visible to an attacker with physical access.	
**2 limitation of FDI** It does not protect system-wide temporary files (/tmp) or swap space (SWAP) unless those specific areas are also manually configured for encryption.
3. **What is LVM and what are its three layers of abstraction (PV, VG, LV)? What advantages does LVM offer over traditional partitioning in a server environment?**
LVM (Logical Volume management) in linux is a logical volume management that provides mass storage in the devices. Also is a device mapper framework, new linux distributions are LVM-aware.
According to Wikipedia (2024) “ LVM is used for the following purposes:
•	Creating single logical volumes of multiple physical volumes or entire hard disks (somewhat similar to RAID 0, but more similar to JBOD), allowing for dynamic volume resizing.
•	Managing large hard disk farms by allowing disks to be added and replaced without downtime or service disruption, in combination with hot swapping.”, LVM works between physical disk and the filesystem, its divided into three parts:
PV: Here we have the physical disk such as, ssd, hdd and nmve, when we want LVM the main step is having a physical disk with a good storage 
VG: Volume group, here we have more PVs like a pool storage, we can use it in a server because servers have some PV for the information and VG helps to create a single VG, example:
The VG allows the operating system to see not 5 separate 1TB disks, but a single 5TB space.

LV: Logical Volume, is the virtual partition that is created from the available space in a Volume Group (VG). The filesystems standards like EXT4 and XFS could be created in logical volume.
When the servers use LVM get advantages because servers need more organization and the ttraditional partitions are confined to the boundaries of a single physical disk. If you have two 500GB drives, you are stuck with two separate 500GB mount points. LVM allow to create backups in the disk that you want, is better for the factories that get much information.
4. **Explain what happens during the boot process of a system with LUKS+LVM: at what point is the decryption password requested and what role does GRUB play in this process?**
Initially, when we load LUKS+LVM, the boot process starts, which is where we have the UEFI or BIOS. However, we need to know something: in Linux, GRUB according to Lenovo (2020) “GRUB (Grand Unified Bootloader) is a widely used boot loader in the Linux® world. It's the initial program that kicks into action when you power on your computer, responsible for loading the operating system kernel into memory.”  
Starts first, which loads the Linux kernel. After that, initram starts, which helps us have the drivers ready for system execution. It will ask for the key to our encrypted disk to give us the necessary information. After that, LVM starts, which helps find the logical volumes like root or home. Finally, everything is mounted, and we have our decrypted information ready.
