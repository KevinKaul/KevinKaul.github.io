# Golang sample code

~~~go
import (
    "bytes"
    "crypto/hmac"
    "crypto/sha1"
    "encoding/base64"
    "time"
)

func getSignature(appId, appSecret string) string {
    s := fmt.Sprintf("appId=%s&timestamp=%d", appId, time.Now().Unix())
    mac := hmac.New(sha1.New, []byte(appSecret))
    mac.Write([]byte(s))
    return base64.StdEncoding.EncodeToString(mac.Sum(nil))
}
~~~
