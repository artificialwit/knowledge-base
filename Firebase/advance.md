### Firebase Messageing

#### Firebase push notification

Reference : 

https://medium.com/android-school/test-fcm-notification-with-postman-f91ba08aacc3  
https://firebase.google.com/docs/cloud-messaging/http-server-ref#table1

Send Firebase push notification from postman. First create a legacy server key or web app key depends on version .
Provide that key on header section. and POST on https://fcm.googleapis.com/fcm/send


Authorization:key=AAAAE566IeA:APA91bGgHuItwR-BkOlD2DMtQihEG5n4N-N5vgL0I4tUh.......



```json
{
    "to": "cUDBc2_9QnetrnqHfWtKxw:APA91bEyS4mfh2g4m2qGVm7HwE_p.........Device FCM ID to be placed here",
    "collapse_key": "type_a",
    "notification": {
        "body": "My Notification body",
        "title": "My Notification Title"
    },
    "data": {
        "body": "Body to pass in data to take action on notification tap",
        "title": "Title 1",
        "field_1": "1233",
        "field_2": "wwwwww"
    }
}

```
