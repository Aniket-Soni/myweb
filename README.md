# devopstask
## myblog
### Task about integration of jenkins with GitHub.

*IN GitHub*
 *  Create one repository without any branches.

*In Windows* 
 * Created a local repository. 
 * In this repository two branches are created. 
   * Master 
   * Dev1 
   javascript
   git init 
   cat > web1.html
   git add web1.html
   git commit. -m "first"
   git branch dev1
   git remote -v
   git remote add origin URL
   git push -u origin master
   git push -u origin  dev1
   
   
   
*this data is updated in github in master  and dev1 branch

*In Jenkins*
  * job1 created using poll scm trigger. 
    * this job keeps on checking dev1 branch. if there's anything updates it automatically send this to testing operating system.
    * this job deploys the data to testing operating system.
  
  * Allowing jenkins to run any command.
  javascript
  gedit /etc/sudoers
  
  * Deploying the Data.
  
    * We create a job1a in this we use poll scm, it copies the data in /lwweb2 folder.
    
      javascript
      sudo cp -v -r -f /lwweb
      
    * Then we created job1b and used chaining with job1a which deployes the data to docker testing server.
    
      javascript
      if sudo docker ps|grep testmyos
      then
      echo "already running"
      else 
      sudo docker run -d -t -i -p 8082:80 -v /lwweb:/usr/local/apache2/htdocs/ --name testmyos1 httpd
      fi
  
    
  * job2 created to keep on checking the main branch.
    * this job send the data to main production team. 
    
  * job 3 created to verify the testing data that was given by job1. for this QAT team is connected to remote url.
     * after testing succeeded, QAT team merge this data to master branch of github.
     
   *after master updated by job3, job3 and job 2 are connected by chaining, so after job3 success job2 starts to run*
      * after job2 created successfully they send data to production team. 
     
  *Production team send this data to webserver using tunnel by exposing  where client can connect* 
  
  *in the job2 execute shell*
  
  javascript
  if sudo docker ps|grep runmyos
  then
  echo "already running"
  else 
  sudo docker run -d -t -i -p 8081:80 -v /lwweb:/usr/local/apache2/htdocs/ --name runmyos1 httpd
  fi
