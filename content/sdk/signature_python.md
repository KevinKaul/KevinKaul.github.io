# Python sample code

~~~python
import hashlib
import hmac
def _hmac_sha1(data, secret):
  return str(base64.b64encode(hmac.new(bytes(secret, 'utf-8'), bytes(data, 'utf-8'),
                                       hashlib.sha1).digest()), 'utf-8')
timestamp = str(int(time.time()))
string_to_sign = "appId=" + app_id + "&timestamp=" + timestamp
signature = _hmac_sha1(string_to_sign, app_secret)
~~~
