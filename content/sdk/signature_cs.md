# C# sample code

~~~c#
public static string HMACSHA1Text(string stringToSign,string appSecret)
{
    HMACSHA1 hmacsha1 = new HMACSHA1();
    hmacsha1.Key = System.Text.Encoding.UTF8.GetBytes(appSecret);
    byte[] dataBuffer = System.Text.Encoding.UTF8.GetBytes(stringToSign);
    byte[] hashBytes = hmacsha1.ComputeHash(dataBuffer);  
    return Convert.ToBase64String(hashBytes); 
}
long timestamp = (long)(DateTime.UtcNow - new DateTime(1970, 1, 1, 0, 0, 0, DateTimeKind.Utc)).TotalSeconds;
string stringToSign = "appId=" + appId + "&timestamp=" + timestamp.ToString();
string signature = HMACSHA1Text(stringToSign, appSecret)
~~~
