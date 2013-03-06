
Bionimbus/UIC Cloud  How To
=====================================


### How to connect to Bionimbus/UIC Cloud

1. if you don't have an account on bionimbus cloud, sign up for one.  To sign up, first generate a keypair ( see http://www.bionimbus.org/tutorials/#tutorial-ssh ) then sign up for the account at http://www.opensciencedatacloud.org/new-account-request/.   You will need to send the bionimbus sys admin your public key file before they can setup an account for you.

2. Login to bionimbus cloud using your account, i.e., ssh USER_NAME@login.bionimbus.org

3. To create virtual and run virtual instances, see http://www.bionimbus.org/tutorials/bionimbus-cloud-instructions/

4.  Once you are on bionimbus cloud, the path for modENCODE data folder is '''/glusterfs/data/modencode'''

For more information, see http://www.bionimbus.org/tutorials/

### How to transfer data between OICR and Bionimbus Cloud

At the moment, Quang Trinh <quang.trinh@oicr.on.ca> is the only person setup for transferring data between OICR and Bionimbus Cloud2.  

To push data from OICR to Bionimbus Cloud2:

1. login to xfer-cloud.res.oicr.on.ca.  

2. Use rsync to 'sync' data from OICR to Bionimbus Cloud2.  for example

> rsync --progress -avu -B 8192 --stats -hh /source/path/data  quang@74.114.99.130::quang/

The modencode data folder on Bionimbus Cloud2 is: '''/glusterfs/data/modencode/modencode-dcc/'''  ( on Bionimbus Cloud1, the path is '''/glusterfs/public/bionimbus/modencode-dcc/''' )


### How to get previous peakcall results from Bionimbus Cloud1 on Bionimbus Cloud2

1. Login to a VM on Cloud2

2. Fetch data from Cloud1 by running this command:

>/cloudconf/list-bionimbus-data qtrinh/cloud1.modencode-dcc/ 

For more information, see http://www.bionimbus.org/tutorials/modencode-dcc-download-instructions/

### How to create a key-pair on Bionimbus Cloud
On the login bionimbus cloud ( i.e., '''login.bionimbus.org''' ) do 
 > euca-add-keypair bionimbus > bionimbus.priv     # create a keypair
 > cp bionimbus.priv  ~/.ssh/id_rsa                # copy your private key to .ssh dir

### How to create a VM and setup environments on Bionimbus Cloud
1. For how to create a VM on Bionimbus Cloud, login the VM and mount the shared file systems on the VM - see http://www.bionimbus.org/tutorials/bionimbus-cloud-instructions/

2. Once you are in your VM, change to softwares directory and set your environments
 > cd /glusterfs/data/modencode/modencode-dcc/softwares
 > . env.sh

### How to run BWA on Bionimbus Cloud
1. Create your VM and setup your environments on Bionimbus Cloud - see http://wiki.modencode.org/project/index.php/Resources/Bionimbus-UIC.how.to#How_to_create_a_VM_and_setup_environments_on_Bionimbus_Cloud

2. BWA should be in your path now.  The full path for BWA is '''/glusterfs/data/modencode/modencode-dcc/softwares/aligners/bwa'''

3. Align your data using BWA with the appropriate reference in '''/glusterfs/data/modencode/modencode-dcc/genomes/<species>/<build>/bwa'''.  For example, for Celegans WS220, the full path of this reference indexed by BWA is in this directory '''/glusterfs/data/modencode/modencode-dcc/genomes/C.elegans/Cele_WS220/bwa'''.  For more information on how to use BWA, see the manual page at http://bio-bwa.sourceforge.net/bwa.shtml.  Typically, there are 4 steps:

 \# step 1: alignment to get the suffix array (SA) coordinates ; -t 7 tells bwa to use 7 cores for the alignment
 
 \> bwa  aln  -t 7  ....   

 \# step 2: convert SA coordinates to SAM
 
 \> bwa  samse  ...    # for single end 
 
 \> bwa  sampe  ...    # for paired-end data 

 \# step 3: convert SAM to BAM
 
 \> samtools  view  -bSo  OUTPUT.bam  INPUT.sam 

 \# step 4: sort BAM
 
 \> samtools sort INPUT.bam OUTPUT_PREFIX

### How to run PeakRanger on Bionimbus Cloud
1. Create your VM and setup your environments on Bionimbus Cloud - see http://wiki.modencode.org/project/index.php/Resources/Bionimbus-UIC.how.to#How_to_create_a_VM_and_setup_environments_on_Bionimbus_Cloud

2. PeakRanger should be in your path now.  The full path for PeaKRanger is ''' /glusterfs/data/modencode/modencode-dcc/softwares/peakcalls/PeakRanger/current'''.  To use PeakRanger, see http://ranger.sourceforge.net/

### How to run macs14 on Bionimbus Cloud
1. Create your VM and setup your environments on Bionimbus Cloud - see http://wiki.modencode.org/project/index.php/Resources/Bionimbus-UIC.how.to#How_to_create_a_VM_and_setup_environments_on_Bionimbus_Cloud

2. macs14 should be in your path now.  The full path for macs14 is '''/glusterfs/data/modencode/modencode-dcc/softwares/peakcalls/MACS/MACS-1.4.1'''.  To use macs14, see 
http://liulab.dfci.harvard.edu/MACS/00README.html

### How to run SPP on Bionimbus Cloud
1. Create your VM and setup your environments on Bionimbus Cloud - see http://wiki.modencode.org/project/index.php/Resources/Bionimbus-UIC.how.to#How_to_create_a_VM_and_setup_environments_on_Bionimbus_Cloud

2. spp should be in your path now.  The full path for spp is '''/glusterfs/data/modencode/modencode-dcc/softwares/peakcalls/SPP'''.  To use spp, see http://sites.google.com/site/anshulkundaje/projects/idr.  There is also a tutorial for spp at http://compbio.med.harvard.edu/Supplements/ChIP-seq/tutorial.html.

### How to run IDR on Bionimbus Cloud
1. Create your VM and setup your environments on Bionimbus Cloud - see http://wiki.modencode.org/project/index.php/Resources/Bionimbus-UIC.how.to#How_to_create_a_VM_and_setup_environments_on_Bionimbus_Cloud

2. IDR should be in your path now.  The full path for IDR is '''/glusterfs/data/modencode/modencode-dcc/softwares/peakcalls/IDR/idrCode'''.  To use IDR, click [https://sites.google.com/site/anshulkundaje/projects/idr here]

