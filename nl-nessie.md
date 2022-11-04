## The basics of what it does
Nessie takes logs from the hdms and sends them out to mailing lists.  This helps diagnose any problems there might be with the systems.

## Architecture

TBD


## How to run application

Make sure you are logged into the dev cluster
Look over how to change the launch.json to include the env variables. Everything should point to dev.
If you are port 80 move it to 3001 or something like that.


## How to test application


How to test daily logs
This hits the onSetDailyLog endpoint to grab the logs from the HDMS.  We can pass messages into
here to test whether or not certain logs get emailed or not.
```
        /*
        setTimeout(() => {
            try {
                let messages = this.spam();
                //console.log(messages)
                
                _.forEach(messages.rows, (row) => {
                    //if (row.Message === 'PR1') {
                        this.service.nessie.onSetDailyLog({actor:{ system:'ADIN23A', zone:1}, verb:{}, object:row, target:{}, published:{}}, 
                            {trace_id:new Date().toISOString()})
                  //  }
                })
            }
            catch (error) {
                console.log(error)
            }
        }, 1000)
        */
    })
}

private getRandomInt(min: number, max: number) {
    min = Math.ceil(min)
    max = Math.floor(max)
    return Math.floor(Math.random() * (max - min + 1)) + min
}

private emptyScheduler(): any {
}
```


The map tells what logs get sent emails. Its a key value pair that maps the message description with the message you want to send via email
```
const alertKey = obj.Player + ':' + obj.Message
        if (alertKey in this.service.dailyLogAlertMap) {
            let alertInfo = this.service.dailyLogAlertMap[alertKey]
            if (typeof alertInfo == 'function')
                alertInfo = alertInfo(request, obj)
         
```
You can go on the intranet and look in the daily log section to see all the logs for each system
Hit F12 to get the json response the from the front end.  Go to networking then the response tab. This can then be passed into the daily log to daignose if nessie will send the email.

If you get a message thats not in the map you will need to add it to the DB table.
