# Request signatures

You must sign all HTTP or HTTPS API requests to ensure security. Alibaba Cloud uses the request signature to verify the identity of a request sender. Alibaba Cloud implements symmetric encryption with an AccessKey pair to verify the identity of the request sender.

**Note:**

-   An AccessKey pair serves as logon credentials that are used to call API operations, and the username and password are used to log on to the Elastic Compute Service \(ECS\) console. An AccessKey pair consists of an AccessKey ID and an AccessKey secret. The AccessKey ID is used to verify the identity of the user, and the AccessKey secret is used to encrypt and verify the signature string. You must keep your AccessKey secret strictly confidential. For more information, see [Create an AccessKey pair]().
-   ECS provides SDKs in multiple programming languages, including third-party SDKs, to facilitate complex signature calculation. For more information, download [SDKs](https://github.com/aliyun).

## Step 1: Create a canonicalized query string

1.  Arrange the request parameters \(including all common and operation-specific parameters except `Signature`\) in alphabetical order. For more information, see [Common parameters](/intl.en-US/API Reference/Getting started/Common parameters.md).

    **Note:** If you use the GET method to send a request, the request parameters are included as a part of the request URL. The first parameter follows the question mark \(`?`\) in the URL, and the other parameters follow an ampersand \(`&`\).

2.  Encode the request parameters and parameter values in UTF-8 based on [RFC 3986](http://tools.ietf.org/html/rfc3986). The following rules apply in the encoding process:
    -   Uppercase letters, lowercase letters, digits, and some special characters such as hyphens \(`-`\), underscores \(`_`\), periods \(`.`\), and tildes \(`~`\) do not need to be encoded.
    -   Other characters must be percent encoded in the `%XY` format. `XY` represents the ASCII code of the characters in hexadecimal notation. For example, double quotation marks \(`"`\) are encoded as `%22`.
    -   Extended UTF-8 characters are encoded in the `%XY%ZA...` format.
    -   Spaces must be encoded as `%20`. Do not encode spaces as plus signs \(`+`\).

        The preceding encoding method is similar to but slightly different from the `application/x-www-form-urlencoded` MIME-type encoding algorithm.

        If you use `java.net.URLEncoder` in the Java standard library, use `percentEncode` to encode request parameters and their values. In the encoded query string, replace plus signs \(`+`\) with `%20`, asterisks \(`*`\) with `%2A`, and `%7E` with tildes \(`~`\). In this way, you can obtain an encoded string that matches the preceding encoding rules.

        ```
        private static final String ENCODING = "UTF-8";
        private static String percentEncode(String value) throws UnsupportedEncodingException {
        return value ! = null ? URLEncoder.encode(value, ENCODING).replace("+", "%20").replace("*", "%2A").replace("%7E", "~") : null;
        }
        ```

3.  Connect the encoded parameter names and values with equal signs \(`=`\).
4.  Use an ampersand \(`&`\) to connect the encoded request parameters. Note that these parameters must be arranged in the same order as those in [Step 1](#section_czy_tyb_wdb).

In this way, you have a canonicalized query string \(CanonicalizedQueryString\) that follows the request syntax. For more information, see [Request syntax](/intl.en-US/API Reference/Getting started/Request syntax.md).

## Step 2: Create a string-to-sign

1.  Create a string-to-sign \(`StringToSign`\). You can also use `percentEncode` to encode the canonicalized query string created in the previous step. The following rules apply:

    ```
    StringToSign=
      HTTPMethod + "&" + // HTTPMethod: HTTP method used to make the request, such as GET.
      percentEncode("/") + "&" + // percentEncode("/"): Encode the forward slash (/) in UTF-8 as %2F.
      percentEncode(CanonicalizedQueryString) //Encode the canonicalized query string created in Step 1.
    ```

2.  Calculate the hash-based message authentication code \(HMAC\) value of the `StringToSign`, as defined in [RFC 2104](http://www.ietf.org/rfc/rfc2104.txt). Use the Secure Hash Algorithm 1 \(SHA-1\) algorithm to calculate the HMAC value. The Java Base64 encoding method is used in this example.

    ```
    Signature = Base64( HMAC-SHA1( AccessSecret, UTF-8-Encoding-Of(StringToSign) ) )
    ```

    **Note:** When you calculate the signature, the key value specified by RFC 2104 is your `AccessKeySecret` with an ampersand \(`&`\) which has an ASCII value of 38. For more information, see [Create an AccessKey pair]().

3.  Encode the `Signature` parameter based on [RFC 3986](http://tools.ietf.org/html/rfc3986) and add the parameter to the canonicalized query string.

## Example 1: Concatenate parameters

The [DescribeRegions](/intl.en-US/API Reference/Regions/DescribeRegions.md) operation is called in this example. The following example shows the signature process when `AccessKeyID` is set to testid and `AccessKeySecret` set to testsecret:

1.  Create a canonicalized query string.

    ```
    http://ecs.aliyuncs.com/?Timestamp=2016-02-23T12%3A46%3A24Z&Format=XML&AccessKeyId=testid&Action=DescribeRegions&SignatureMethod=HMAC-SHA1&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf&Version=2014-05-26&SignatureVersion=1.0
    ```

2.  Create a string-to-sign \([`StringToSign`](#StringToSign)\).

    ```
    GET&%2F&AccessKeyId%3Dtestid%26Action%3DDescribeRegions%26Format%3DXML%26SignatureMethod%3DHMAC-SHA1%26SignatureNonce%3D3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf%26SignatureVersion%3D1.0%26Timestamp%3D2016-02-23T12%253A46%253A24Z%26Version%3D2014-05-26
    ```

3.  Calculate the signature. If `AccessKeySecret` is set to testsecret, the key value used for calculation is `testsecret&`. The calculated signature is `OLeaidS1JvxuMvnyHOwuJ+uX5qY=`. The Java Base64 encoding method is used in this example.

    ```
    Signature = Base64( HMAC-SHA1( AccessSecret, UTF-8-Encoding-Of(StringToSign) ) )
    ```

4.  Add the `Signature=OLeaidS1JvxuMvnyHOwuJ%2BuX5qY%3D` string that is encoded based on [RFC 3986](http://tools.ietf.org/html/rfc3986) to the URL in [Step 1](#section_czy_tyb_wdb).

    ```
    http://ecs.aliyuncs.com/?SignatureVersion=1.0&Action=DescribeRegions&Format=XML&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf&Version=2014-05-26&AccessKeyId=testid&Signature=OLeaidS1JvxuMvnyHOwuJ%2BuX5qY%3D&SignatureMethod=HMAC-SHA1&Timestamp=2016-02-23T12%253A46%253A24Z
    ```


You can use browsers or tools such as cURL and Wget to initiate an HTTP request by using the new URL. The HTTP request calls the `DescribeRegions` operation to query the Alibaba Cloud region list.

## Example 2: Use the standard library of the programming language

The [DescribeRegions](/intl.en-US/API Reference/Regions/DescribeRegions.md) operation is called in this example. The following example shows the signature process when `AccessKeyID` is set to testid and `AccessKeySecret` is set to testsecret, and all request parameters are placed in a Java `Map<String, String>` object:

1.  Predefine an encoding method.

    ```
    private static final String ENCODING = "UTF-8";
    private static String percentEncode(String value) throws UnsupportedEncodingException {
      return value ! = null ? URLEncoder.encode(value, ENCODING).replace("+", "%20").replace("*", "%2A").replace("%7E", "~") : null;
    }
    ```

2.  Predefine the time format for the `Timestamp` parameter. The value of the `Timestamp` parameter must be specified in the [ISO 8601](/intl.en-US/API Reference/Appendix/ISO 8601 Time Format.md) standard. The time must be in UTC.

    ```
    private static final String ISO8601_DATE_FORMAT = "yyyy-MM-dd'T'HH:mm:ss'Z'";
    private static String formatIso8601Date(Date date) {
      SimpleDateFormat df = new SimpleDateFormat(ISO8601_DATE_FORMAT);
      df.setTimeZone(new SimpleTimeZone(0, "GMT"));
      return df.format(date);
    }
    ```

3.  Create a query string.

    ```
    final String HTTP_METHOD = "GET";
    Map parameters = new HashMap();
    // Specify request parameters.
    parameters.put("Action", "DescribeRegions");
    parameters.put("Version", "2014-05-26");
    parameters.put("AccessKeyId", "testid");
    parameters.put("Timestamp", formatIso8601Date(new Date()));
    parameters.put("SignatureMethod", "HMAC-SHA1");
    parameters.put("SignatureVersion", "1.0");
    parameters.put("SignatureNonce", UUID.randomUUID().toString());
    parameters.put("Format", "XML");
    // Arrange request parameters.
    String[] sortedKeys = parameters.keySet().toArray(new String[]{});
    Arrays.sort(sortedKeys);
    final String SEPARATOR = "&";
    // Create a string-to-sign.
    StringBuilder stringToSign = new StringBuilder();
    stringToSign.append(HTTP_METHOD).append(SEPARATOR);
    stringToSign.append(percentEncode("/")).append(SEPARATOR);
    StringBuilder canonicalizedQueryString = new StringBuilder();
    for(String key : sortedKeys) {
    // Encode the key and the value.
      canonicalizedQueryString.append("&")
      .append(percentEncode(key)).append("=")
      .append(percentEncode(parameters.get(key)));
    }
    // Encode the canonicalized query string.
    stringToSign.append(percentEncode(
      canonicalizedQueryString.toString().substring(1)));
    ```

4.  Calculate the signature. If `AccessKeySecret` is set to testsecret, the key used for calculation is `testsecret&`. The calculated signature is `OLeaidS1JvxuMvnyHOwuJ%2BuX5qY%3D`.

    ```
    // The following code demonstrates how to calculate the signature:
    final String ALGORITHM = "HmacSHA1";
    final String ENCODING = "UTF-8";
    key = "testsecret&";
    Mac mac = Mac.getInstance(ALGORITHM);
    mac.init(new SecretKeySpec(key.getBytes(ENCODING), ALGORITHM));
    byte[] signData = mac.doFinal(stringToSign.getBytes(ENCODING));
    String signature = new String(Base64.encodeBase64(signData));
    ```

    Encode the Signature parameter based on [RFC 3986](http://tools.ietf.org/html/rfc3986) and add the parameter to the URL. The following section shows the new URL:

    ```
    http://ecs.aliyuncs.com/?SignatureVersion=1.0&Action=DescribeRegions&Format=XML&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf&Version=2014-05-26&AccessKeyId=testid&Signature=OLeaidS1JvxuMvnyHOwuJ%2BuX5qY%3D&SignatureMethod=HMAC-SHA1&Timestamp=2016-02-23T12%253A46%253A24Z
    ```

5.  Send HTTP requests by using a browser, cURL, or Wget.

    ```
    <DescribeRegionsResponse>
     <Regions>
         <Region>
             <LocalName>China (Qingdao)</LocalName>
             <RegionId>cn-qingdao</RegionId>
         </Region>
         <Region>
             <LocalName>China (Hangzhou)</LocalName>
             <RegionId>cn-hangzhou</RegionId>
         </Region>
     </Regions>
     <RequestId>833C6B2C-E309-45D4-A5C3-03A7A7A48ACF</RequestId>
    </DescribeRegionsResponse>
    ```


The response lists regions and region IDs. If you set `Format` to JSON when you submit a request, the response is returned in the JSON format instead of the XML format. For more information, see [Responses](/intl.en-US/API Reference/Getting started/Responses.md).

