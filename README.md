ipop-test
=========

ipop-test provides test harness for ipop and helps deploying multiple ipop-nodes in cluster environment. It leverages python unittes framework (https://docs.python.org/2/library/unittest.html). With this script, you can deploy and run multiple ipop-nodes in blank VM. 


TEST CLASSES
============

At this point, there are three test classes. TestInstall and TestLxcCreate classes are the prerequisite class, so you need to run these two classes before other test class. 

1. TestInstall
  Install XMPP and LXC.
2. TestLxcCreate
  Create LXC instances 
3. TestSocialVPN
  TestInstall and TestLxcCreate should had run once before this test. This test send ping packet from one node to all the other nodes. For example, if instance_count is set 5, 5 lxc instances created and each instance sends ping to all the other ipop-nodes. In total, 20 differeng ping command runs. 
...

We plan to add more complex and thorough test scenarios alongside with script implementation.


Usage instruction
=================

1. Prepare a blank VM(Ubuntu is preferred)

2. download test.py script 

```
wget https://github.com/ipop-project/ipop-test/raw/master/test.py
chmod +x test.py
```

3. Install XMPP and LXC in VM
```
python -m unittest -v test.TestInstall
```

This command should complete with this output
```
----------------------------------------------------------------------
Ran 2 tests in 86.865s

OK
```

4. Create LXC isntances 

The number of LXC can be specified in the script. 
instance_count : number of LXC instances
ipop_download_link : URL link for ipop-download
ipop_dir : directory name of IPOP after extraction

```
vi test.py

instance_count = 3
ipop_download_link = "https://github.com/ipop-project/downloads/releases/"+\
                     "download/14.07.1.rc2/ipop-14.07.1.rc2-x86_ubuntu.tar.gz"
ipop_dir = "ipop-14.07.1.rc2-x86_ubuntu"
```

```
python -m unittest -v test.TestLxcCreate
```

5. Choose the test class you want and run it 
```
python -m unittest -v test.TestSocialVPN
```


