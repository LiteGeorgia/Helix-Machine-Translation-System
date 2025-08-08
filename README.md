# Helix Machine Translation System using Sampark

## About
Helix is a Machine Translation System developed by Calnic Solutions and incubated in TWFTW International to translate text for low digital resource languages Powari & Mehra among other languages of India. Its open system can be used to develop other language pairs by incorporating language specific database. Tested on the available corpus of the Bible, HELIX can also translate General Domain text.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Contact](#contact)

---

## Usage

### Download or Clone system repository from git.

**Commands:**

```bash
cd
git clone https://github.com/LiteGeorgia/Helix-Machine-Translation-Sampark-System.git
cd Helix-Machine-Translation-Sampark-System
```

---

## Installation

> Below mentioned language system mainly installed and tested in Ubuntu Operating Systems.  
> Dependency Software Requirements: Java, CRF++, DashboardTool

---

### Step 1: JAVA Installation (JDK 8u101)

#### Require Jdk 1.8 or higher, Download and copy it to /usr/local

- Create an Oracle account (if you don’t have one):
```bash
https://profile.oracle.com/myprofile/account/create-account.jspx
```
- Sign in to your Oracle account:
```bash
https://signon.oracle.com/signin
```
- Go to the Java SE 8 Archive Downloads page:
```bash
https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html
```
- Find and download the specific file:
```bash
jdk-8u101-linux-x64.tar.gz
```
- Download and save the downloaded file in the directory.

**Commands:**

- Copy the downloaded file to /usr/local/:

```bash
sudo cp jdk-8u101-linux-x64.tar.gz /usr/local/
cd /usr/local/
```

- Extract JAVA File:

```bash
sudo tar -xvzf jdk-8u101-linux-x64.tar.gz
sudo vi /etc/profile
```

- Inside VI Editor copy below two lines:

```bash
export JAVA_HOME=/usr/local/jdk1.8.0_101
export PATH=$JAVA_HOME/bin:$PATH
```
- And paste these lines at bottom (Below fi line) inside the VI Editor.
- Save and quit the editor window.

- Change to source mode:
```bash
source /etc/profile
#check java version
java -version
```
- It should show like this:
```bash
java version "1.8.0_101"
Java(TM) SE Runtime Environment (build 1.8.0_101-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.101-b13, mixed mode)

```
- Exit Profile:
```bash
exec bash
```
- Check for Java Version:
```bash
java -version
```
- It should show like this:
```bash
java version "1.8.0_101"
Java(TM) SE Runtime Environment (build 1.8.0_101-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.101-b13, mixed mode)

```
- If it doesnot show like this then do following steps:
```bash
#Extract and Install:

sudo mkdir -p /opt/java
sudo tar -xzvf jdk-8u101-linux-x64.tar.gz -C /opt/java

#Configure Java Alternatives:

sudo update-alternatives --install /usr/bin/java java /opt/java/jdk1.8.0_101/bin/java 1
sudo update-alternatives --install /usr/bin/javac javac /opt/java/jdk1.8.0_101/bin/javac 1

#Then configure default (This step is optional):

sudo update-alternatives --config java
sudo update-alternatives --config javac

#Verify Installation:
java -version

```
---

### Step 2: Install Essential Files

**Commands:**

- Install files

```bash
sudo apt update
sudo apt-get install build-essential
sudo apt-get install libgdbm-dev libglib2.0-dev
```

---

### Step 3: CRF++ Installation

**Commands:**

- Open a new terminal for CRF++ & Dashboard Installation in project folder:

```bash
cd
cd Helix-Machine-Translation-Sampark-System
```
 
- Extract CRF++ File

```bash
tar -xvzf CRF++-0.58.tgz
cd CRF++-0.58/ 
```
- Use below four commands to configure CRF++ and install it.

```bash
./configure
make
sudo make install
```

- Create a symbolic Link from the library file ‘/usr/local/lib/libcrfpp.so.0’ to ‘/usr/lib/libcrfpp.so.0’.
  
```bash
sudo ln -s /usr/local/lib/libcrfpp.so.0 /usr/lib/libcrfpp.so.0
```
- Test CRF++ Version.

```bash
crf_test --version
```

- It should show like this:

```bash
CRF++ of 0.58

```
---

### Step 4: Installation of Dashboard

**Commands:**

```bash
cd ..

# Extract Dashboard Files.

tar -xvzf DashboardTool-1.9.tgz
```

- Navigate to Dashboard Tool-1.9

```bash
cd DashboardTool-1.9/
```
- Open Installation_Dash.sh in VI editor

```bash
vi Installation_Dash.sh
```

- In VI Editor:

- Hash first two lines:

```bash
#PERL=’perl -v 2>/dev/null’
#PERL_VER= ‘echo $PERL | awk ‘{ print substr($4, 2, 7);}’
```
- Check your perl version:
```bash
  perl -version
  ```
- Change version 5.34 to latest version of perl (eg: 5.38) in 4th and 5th lines.
- Save and exit.

- Install Dashboard.

```bash
sudo sh Installation_Dash.sh
```

- Open Dashboard.

```bash
source /etc/profile
Dashboard.sh
```

- Inside the Dashboard specify locations Set path:
  
```bash
/usr/share/Dashboard
```
- Then Click Apply to continue.
---

### Step 5: Morph Extraction (Hindi morph required only for Hindi analysis systems)

**Commands:**

- Extract hin-morph File and navigate to the hin-morph directory:

```bash
cd ..
tar -xvzf hin-morph.tgz
cd hin-morph/
```

- Create a new directory named mymorph:

```bash
mkdir mymorph
```

- Assign the values in the current directory to setu:

```bash
export setu=/home/{user_name}/Helix-Machine-Translation-Sampark-System/hin-morph
#Example: setu=/home/calnic/Helix-Machine-Translation-Sampark-System/hin-morph
```

- Navigate to src/sl/morph/hin/:

```bash
cd src/sl/morph/hin/
```

- Compile:

```bash
make compile
```

- Install:

```bash
make install
```

---

### Step 6: Install Sampark system 

**Commands:**

- Navigate to Helix-Machine-Translation-Sampark-System, Un-tar language_file and move it to home:

```bash
cd ../../../../..
tar -xvzf language_file.tgz
mv language_file ~

#Example
#tar -xvzf sampark-hin-hlb.tgz
#mv sampark-hin-hb-0.1 ~

```

- Navigate to home:

```bash
cd
```

- Create a symbolic link named "sampark" that points to the "sampark-hin-hb-0.1" directory:

```bash
ln -s language_file sampark

#Example
#ln -s sampark-hin-hb-0.1 sampark
```

- Edit .bashrc to include setu variable:

```bash
vi .bashrc
#Inside the editor add one line to the bottom of the page ie, below fi.
export setu=$HOME/sampark
```
- Save and Quit.
  
- Apply changes and check setu:

```bash
source .bashrc

#Display the value of the environment variable.

echo $setu
```

- Edit sampark/bin/sys/hin_tel/hin_tel_setu.spec:

- Open sampark/bin/sys/hin_tel/hin_tel_setu.spec in VI editor.

```bash
# Modify paths: - Inside the editor change the system name as your home directory.
vi sampark/bin/sys/hin_tel/hin_tel_setu.spec

#Example:

#<ENV>$setu=/home/trmt/sampark ➜ <ENV>$setu=/home/calnic/sampark
#Also change the system name above “%SYSTEM%” code.
#<OUTPUT_DIR>/home/trmt/OUTPUT.tmp ➜ <OUTPUT_DIR>/home/calnic/OUTPUT.tmp
```
- Save and Exit
---

### Step 7:Morph Configurations 

**Commands:**

- Navigate to sampark then to /bin/sl/morph/:

```bash

cd ../../..
cd bin/sl/morph/
cd hin
```

- Run scripts:

```bash
sh morph_run.sh tests/morph_test.in
echo $setu
sh morph.sh tests/morph_test.in
```
- It should show the results.
---

### Step 8: Final Steps

**Commands:**

- Navigate to Home:
  
```bash
cd 
```
- Create a Folder named OUTPUT.tmp:

```bash
mkdir OUTPUT.tmp
```
- Run Dashboard:
  
```bash
Dashboard.sh
```

- Inside Dashboard:

- Set sampark Path as: /home/{user_name}/sampark
- Set Output Direct as: /home/{user_name}/OUTPUT.tmp 
- Select Source as Hindi and Target Language as Telugu.

### Another Language File Configration:

- If you want to configure another language pair then do the following:

**Commands:**

- Remove sampark:
```bash
rm sampark
```

- Un-tar the language pair file and move it to home directory:

```bash
tar -xvzf language_file.tgz
mv language_file ~

#Example
#tar -xvzf sampark-hin-hlb.tgz
#mv sampark-hin-hb-0.1 ~

```

- Navigate to home:

```bash
cd
```

- Create a symbolic link named "sampark" that points to the "language_file" directory:

```bash
ln -s language_file sampark

#Example
#ln -s sampark-hin-hb-0.1 sampark
```  

- Edit sampark/bin/sys/hin_tel/hin_tel_setu.spec:

- Open sampark/bin/sys/hin_tel/hin_tel_setu.spec in VI editor.

```bash
# Modify paths: - Inside the editor change the system name as your home directory.
vi sampark/bin/sys/hin_tel/hin_tel_setu.spec

#Example:

#<ENV>$setu=/home/trmt/sampark ➜ <ENV>$setu=/home/calnic/sampark
#Also change the system name above “%SYSTEM%” code.
#<OUTPUT_DIR>/home/trmt/OUTPUT.tmp ➜ <OUTPUT_DIR>/home/calnic/OUTPUT.tmp
```
- Save and Exit
- Navigate to home:

```bash
cd
```

- Run Dashboard:
  
```bash
Dashboard.sh
```
---

> **Note:** Home, language pair and test files changes according to your requirement and setup.

---

## Contact

For any queries or support, please contact:

jossy@calnicsolutions.com
