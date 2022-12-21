nl-chatterbox

These events needed to be added to update which systems are online 
```typescript
        this.rpc.addEventHandler("nl-ocd-chatterbox.default.event", "nl-hdms.event.control.system_online", OnlineSystemsController.instance.onSystemOnlineEvent.bind(OnlineSystemsController.instance), undefined)
        this.rpc.addEventHandler("nl-ocd-chatterbox.default.event", "nl-hdms.event.control.system_offline", OnlineSystemsController.instance.onSystemOfflineEvent.bind(OnlineSystemsController.instance), undefined)
    if (!OnlineSystemsController.instance.isSystemOnline(row.system_id))
        return this.offlineCheck(row.system_id)           
```

This part of chatterbox will update configuration of the servers and populate which server is online and which ones can hit the internal content server

```typescript
    return Promise.all([
      this.updateServerConfiguration(),
      OnlineSystemsController.instance.populate(),
      InternalSystemsController.instance.populate(),
    ])
    .then(() => {
```

The chatterbox controller is local scoped to this
It then eventually be becomes more available to the app via the service container
The other three are close scoped to this object
We don't need to share the other controller instances outside of this class.
That is why it is static
```typescript
    this.ocdChatterboxController = new OcdChatterboxController(this.config, 
                                                               this.service, 
                                                               this.service.jobAPIController, 
                                                               'Ocd chatterbox Controller', 4);
    this.service.ocdChatterboxController = this.ocdChatterboxController;

    new ErrorsController(this.config, this.service, "ErrorsController")
    new OnlineSystemsController(this.config, this.service, "OnlineSystemsController")
    new InternalSystemsController(this.config, this.service, "InternalSystemsConstroller")
```

This is an override to which queue we want to recieve messages to (ocd or ocd-lite)
```typescript
    if(config.is_ocd_lite){
        //@ts-ignore
        config.rmq_rpc.event_queue_bindings = {
            default : [
                "nl-hdms.event.control.system_online",
                "nl-hdms.event.control.system_offline",
            ]
        }

        config.app_meta.name = config.app_meta.name + '-lite'
    }
    if (!this.debug) {
        if (!this.config.is_ocd_lite)
            this.consumeMessages()
        this.rpc.addEventHandler(this.app_meta.name + ".default.event", "nl-hdms.event.control.system_online", this.onSystemOnline.bind(this), undefined)
        this.rpc.addEventHandler(this.app_meta.name + ".default.event", "nl-hdms.event.control.system_offline", OnlineSystemsController.instance.onSystemOfflineEvent.bind(OnlineSystemsController.instance), undefined)            
    }
```
read the database
make sure you read the populate
checks to see if they are online or offlines

online systems controller
recorded the status of the systems

cannot check the status if its offlines

internal system
start internal -> then assigned a client
ship them onsite 
any systems that can hit the internal content server
push proirities
