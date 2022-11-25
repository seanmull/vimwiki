## Snippets

RMQ pub-sub pattern

```typescript
// processes the event
// the function on the ocd side that does something
public requestGreyListFromMacyGrey() {
  return Promise.resolve()
    .then(() => {
      let payload: any = {
      // we grab the payload from redis
        format: "csv",
      };
      return this.service.rmqRpc?.sendRpc(
        "nl-macygrey.list.get",
        payload,
        {},
        { trace_id: this.ocdService.uuid() }
      );
    })
    .then((results) => {
      return results
    });
}
```

```typescript
// add listener
// ties an event to a function
this.rpc.addEventHandler(
    "nl-ocd.default.event",
    "nl-macygrey.event.error",
    this.softwareServer.getGreyList.bind(this.softwareServer),
    undefined
);
```

```typescript
// emits
// tell ocd when to do something
// store something here in redis
this.sendNotification("error", "event", {
  message: "GreyList has changed."
})
return result[1][0];
});
```

## Another example


```typescript
// listener function
updateTimeTillNextCheck(){
    return Promise.resolve().then(() => {
        return this.getRowDataFromRedis()
    }).then((results: number) => {
        return this.setTimeTillNextCheck(results)
    }).then(() => {
        this.checkStatusTask.interval = this.getTimeTillNextCheck()
    })
}

// helper function
public getRowDataFromRedis(){
    if(this.service.redis){
            return Promise.resolve().then(() => {
                return this.service.redis?.hgetall("nl-ocd.update_time_till_next_check.row_info")
        }).then((results) => {
            if(results){
                const row_info = JSON.parse(results["nl-ocd.update_time_till_next_check.row_info"])
                console.log(row_info)
                return row_info
            }
        })
        .catch((error) => {
            console.error(error)
        })
    }
}
```
    
```typescript
// emits notifiction
Promise.resolve().then(() => {
    return this.service.redis?.hset("nl-ocd.update_time_till_next_check.row_info", "nl-ocd.update_time_till_next_check.row_info", JSON.stringify(Number(row.info.replace(/"/g, ''))))
}).then(() => {
    return this.sendNotification('update_time_till_next_check', 'event', {
        message: 'Update the time until next check.' })
})

```

```typescript
// event handler/listener
this.rpc.addEventHandler("nl-ocd-chatterbox.default.event", "nl-ocd.event.update_time_till_next_check", this.ocdChatterboxController.updateTimeTillNextCheck.bind(this.ocdChatterboxController), undefined)
```
