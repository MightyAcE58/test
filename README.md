# Linux Administration Practicals

---

## Practical 1: Basic Linux Commands — Calendar, Date, Calculator, Users, and File Operations

### 1.1 Calendar Commands

```bash
# Display current month calendar
ncal

# Display calendar for the year 2011
ncal 2011

# Display calendar for July 1998
ncal 7 1998

# Display calendars from 1990 to 2000
for year in {1990..2000}; do cal $year; done

# Display previous, current, and next month
ncal -3

# Display calendar with week numbers
ncal -w

# Display current month vertically (ncal format)
ncal

# Convert ncal output back to traditional cal format
ncal -C

# Display calendar in Julian format
ncal -j
```

### 1.2 Date and Time Commands

```bash
# Display today's date
date

# Display date in mm-dd-yy format
date +"%m-%d-%y"

# Display current time in HH:MM:SS format
date +"%H:%M:%S"

# Display day of the week (full name)
date +"%A"

# Display first 3 letters of the weekday
date +"%a"

# Display first 3 letters of the month
date +"%b"

# Display last 2 digits of the year
date +"%y"

# Display time in AM/PM format
date +"%r"
```

### 1.3 Basic Calculator (bc)

```bash
# Launch the basic calculator
bc

# Inside bc:
# 6+7
# 12*12
# 144/3
# (8+2)*5
# (2+3)*8.4*(6-3)
# 2^3
# Convert decimal to binary: obase=2; 144
# Convert binary to decimal: ibase=2; 11001010
# Type 'quit' to exit
```

### 1.4 User Information Commands

```bash
# Display all currently logged-in users
who

# Display logged-in users with headers
who -H

# Display the current user
whoami

# Display quick list of usernames and total count
who -q

# Display idle time of each user
who -u

# Display current system run level
who -r

# Display date and time of last system boot
who -b
```

### 1.5 File and Directory Operations

```bash
# Create 3 files using cat
cat > A1
# (type content, press Ctrl+D to save)
cat > B2
cat > C3

# List all files
ls

# Display contents of files
cat A1
cat B2
cat C3

# Display file contents with line numbers
cat -n A1
cat -n B2
cat -n C3

# Copy file contents
cp A1 B4
cp B2 E5

# Concatenate contents of A1, B2, C3 into a single file
cat A1 B2 C3 > combined.txt

# Create directories
mkdir dd1 dd2

# Copy files to dd1 and list
cp A1 B2 dd1/
ls dd1

# Copy files to dd2, list, then remove dd2
cp C3 B4 dd2/
ls dd2
rm -r dd2
```

---

## Practical 2: User Management, Group Management, Permissions, and Basic Shell Scripts

### 2.1 User and Group Management

```bash
# Create a new user
sudo adduser newuser

# Set/change password for user
sudo passwd newuser

# Create a new group
sudo groupadd newgroup

# Add user to group
sudo usermod -aG newgroup newuser

# Display all users
cat /etc/passwd

# Display all groups
cat /etc/group
```

### 2.2 File Ownership and Permissions

```bash
# Create a file
touch myfile.txt

# Change ownership of the file
sudo chown newuser myfile.txt

# Change group ownership of the file
sudo chgrp newgroup myfile.txt

# Display file ownership and permissions
ls -l myfile.txt

# Set file to read-only for all users (absolute method)
chmod 444 myfile.txt

# Give execute permission to owner only
chmod u+x myfile.txt

# Remove write permission from group
chmod g-w myfile.txt

# Set owner=rwx, group=rx, others=r (absolute method)
chmod 754 myfile.txt
```

### 2.3 Shell Script — Compare Number with 10

```bash
nano num.sh
```

```sh
#!/bin/bash
echo "Enter a number:"
read num1

if [ "$num1" -gt 10 ]; then
    echo "$num1 is greater than 10"
else
    echo "10 is greater than $num1"
fi
```

```bash
chmod +x num.sh
./num.sh
```

### 2.4 Shell Script — Positive or Negative

```sh
#!/bin/bash
echo "Enter a number:"
read num

if [ "$num" -gt 0 ]; then
    echo "$num is Positive"
elif [ "$num" -lt 0 ]; then
    echo "$num is Negative"
else
    echo "The number is Zero"
fi
```

### 2.5 Shell Script — Even or Odd

```sh
#!/bin/bash
echo "Enter a number:"
read num

if [ $((num % 2)) -eq 0 ]; then
    echo "The number is Even"
else
    echo "The number is Odd"
fi
```

### 2.6 Shell Script — Maximum of Two Numbers

```sh
#!/bin/bash
echo "Enter number 1:"
read a
echo "Enter number 2:"
read b

if [ "$a" -gt "$b" ]; then
    echo "$a is greater"
else
    echo "$b is greater"
fi
```

---

## Practical 3: Shell Scripting — Conditions and Case Statements

### 3.1 Smallest of Three Numbers (Logical Operators)

```sh
#!/bin/bash
echo "Enter first number:"
read a
echo "Enter second number:"
read b
echo "Enter third number:"
read c

if [ "$a" -le "$b" ] && [ "$a" -le "$c" ]; then
    echo "$a is the smallest number"
elif [ "$b" -le "$a" ] && [ "$b" -le "$c" ]; then
    echo "$b is the smallest number"
else
    echo "$c is the smallest number"
fi
```

### 3.2 Maximum of Three Numbers (Logical Operators)

```sh
#!/bin/bash
echo "Enter three numbers:"
read a
read b
read c

if [ "$a" -ge "$b" ] && [ "$a" -ge "$c" ]; then
    echo "Maximum number is: $a"
elif [ "$b" -ge "$a" ] && [ "$b" -ge "$c" ]; then
    echo "Maximum number is: $b"
else
    echo "Maximum number is: $c"
fi
```

### 3.3 Grade Calculator (5 Subjects)

```sh
#!/bin/bash
echo "Enter marks of 5 subjects (out of 100):"
read -p "Subject 1: " m1
read -p "Subject 2: " m2
read -p "Subject 3: " m3
read -p "Subject 4: " m4
read -p "Subject 5: " m5

total=$((m1 + m2 + m3 + m4 + m5))
percentage=$((total / 5))

echo "Total Marks: $total"
echo "Percentage: $percentage%"

if [ "$percentage" -lt 35 ]; then
    echo "Grade: FAIL"
elif [ "$percentage" -ge 35 ] && [ "$percentage" -lt 45 ]; then
    echo "Grade: C"
elif [ "$percentage" -ge 45 ] && [ "$percentage" -lt 60 ]; then
    echo "Grade: B"
elif [ "$percentage" -ge 60 ] && [ "$percentage" -lt 75 ]; then
    echo "Grade: A"
elif [ "$percentage" -ge 75 ] && [ "$percentage" -le 100 ]; then
    echo "Grade: O"
else
    echo "Invalid Marks Entered"
fi
```

### 3.4 Day Name from Number (Case Statement)

```sh
#!/bin/bash
echo "Enter a number (1-7):"
read num

case $num in
    1) echo "Monday" ;;
    2) echo "Tuesday" ;;
    3) echo "Wednesday" ;;
    4) echo "Thursday" ;;
    5) echo "Friday" ;;
    6) echo "Saturday" ;;
    7) echo "Sunday" ;;
    *) echo "Invalid input! Enter a number between 1 and 7." ;;
esac
```

### 3.5 Character Type Checker

```sh
#!/bin/bash
echo "Enter a single character:"
read ch

case "$ch" in
    [a-z]) echo "The character is a lowercase letter" ;;
    [A-Z]) echo "The character is an uppercase letter" ;;
    [0-9]) echo "The character is a digit" ;;
    *)     echo "The character is a special character" ;;
esac
```

### 3.6 Menu-Driven Program

```sh
#!/bin/bash
while true; do
    echo ""
    echo "1. Create a file named demo"
    echo "2. Display present working directory"
    echo "3. List all files including hidden files"
    echo "4. Display contents of demo file"
    echo "5. Exit"
    echo "Enter your choice:"
    read choice

    case $choice in
        1)
            echo "Enter content for demo file:"
            read data
            echo "$data" > demo
            echo "File 'demo' created successfully."
            ;;
        2)
            pwd
            ;;
        3)
            ls -a
            ;;
        4)
            if [ -f demo ]; then
                cat demo
            else
                echo "File 'demo' does not exist."
            fi
            ;;
        5)
            echo "Exiting..."
            exit 0
            ;;
        *)
            echo "Invalid choice!"
            ;;
    esac
done
```

---

## Practical 4: Loops, Factorial, and Fibonacci

### 4.1 First 5 Natural Numbers (While and For Loop)

```sh
#!/bin/bash

echo "Using while loop:"
i=1
while [ $i -le 5 ]; do
    echo $i
    i=$((i + 1))
done

echo ""
echo "Using for loop:"
for i in 1 2 3 4 5; do
    echo $i
done
```

### 4.2 Multiplication Table (While Loop)

```sh
#!/bin/bash
echo "Enter a number:"
read num

i=1
while [ $i -le 10 ]; do
    echo "$num x $i = $((num * i))"
    i=$((i + 1))
done
```

### 4.3 Sum of Squares of First 10 Numbers

```sh
#!/bin/bash
sum=0

for i in {1..10}; do
    square=$((i * i))
    echo "Square of $i = $square"
    sum=$((sum + square))
done

echo "---------------------------"
echo "Sum of squares = $sum"
```

### 4.4 Factorial of a Number

```sh
#!/bin/bash
echo "Enter a number:"
read num

fact=1
for ((i = 1; i <= num; i++)); do
    fact=$((fact * i))
done

echo "Factorial of $num is: $fact"
```

### 4.5 Power (x^y) Using Loop

```sh
#!/bin/bash
echo "Enter base (x):"
read x
echo "Enter exponent (y):"
read y

result=1
for ((i = 1; i <= y; i++)); do
    result=$((result * x))
done

echo "$x ^ $y = $result"
```

### 4.6 Menu-Driven: Positive/Negative Check with Factorial and Fibonacci

```sh
#!/bin/bash
echo "Enter a number:"
read number

if [ $number -gt 0 ]; then
    echo "The number $number is positive."
elif [ $number -lt 0 ]; then
    echo "The number $number is negative."
else
    echo "The number is zero."
fi

echo ""
echo "Choose an operation:"
echo "1. Fibonacci sequence"
echo "2. Factorial"
read choice

case $choice in
    1)
        a=0
        b=1
        echo "Fibonacci sequence up to $number terms:"
        for ((i = 0; i < number; i++)); do
            echo -n "$a "
            fn=$((a + b))
            a=$b
            b=$fn
        done
        echo
        ;;
    2)
        fact=1
        for ((i = 1; i <= number; i++)); do
            fact=$((fact * i))
        done
        echo "Factorial of $number is: $fact"
        ;;
    *)
        echo "Invalid choice."
        ;;
esac
```

---

## Practical 5: Links and Data Backup

### 5.1 Soft Link (Symbolic Link)

```bash
# Create a file
echo "Hello World" > original.txt

# Create a symbolic link
ln -s original.txt softlink.txt

# Verify
ls -l softlink.txt
cat softlink.txt
```

### 5.2 Hard Link

```bash
# Create a hard link
ln original.txt hardlink.txt

# Verify (both will share the same inode)
ls -li original.txt hardlink.txt
cat hardlink.txt
```

### 5.3 Compress Files Using tar

```bash
# Create a tar.gz archive
tar -czvf archive.tar.gz original.txt softlink.txt

# Verify
ls -l archive.tar.gz
```

### 5.4 Extract Files Using tar

```bash
# Extract the archive
tar -xzvf archive.tar.gz

# List contents without extracting
tar -tzvf archive.tar.gz
```

---

## Practical 6: SSH Server Configuration

### Objective

Configure an SSH server on Ubuntu and connect from a remote machine using PuTTY.

### Steps

```bash
# Update packages
sudo apt-get update

# Install OpenSSH server
sudo apt install openssh-server -y

# Start and enable SSH service
sudo systemctl start ssh
sudo systemctl enable ssh

# Verify SSH is running
sudo systemctl status ssh

# Check firewall status and allow SSH
sudo ufw status
sudo ufw allow ssh
sudo ufw enable

# Check SSH configuration for errors
sudo sshd -t

# View SSH log entries
journalctl -u ssh.service -n 50

# Find the server IP address
ip a
```

### Connect from Windows

1. Install PuTTY on the Windows machine.
2. Open PuTTY and enter the Ubuntu server's IP address (e.g., `192.168.112.141`).
3. Set port to `22` and connection type to `SSH`.
4. Click **Open** and log in with the Ubuntu username and password.

### tcpdump (Network Packet Capture)

```bash
# Install tcpdump
sudo apt install tcpdump -y

# Capture packets on default interface
sudo tcpdump

# Capture packets on a specific interface
sudo tcpdump -i eth0

# Capture and save to file
sudo tcpdump -w capture.pcap

# Read a capture file
sudo tcpdump -r capture.pcap
```

---

## Practical 7: FTP Server Configuration (vsftpd)

### Objective

Install and configure an FTP server using vsftpd on Ubuntu.

### Steps

```bash
# Update system packages
sudo apt update
sudo apt upgrade -y

# Install vsftpd
sudo apt install vsftpd -y

# Backup original configuration
sudo cp /etc/vsftpd.conf /etc/vsftpd.conf.backup

# Edit configuration
sudo nano /etc/vsftpd.conf
```

In the configuration file, ensure the following settings:

```
anonymous_enable=YES
local_enable=YES
write_enable=YES
```

```bash
# Create FTP directory and test file
sudo mkdir -p /srv/ftp/ftpdir
sudo touch /srv/ftp/ftpdir/first.txt

# Restart and verify the service
sudo systemctl restart vsftpd
sudo systemctl status vsftpd

# Create an FTP user
sudo adduser ftpuser
# (Set password when prompted)

# Optional: restrict user to FTP only
sudo usermod -s /usr/sbin/nologin ftpuser

# Configure firewall
sudo ufw allow 21/tcp
sudo ufw reload

# Find server IP
ip a

# Test FTP locally
ftp localhost
```

---

## Practical 8: Samba Server Configuration

### Objective

Install and configure Samba to share files between Ubuntu and Windows.

### Steps on Ubuntu

```bash
# Install Samba
sudo apt install samba -y

# Start and enable Samba
sudo systemctl start smbd
sudo systemctl enable smbd

# Check status
sudo systemctl status smbd

# Backup configuration
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.backup

# Create a Samba user and set password
sudo smbpasswd -a pratik

# Edit Samba configuration
sudo nano /etc/samba/smb.conf
```

Add the following at the end of `smb.conf`:

```
[pratik]
   path = /home/pratik
   read only = no
   browsable = yes
   guest ok = yes
   force user = pratik
```

```bash
# Restart Samba
sudo systemctl restart smbd
sudo systemctl status smbd

# Find IP address
ip a
```

### Access from Windows

1. Open **Windows Firewall Defender** and turn off all firewalls (for testing only).
2. Open **Control Panel > Network and Sharing Center**.
3. Click on **Ethernet > Properties > TCP/IPv4 > Advanced** and enable **NetBIOS over TCP/IP**.
4. Open **File Explorer**, right-click **This PC > Map network drive**.
5. Enter `\\<ubuntu-ip>\pratik` and log in with the Samba credentials.

---

## Practical 9: C Programming on Linux

### 9.1 Setup

```bash
sudo apt-get update
sudo apt-get install build-essential -y
gcc --version
```

### 9.2 Hello World

```c
// hello.c
#include <stdio.h>

int main() {
    printf("Hello World\n");
    return 0;
}
```

```bash
gcc hello.c -o hello
./hello
```

### 9.3 Arithmetic Operations

```c
// arithmetic.c
#include <stdio.h>

int main() {
    int a, b;
    printf("Enter two numbers: ");
    scanf("%d %d", &a, &b);

    printf("Addition: %d\n", a + b);
    printf("Subtraction: %d\n", a - b);
    printf("Multiplication: %d\n", a * b);
    printf("Division: %d\n", a / b);
    printf("Modulus: %d\n", a % b);
    return 0;
}
```

```bash
gcc arithmetic.c -o arithmetic
./arithmetic
```

### 9.4 Even or Odd

```c
// evenodd.c
#include <stdio.h>

int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);

    if (num % 2 == 0)
        printf("%d is Even\n", num);
    else
        printf("%d is Odd\n", num);
    return 0;
}
```

```bash
gcc evenodd.c -o evenodd
./evenodd
```

### 9.5 Largest of Three Numbers

```c
// largest.c
#include <stdio.h>

int main() {
    int a, b, c;
    printf("Enter three numbers: ");
    scanf("%d %d %d", &a, &b, &c);

    if (a >= b && a >= c)
        printf("Largest number = %d\n", a);
    else if (b >= a && b >= c)
        printf("Largest number = %d\n", b);
    else
        printf("Largest number = %d\n", c);
    return 0;
}
```

```bash
gcc largest.c -o largest
./largest
```

### 9.6 Positive, Negative, or Zero

```c
// posneg.c
#include <stdio.h>

int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);

    if (num > 0)
        printf("Number is Positive\n");
    else if (num < 0)
        printf("Number is Negative\n");
    else
        printf("Number is Zero\n");
    return 0;
}
```

```bash
gcc posneg.c -o posneg
./posneg
```

### 9.7 Character Type Checker

```c
// charcheck.c
#include <stdio.h>

int main() {
    char ch;
    printf("Enter a character: ");
    scanf(" %c", &ch);

    if (ch >= 'A' && ch <= 'Z')
        printf("Capital Letter\n");
    else if (ch >= 'a' && ch <= 'z')
        printf("Small Letter\n");
    else if (ch >= '0' && ch <= '9')
        printf("Digit\n");
    else
        printf("Special Symbol\n");
    return 0;
}
```

```bash
gcc charcheck.c -o charcheck
./charcheck
```

### 9.8 Multiplication Table (While Loop)

```c
// table.c
#include <stdio.h>

int main() {
    int num, i = 1;
    printf("Enter a number: ");
    scanf("%d", &num);

    while (i <= 10) {
        printf("%d x %d = %d\n", num, i, num * i);
        i++;
    }
    return 0;
}
```

```bash
gcc table.c -o table
./table
```

### 9.9 Palindrome Number

```c
// palindrome.c
#include <stdio.h>

int main() {
    int num, reversed = 0, remainder, original;
    printf("Enter a number: ");
    scanf("%d", &num);

    original = num;
    while (num != 0) {
        remainder = num % 10;
        reversed = reversed * 10 + remainder;
        num /= 10;
    }

    if (original == reversed)
        printf("%d is a Palindrome\n", original);
    else
        printf("%d is not a Palindrome\n", original);
    return 0;
}
```

```bash
gcc palindrome.c -o palindrome
./palindrome
```

### 9.10 Swap Two Numbers Without Third Variable

```c
// swap.c
#include <stdio.h>

int main() {
    int a, b;
    printf("Enter number 1: ");
    scanf("%d", &a);
    printf("Enter number 2: ");
    scanf("%d", &b);

    printf("Before swap: a = %d, b = %d\n", a, b);

    a = a + b;
    b = a - b;
    a = a - b;

    printf("After swap: a = %d, b = %d\n", a, b);
    return 0;
}
```

```bash
gcc swap.c -o swap
./swap
```

### 9.11 Even Numbers Between 10 and 50

```c
// evennums.c
#include <stdio.h>

int main() {
    for (int i = 10; i <= 50; i++) {
        if (i % 2 == 0)
            printf("%d\n", i);
    }
    return 0;
}
```

```bash
gcc evennums.c -o evennums
./evennums
```

---

## Practical 10: NFS Server Configuration

### Objective

Install and configure an NFS (Network File System) server to share files between two Ubuntu machines.

### Server Setup

```bash
# Update and install NFS server
sudo apt-get update
sudo apt install nfs-kernel-server -y

# Create shared directory and a test file
sudo mkdir -p /home/shared
echo "This is a shared file via NFS" | sudo tee /home/shared/file.txt
sudo chmod -R 755 /home/shared

# Configure NFS exports
sudo nano /etc/exports
```

Add the following line to `/etc/exports`:

```
/home/shared *(rw,sync,no_subtree_check)
```

```bash
# Apply export configuration and restart NFS
sudo exportfs -a
sudo systemctl restart nfs-kernel-server
```

### Client Setup

```bash
# Install NFS client utilities
sudo apt install nfs-common -y

# Create mount point and mount the NFS share
sudo mkdir -p /mnt/nfs_client
sudo mount <server-ip>:/home/shared /mnt/nfs_client

# Verify the mount
ls /mnt/nfs_client
cat /mnt/nfs_client/file.txt

# Check mounted NFS shares
df -h | grep nfs
```

Replace `<server-ip>` with the actual IP address of the NFS server.
