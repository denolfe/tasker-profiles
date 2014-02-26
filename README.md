# Tasker Profiles

## Home Near
Turns Wifi on when near Home, based upon cell tower location
#### Context
- NOT Wifi Connected (Home Wifi)
- Cell Near

#### Enter
- Wifi On

#### Exit
- Wifi Off

## Home
Maximizes volume and sets HOME variable
#### Context
- Wifi Near

#### Enter
- Variable Set: `%HOME` To 1
- Say: Welcome Home
- Perform Task: Sound Loud

#### Exit
- Variable Clear: `%HOME`

## Car BT
Misc actions on bluetooth connect
#### Context
- Bluetooth Connected

#### Enter
- Wait: 2 secs
- Music Play: Ringtones/hangouts_message.ogg
- Wait: 4 secs
- Media Volume: 15
- Load App: Pocket Casts
- Wifi Off
- Display Timeout: 10 mins
- Variable Set: `%CAR` To 1
- Variable Clear: `%HOME`

#### Exit
- Media Control
    + Cmd Stop, Simulate Media Button Off
- Media Control: 
    + Cmd Stop, Simulate Media Button On
- Music Stop
- Go Home: 0
    + If `%WIN !~ Home`
- Variable Clear: `%CAR`

## Work
Silent mode at work
#### Context
- 8a-5p
- Mon-Fri
- NOT Wifi Near (Home Wifi)

#### Enter
- Silent Mode: On
- Wifi On
- Variable Set: `%WORK` To 1

#### Exit
- Perform Task: Sound Loud
- Media Volume: 15
- Variable Clear: `%WORK`

## Unpaired BT
Turn off bluetooth if disconnected for 10 mins
### Context
- NOT Bluetooth Connected
- `%BLUE` matches on

#### Enter
- Variable Set: `%BTCOUNTER` To `%TIMES + 600` (10 mins)
- Wait 1 min
    + Until `%TIMES` > `%BTCOUNTER`
- Bluetooth Off
    + If `%PACTIVE` matches `*Unpaired*`

#### Exit
- Bluetooth Off
- Variable Clear: `%BTCOUNTER`

## Call Ended/Dropped
Vibrates when call ended. Useful to know when a call is dropped.
### Context
- Phone Idle

#### Enter
- Vibrate Pattern: 0,75,100,75
- Go Home: 0
