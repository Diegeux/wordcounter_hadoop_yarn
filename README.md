![Hadoop](https://user-images.githubusercontent.com/39379425/167266549-5661b21d-4f4c-4bc4-971a-d82012620689.png)

# Wordcounter with Hadoop
We're going to develop a project which is going to count how many times the words appear in the file. For it, we're going to make use of Hadoop and its modules to process 
big data in a parallel and distributed way, such as:

- Hadoop HDFS: it means Hadoop Distributed File System, it provides high-throughput access to application data;
- Hadoop Yarn: it's a framework that schedules the jobs and manages the cluster resources;
- Hadoop MapReduce: it's a Yarn-based system that works to process large datasets in parallel;

## Tools
- Oracle Virtual Machine - 6.1.26 version;
- PuTTy version - 0.76 version;
- Everis_BigData-v3.ova (Linux CentOS 7.0 / Hadoop 2.6 version);
- Microsoft Windows 10;

## Challenge
1. Install and set up Hadoop server in the Virtual Machine (Linux environment);
2. Access the Hadoop Server in the local machine through PuTTy (I used Windows environment in my development);
3. Use Hadoop to run, stop and manage the resources, for example: wordcout, jobs, logs and etc...

## Development
Download the file Everis_BigData-v3.ova (https://drive.google.com/file/d/1CsHc311jp4EuZ8be5KGaumniGAafa8sC/view), execute it in your Virtual Machine to install Linux and all 
resources of Hadoop, pay attention: take a look in your computer hardware (RAM and network). Change your network configuration for Bridge mode. Then, you are able to log in.

Login: everis
Password: everis2021

![0](https://user-images.githubusercontent.com/39379425/167263820-8d730997-d3e4-422f-a948-5222d18edf14.png)

Alright, try it: ifconfig to find out your Virtual Machine IP. At the exemplo, mine is 192.168.0.120
![1](https://user-images.githubusercontent.com/39379425/167263933-b58684f0-01b8-4cae-a845-0f9fdf925644.png)

Open PuTTy software, use your Virtual Machine IP to set up the SSH access. This means which you are able to access all resources of Virtual Machine (Linux CentOS, Hadoop, Yarn, Mapreduce and so on)
in your Local Machine through SSH protocol. So then, click in Open option.
![2](https://user-images.githubusercontent.com/39379425/167264167-885c4bfa-8f59-491c-8da7-5fdbf8e53324.jpg)

Everything's good, access with the credentials told before. See the expected result:
![3](https://user-images.githubusercontent.com/39379425/167264170-9eb68fc8-e607-4f3c-89b0-a1f2572ba671.jpg)

As we've gotten to access the machine, it's necessary to start the Hadoop services, therefore, run the command: sh script_apoio/start_all_service.sh
![4](https://user-images.githubusercontent.com/39379425/167264171-2df5a312-074d-44ae-b200-b4872330c107.jpg)

I'd recommend that you to run some commands for not to happen issues.

sudo -u hdfs hdfs dfsadmin -safemode leave

To avoid access issues to the File System, it's a great idea to run the above command. It's going to disable the safemode of the hadoop, this allows us any modifications to the File System.

systemctl disable firewalld

To avoid access issues to the Hadoop on the Browser. This command disables the firewall.

Besides it, to have sure that you are able to access Hadoop on the browser, you can run the following command: cat /etc/hadoop/conf/yarn-site.xml |grep bigdata-srv 

![5](https://user-images.githubusercontent.com/39379425/167264172-ecd048fc-dfe5-4f8d-8d5a-cba024f5c0dd.jpg)

Awsomeeeeee and terrificcc...open your browser, and write: your Virtual Machine IP:8080/cluster, like mine: 192.168.9.120:8080/cluster.
![6](https://user-images.githubusercontent.com/39379425/167264174-e5484be6-358b-4c77-adc6-f2283ab6a2cc.jpg)

The party has just begun, mates. Right now, let's enjoy the cake. Heheheh...
Run the command to count the occurence of the words of the file_teste.txt file which is in the path /tmp/file_teste.txt, and the result's going to be saved in the path /tmp/result

sudo -u hdfs yarn jar /usr/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar wordcount /tmp/file_teste.txt /tmp/result
![7](https://user-images.githubusercontent.com/39379425/167264175-654ebe16-2fb7-478f-9728-387038e80bd2.jpg)

Let's check it out! Run the command hdfs dfs -ls /tmp/result to see the result of the process
![8](https://user-images.githubusercontent.com/39379425/167264177-1647bb8d-d1eb-42bc-b0c5-bb1be8d1f49f.png)

Then, see what part-r-00000 file has, write hdfs dfs -cat /tmp/result/part-r-00000
![9](https://user-images.githubusercontent.com/39379425/167264178-41485013-0288-417a-9973-4753ecf2be57.png)

We can realize how many times each words appear, for example, teste, de and datanode appeared 200 times, 99, 98, 97...appeared 2 times.

If you're interested at seeing information about resources managment, you can get it by the application ID. In your Hadoop access (browser), click on Applications option, or write 
your Virtual Machine IP:8080/cluster/apps, follow like mine: 192.168.9.120:8080/cluster/apps. There's a job over there.
![10](https://user-images.githubusercontent.com/39379425/167264179-5c604109-f995-4e08-be1d-8ed6a12498f3.jpg)

Click on it and see more details about it.
![11](https://user-images.githubusercontent.com/39379425/167264182-b56b4678-ebb0-4529-a7e2-25c51997e6bf.jpg)

If to prefer to access via command line, you need to copy the application ID and paste in the command: sudo -u hdfs yarn logs -applicationId "application_ID" |more

Look it as I did: sudo -u hdfs yarn logs -applicationId "application_1651686379034_0001" | more
![12](https://user-images.githubusercontent.com/39379425/167264186-2eee430f-d452-44fe-b602-2d8321e5b39c.jpg)

We can also save the information about the jobs in our machine with the command: sudo -u hdfs yarn logs -applicationId "application_1651686379034_0001" > job_Diego.log

job_Diego.log is the file which stored the job information
![13](https://user-images.githubusercontent.com/39379425/167264187-30bd9968-fa30-45ff-83a4-ed44d7ee4b12.jpg)












