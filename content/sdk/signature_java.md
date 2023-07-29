# Java sample code

~~~java
import java.util.Base64;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
public static String calculateRFC2104HMAC(String stringToSign, String appSecret) {
    SecretKeySpec signingKey = new SecretKeySpec(appSecret.getBytes(),"HmacSHA1");
    Mac mac = Mac.getInstance("HmacSHA1");
    mac.init(signingKey);
    byte[] hashBytes = mac.doFinal(stringToSign.getBytes());
    return Base64.getEncoder().encodeToString(hashBytes);
}
String timestamp = Long.toString(System.currentTimeMillis() / 1000);
String stringToSign = "appId=" + appId + "&timestamp=" + timestamp;
String signature = calculateRFC2104HMAC(stringToSign, appSecret)
~~~
