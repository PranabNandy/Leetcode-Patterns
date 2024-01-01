#include <linux/init.h>
#include <linux/module.h>
#include <linux/kernel.h>
#include <linux/printk.h>
#include <linux/fs.h>
#include <linux/string.h>
#include <linux/uaccess.h>


MODULE_AUTHOR("pranab");
MODULE_LICENSE("GPL");
MODULE_DESCRIPTION("my_first_module");
MODULE_VERSION("1.0.0");


static char kern_buf[100];
ssize_t simple_write (struct file *file, const char __user *buf, size_t len, loff_t *off);
ssize_t simple_read (struct file *file, char __user *buf, size_t len, loff_t *off);
int simple_open (struct inode *inode, struct file *file);
int simple_release (struct inode *inode, struct file *file);
static const struct file_operations file_ops= {    // for the register driver file operation mentioned                      
        .owner = THIS_MODULE,    
        .open = simple_open,   // respective file operation for "cat /dev/driver3_pranab_nandy"
	.release =  simple_release, 
        .read = simple_read,                                    
        .write = simple_write,                       
};


static int  __init entry_function(void){
	int t=register_chrdev(199,"foo_pranab_nandy",&file_ops); // we have to register a driver to /proc/devices
	if(t<0){
		printk(KERN_ERR "Fail to register the device driver(Charecter Driver)");
		return EIO;
	}
	printk("hello Driver 3 init function\n");
	return 0;
}



ssize_t simple_write (struct file *file, const char __user *user_space_buf, size_t len, loff_t *off){
	printk("write Driver 3 \n");
	if(len>sizeof(kern_buf))
		return EIO;
	memset(kern_buf,0,sizeof(kern_buf));
	copy_from_user(kern_buf,user_space_buf,len);
	kern_buf[len]=0;
	return (ssize_t)len;
}

ssize_t simple_read (struct file *file, char __user *user_space_buf, size_t len, loff_t *off){
	printk("Read Driver 3 \n");
	if(*off>sizeof(kern_buf))
		return 0;
	if(len>sizeof(kern_buf))
		len=sizeof(kern_buf);
	copy_to_user(user_space_buf,kern_buf,len);
	return (ssize_t)len;

}
int simple_open (struct inode *inode, struct file *file){
 	printk(KERN_ERR "OPEN Driver 3 \n");
	return 0;
}
int simple_release (struct inode *inode, struct file *file){
	printk(KERN_INFO "RELEASE Driver 3 \n");
	return 0;
}


static void __exit exit_function(void){
	printk("bye bye Driver 3 function\n");
	unregister_chrdev(199,"foo_pranab_nandy"); // we have to register a driver to /proc/devices
	
}



module_init(entry_function);
module_exit(exit_function);



// --------------------------------------------------------------------
/* command */
// sudo make -C /usr/src/linux-headers-5.15.0-76-generic/ M=/home/pranab/Linux_kernel/
// sudo insmod driver3.ko
// sudo rmmod driver3.ko
// cat /dev/driver3_pranab_nandy  // sudo mknod /dev/driver3_pranab_nandy c 199 1
// cat /proc/devices    // check "199 foo_pranab_nandy"
// sudo dmesg -c 
// sudo tail -f /var/log/syslog/   // system log information
//ls /sys/module/    //lsmod
//cat /proc/modules/driver3    //status of the module
// grep driver3 /proc/kallsyms      // kernel symbol for driver3

//----- some imporant header files are
// /include/linux/kern_levels.h 
// /include/linux//printk.h  
// /include/linux//fs.h  


//------------ extra command
// cat /proc/sys/kernel/printk     // log level of console driver and printk 
// strace hello.out
// uname -r
//sudo apt-get install linux-kernel-headers


// --------- Important for linux
// https://elixir.bootlin.com/linux/latest/source

// git commit -s -v


// ---- To fix linux driver compilation issue
// sudo apt install --reinstall linux-headers-$(uname -r)






To
The Officer-in-Charge
Liluah Police Station
Howrah

	Subject: Loss of LIC Policy Document
	
Respected Sir/ Ma'am,
	with due respect, I want to inform you that I am ARCHANA PATRA, a permanent resident of KONA NASKAR PARA,
HOWRAH-711114. My Husband, Late BANAMALI PATRA had a LIC policy having Policy Number : 439 572 386. I lost my 
husband on 26/11/2023. Before that my husband lost the main LIC Policy Document in Kona Bazar on 10/10/2023. I 
am writing to formally report the loss of my LIC Policy document and seek your guidance and assistance in 
addressing this matter promptly.

The relevant details of the lost policy document are as follows:
Policyholder Name: BANAMALI PATRA
LIC Policy Number: 439 572 386

I have taken immediate measures to report this loss, and I am reaching out to request your guidance on the 
necessary steps and procedures to follow in order to obtain a duplicate copy of the policy document. Additionally,
I would appreciate any advice or documentation requirements that may expedite this process.

Thank you.

									Sincerely,
Date: 1/1/2024								__________________
									