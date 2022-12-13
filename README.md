# SPCN-011
ขั้นตอนการใช้งานของสร้าง vm and ct on Proxmox cluster

1) Create master vm [ ubuntu-22.04 ]
   - สร้าง master vm มา 1 ตัว แล้วทำการ set ค่าพื้นฐานต่างๆ
   - เช็คเวลาด้วย dateและตset update time ด้วยคำสั่ง sudo timedatectl set-timezone Asia/Bangkok
   - ทำการเปิดใช้งาน ip qemu ด้วยคำสั่ง
       - sudo -i
       - apt update
       - apt install qemu-guest-agent
       - systemctl enable qemu-guest-agent
       - และทำการตั้งค่าที่ option ให้เปิดใช้งานตัว Qemu guest agent เป็น Enable 
        ![image](https://user-images.githubusercontent.com/117457958/207245641-40c1e992-fb5d-4e89-9abb-ed9f05b29cbf.png)
       - reboot เพื่อรีระบบ
   1.1) clone from template 2 vm
   - Click ที่ vm(master) > Convert to template
   -  หลังจาก vm(master) กลายเป็นtemplate ให้ Click vm แล้วเลือก Clone เป็นตัวvmใหม่2ตัว
      ![image](https://user-images.githubusercontent.com/117457958/207246162-80db51e3-06a4-4612-9ce4-f3f0d73dc0b9.png)
   - ทำการsetระบบโดย
        - date เพื่อเช็คtimezone
          ![image](https://user-images.githubusercontent.com/117457958/207246791-4c5e1549-ce47-4935-952b-6e9f3d2b3e4e.png)  
        - ทำการเปลี่ยนipของระบบเพื่อไม่ให้ipซ้ำกันโดย
            - sudo -i
            - rm /var/lib/dbus/machine-id
            - nano /etc/machine-id เพื่อลบ id เก่าออก
            - ln -s /etc/machine-id /var/lib/dbus/machine-id เพื่อ link เชื่อมต่อกับ machine-id
            - reboot เพื่อรี ip ใหม่
            - หลังเปลี่ยน ip clone1
              ![clone summary1](https://user-images.githubusercontent.com/119097660/206990489-4c7e5fdc-0ebc-4848-8097-9ff66c473168.png)
            - หลังเปลี่ยน ip clone2
              ![clone summary2](https://user-images.githubusercontent.com/119097660/206990515-facba323-a7f5-4538-9911-38dc16157b27.png)
 
2) create vm from other os
   - Create VM จากนั้นทำการตั้งค่าที่กำหนดโดยระบบปฏิบัติการที่เลือกใช้คือ Kali
      - Summary ของ Kali
        ![summary os other](https://user-images.githubusercontent.com/119097660/206990720-54d13749-d4e8-411a-8193-7eced674c558.png)
      - หน้า console screen
        ![watch screen other](https://user-images.githubusercontent.com/119097660/206990727-765816a0-5a64-4e54-b34d-ca6a22a91cd6.png)  

3) create vm from other os
   - Click create container template เพื่อสร้าง CT
      - Summary 
        ![summary ct](https://user-images.githubusercontent.com/119097660/206991056-5ab02e66-2cb3-4f75-b49c-8512e565e7f3.png)
      - console screen 
        ![watch screen  ct](https://user-images.githubusercontent.com/119097660/206991066-895b52ea-7bcc-41a7-a1da-aa7b5cf7c098.png)
