# SEA:ME@Korea 2023 Summer Hackathon<br>

## Contents
- [Step 1 : Install Ubuntu image on VMware](#Step-1-VMwareWorkstation17)
- [Step 2 : Windows settings for VMware WIFI](#windows-settings-for-VMware-WIFI)
- [Step 3 : VMware Ubuntu settings](#VMware-Ubuntu-Settings)

---

### Install OpenJDK Java 8 on your device
OpenJDK – An open-source Java environment, licensed under the GNU General Public License.
Oracle Java – A paid service that includes support options and licensing. (most are not compatible with Raspberry Pi) JRE: Java Runtime Environment (for running Java applications)
<pre>
<code>
sudo apt update
sudo apt install openjdk-8-jdk
</code>
</pre>
You can check installation
<pre>
<code>
java -version
// Check 1.8.0.xxx
</code>
</pre>
If you have installed both OpenJDK 8 and 11, your default version will OpenJDK 11.
<br>
To manually set a Java version, start by running the following command
<pre>
<code>
sudo update-alternatives --config java
</code>
</pre>
Select number and set OpenJDK 8 as the system default

