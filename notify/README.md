### API:
https://bbernhard.github.io/signal-cli-rest-api/  

### QR:
http://localhost:8020/v1/qrcodelink?device_name=signal-api  

### Test:
```bash
curl -X POST -H "Content-Type: application/json" 'http://localhost:8020/v2/send' -d '{"message": "Test via Signal API!", "number": "+XXYYYYYYYYYY", "recipients": [ "+XXYYYYYYYYYY" ]}'
```
#### ----------------------------------------- registering ---------------------------------------------------------
More info: https://github.com/bbernhard/signal-cli-rest-api/blob/master/doc/HOMEASSISTANT.md#set-up-a-phone-number  
find captcha through browser F12, dev tools, generated HTML via: https://signalcaptchas.org/registration/generate  
  
```bash
curl -X POST -H "Content-Type: application/json" -d '{"captcha":"signal-hcaptcha-short......................", "use_voice": false}' 'http://localhost:8020/v1/register/+XXYYYYYYYYYY'
curl -X POST -H "Content-Type: application/json" 'localhost:8020/v1/register/+XXYYYYYYYYYY/verify/[pinsms]'
curl -X POST -H "Content-Type: application/json" 'http://localhost:8020/v1/accounts/+XXYYYYYYYYYY/username' -d '{"username": "username"}'
curl -X PUT -H "Content-Type: application/json" 'http://localhost:8020/v1/profiles/+XXYYYYYYYYYY' -d '{"name": "name surname", "about": "", "base64_avatar": ""}'
```
