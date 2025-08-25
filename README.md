# Setup for ClamSAP on OS level

## Linux

### Debian / Ubuntu or other generic Unix systems
Manual build can be done similar to github action of
https://github.com/ehhle/clamsap/blob/main/.github/workflows/c-cpp.yml

### RHEL
ClamSAP RPM build

Dependencies
You need to create a basis OS with following needed dependencies
-	rpm build and development tools, because finally you should install the RPM version on your enterprise OS (RHEL, CentOS)
-	clamav-devel packages to build against clamav
-	gc, automake, etc. (everything you need to to a pure C build)
-	git (to retrieve clamsap from source repo)

### Start with a RHEL 8 or 9

sudo yum install -y rpmdevtools rpmlint -y
sudo yum install epel-release -y
sudo yum -y install clamav-server clamav-data clamav-update clamav-filesystem clamav clamav-scanner-systemd clamav-devel clamav-lib clamav-server-systemd -y

### Development tools , e.g. automake , cc, gcc

sudo yum group install "Development Tools" -y 

  -> not all from that needed, but if you can execute gc, gcc and automake try without it
  
sudo yum install git -y

### go to your local directory to build clamsap

git clone https://git.code.sf.net/p/clamsap/git clamsap-git
cd clamsap-git/scripts/
mkdir -p ~/rpmbuild/RPMS/
./rpm_build.sh


#### Finally test the RPM

cd ~/rpmbuild/RPMS/x86_64/
sudo rpm -U clamsap-0.104.3-1.x86_64.rpm

you should have  /usr/lib64/libclamsap.so and  /usr/lib64/libclamdsap.so which can be used from all SAP VSI versions, e.g. ABAP, NetWeaver etc.

### SUSE
ClamSAP on SUSE can installed simply, because there we have a OS level integration.
See zypper commands, e.g. https://github.com/strehle/clamav_vsi_setup?tab=readme-ov-file#example-setup-for-clamsap-on-sles111215
