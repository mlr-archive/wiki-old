0. Get your API token from your profile page at: https://travis-ci.org/profile

1. Send a POST request to /job/:job_id/debug replacing the TOKEN and JOB_ID values below:

```bash
#! /usr/bin/env bash  curl -s -X POST \
   -H "Content-Type: application/json" \
   -H "Accept: application/json" \
   -H "Travis-API-Version: 3" \
   -H "Authorization: token <TOKEN>" \
   -d '{ "quiet": true }' \
   https://api.travis-ci.org/job/<JOB_ID>/debug 
```

The Job ID is displayed in the build log after expanding "Build system information".

2. Head back to the web UI and in the log of your job. There you should see the following lines to connect to the VM:

Setting up debug tools.
Preparing debug sessions.
Use the following SSH command to access the interactive debugging environment:
ssh ukjiuCEkxBBnRAe32Y8xCH0zj@ny2.tmate.io

3. Connect from your computer using SSH into the interactive session, and once you're done, just type exit and your build will terminate.

Once in the SSH session, these bash functions will come in handy to run the different phases in your build: https://docs.travis-ci.com/user/running-build-in-debug-mode/#Things-to-do-once-you-are-inside-the-debug-VM