# C sample code

~~~c
static void ZY_hmac_sha1(__u8 *key,__s32 key_len,__u8 *data,__s32 data_len,__u8 *digest)
{
    __s32 b = 64; /* blocksize */
    __u8 ipad = 0x36;
    __u8 opad = 0x5c;
    __u8 k0[64];
    __u8 k0xorIpad[64];
    __u8 step7data[64];
    __u8 step5data[4096+128];
    __u8 step8data[64+20];
    __s32 i=0;

    ukit_memset(k0,0,sizeof(k0));
    ukit_memset(k0xorIpad,0,sizeof(k0xorIpad));
    ukit_memset(step7data,0,sizeof(step7data));
    ukit_memset(step5data,0,sizeof(step5data));
    ukit_memset(step8data,0,sizeof(step8data));
 
    for (i=0; i<64; i++)
    {
        k0[i] = 0x00;
    }

    if (key_len != b)    /* Step 1 */
    {
        /* Step 2 */
        if (key_len > b)
        {
            mbedtls_sha1(key, key_len, digest);
            for (i=0;i<20;i++)
            {
                k0[i]=digest[i];
            }
        }
        else if (key_len < b)  /* Step 3 */
        {
            for (i=0; i<key_len; i++)
            {
                k0[i] = key[i];
            }
        }
    }
    else
    {
        for (i=0;i<b;i++)
        {
            k0[i] = key[i];
        }
    }

    /* Step 4 */
    for (i=0; i<64; i++)
    {
        k0xorIpad[i] = k0[i] ^ ipad;
    }

    /* Step 5 */
    for (i=0; i<64; i++)
    {
        step5data[i] = k0xorIpad[i];
    }
    for (i=0;i<data_len;i++)
    {
        step5data[i+64] = data[i];
    }

    /* Step 6 */
    mbedtls_sha1(step5data, data_len+b, digest);

    /* Step 7 */
    for (i=0; i<64; i++)
    {
        step7data[i] = k0[i] ^ opad;
    }

    /* Step 8 */
    for (i=0;i<64;i++)
    {
        step8data[i] = step7data[i];
    }
    for (i=0;i<20;i++)
    {
        step8data[i+64] = digest[i];
    }
    /* Step 9 */
    mbedtls_sha1(step8data, b+20, digest);
}

__u8 ZY_kupc_get_sign(__u8** sign)
{
    int ret = UKIT_FAIL;
	int len = 0;
	char buf_base64[1024];
    char stringToSign[1024];
    char Sign_buf[256+1];

	ukit_memset(buf_base64,0,sizeof(buf_base64));
	ukit_memset(stringToSign,0,sizeof(stringToSign));
	ukit_snprintf(stringToSign,1024,"appId=%s&timestamp=%d",ZY_KYPC_APPID,uQDS_ntp_get_second());
	
	printf("the stringToSign :%s \n",stringToSign);
	ukit_memset(Sign_buf,0,sizeof(Sign_buf));
	ZY_hmac_sha1(ZY_KYPC_APP_SECRET,ukit_strlen(ZY_KYPC_APP_SECRET),stringToSign,ukit_strlen(stringToSign),Sign_buf);

	ukit_hexdump(Sign_buf,256+1);
	mbedtls_base64_encode(buf_base64,sizeof(buf_base64),&len,Sign_buf,ukit_strlen(Sign_buf));
	*sign = ukit_strdup(buf_base64);

    return ret;
}
~~~
