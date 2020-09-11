# Kijiji-Reposter
Kijiji Automated Reposting and Replying Utility written in Python (version 3.7.7 at time of creation). Is completely api driven (i.e. no webscraping). Utilizes Flask, to run a local server designed to manage the GUI interface and reposting / scheduling and auto reply functions. Viable for both server and desktop environments, but if desktop, system must run 24/7 and have sleep functions disabled.


__Recent Updates:__
- added conversations support
- fixed message auto replier bugs
- absolute paths incorporated for wider compatability
- retry failed attempts

__Requirements:__
```
wheel
Flask-WTF
Flask
xmltodict
httpx
apscheduler
urllib3
```


__Usage:__

Edit the secret key argument on line 24 in server.py. Then run:
```
python server.py
```


__Connections:__

Once server is running, connect to either of the addresses listed below in a web browser. Or if running on a network, connect to the ip and port 5000 of computer running the kijiji reposter server.
```
localhost:5000/
127.0.0.1:5000/
```


__Accounts:__

Login using an existing kijiji account. Or if you do not have an account, create one at kijiji.ca.


__Reposting:__

To create a reposting schedule, begin creating an ad by clicking the 'Post' icon at the top of the home screen. While entering the ad details, make sure to check the repost checkbox and enter the reposting times (eg. 07:00 am, 1:30 pm). Currently, only 8 reposting slots have been implemented. But you can edit the server.py code to allow for more.


__Auto Replier:__

The auto replier scans your account for new messages, and if a new message is found and contains any word or phrase (not case sensitive) defined as a 'rule', it will automatically send the associated 'response'. When setting up a new rule, enter the desired, rule and response along with your password, as it will be required by the auto replier when logging in to check recent messages. Currently the auto replier checks your messages every 25 minutes if rules have been created.  You can adjust the timing by editing the following code on line 1655:

```
sched.add_job(messageAutoReplier,'cron',minute='*/25')
```

Change the `*/25` to any number of your choosing, example: `*/6`

Please note that using the auto replier will mark messages as read, meaning that when checking your messages manually they will not appear as new / unread.


__Force Post Ad from File:__

If you require the ability to force post an ad from file due to botched reposting, accidental deletion or other strange circumstances, you can access the force post function at `localhost:5000/force`. Note that you will first need to have an ad file saved in the users folder, both of which would have been created when initially posting an ad with a reposting schedule, and two, you will also be required to manually update the 'current_ad_id' field in the schedules.json file after the forced repost if a reposting schedule exists.


__ToDo:__

- implement async
- impliment notification functionality
- basic bug fixes / improvements
