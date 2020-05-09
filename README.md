# niksms-dotnetcore
<p>Niksms API Client Writen In Dotnet.Core</p>

<p>You need to have an active account in <a target='_blank' href='https://niksms.com'>NikSms Website</a></p>

## Installation
<p>You can download and use our SDK from this <a href='https://niksms.com/'>link</a>. </p>
<p>If you dont want to use SDK then you should Install Newtonsoft.Json from nuget.</p>

```
Install-Package Newtonsoft.Json
```
<p>Now use bellow libraries in your code:</p>

```c#

using System.Net;
using Newtonsoft.Json;
using System.IO;

```
## Usage

### Send Single SMS
<p>You can Send Single SMS using bellow Code</p>

```c#
string BaseUrl = "http://api.niksms.com/";

string apiKey = "Your Api Key";
string message = "Yout Text Message To Send";
string senderNumber = ""; // Your private line to send SMS Or Niksms public lines
string mobile = ""; // Reciever phone number

string url = BaseUrl + $"SingleSms?apiKey={apiKey}&senderNumber={senderNumber}&message={message}&mobile={mobile}";

HttpWebRequest request = (HttpWebRequest)WebRequest.Create(url);
request.AutomaticDecompression = DecompressionMethods.GZip | DecompressionMethods.Deflate;

using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
using (Stream stream = response.GetResponseStream())
using (StreamReader reader = new StreamReader(stream))
{
    string result = reader.ReadToEnd();
    string NikId = JsonConvert.DeserializeObject<string>(result);
    if(!NikId.Equals("-1"))
        Console.WriteLine($"Sms has been Sent. NikId is: {NikId}");
    else
        Console.WriteLine($"Error occured.");
}

```

### Send Bulk SMS
<p>You can Send Bulk Sms using bellow Code</p>

```c#

string BaseUrl = "http://api.niksms.com/";
string apiKey = "Your Api Key";
string message= "Yout Text Message To Send";
string senderNumber= ""; // Your private line to send SMS Or Niksms public lines
string mobiles = ""; // Recievers phone number sepereated by , (comma)

string url = BaseUrl + $"SingleSms?apiKey={apiKey}&senderNumber={senderNumber}&message={message}&mobiles={mobiles}";

HttpWebRequest request = (HttpWebRequest)WebRequest.Create(url);
request.AutomaticDecompression = DecompressionMethods.GZip | DecompressionMethods.Deflate;

using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
using (Stream stream = response.GetResponseStream())
using (StreamReader reader = new StreamReader(stream))
{
    string result = reader.ReadToEnd();
    string NikId = JsonConvert.DeserializeObject<string>(result);
    if(!NikId.Equals("-1"))
        Console.WriteLine($"Sms has been Sent. NikId is: {NikId}");
    else
        Console.WriteLine($"Error occured.");
}



```

### Send point to point SMS
<p>If you want to send different SMS messages to diffrerent numbers in one request you can use PTPsend method.</p>

```c#

string BaseUrl = "http://api.niksms.com/";
string apiKey = "Your Api Key";
string senderNumber= ""; // Your private line to send SMS Or Niksms public lines
string mobiles = ""; // Recievers phone number sepereated by , (comma)
string messages = ""; // Messages sepreated by | (vertical bar)
	
string url = BaseUrl + $"PtpSms?apiKey={apiKey}&senderNumber={senderNumber}&messages={messages}&mobiles={mobiles}";


HttpWebRequest request = (HttpWebRequest)WebRequest.Create(url);
request.AutomaticDecompression = DecompressionMethods.GZip | DecompressionMethods.Deflate;

using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
using (Stream stream = response.GetResponseStream())
using (StreamReader reader = new StreamReader(stream))
{
    string result = reader.ReadToEnd();
    string NikId = JsonConvert.DeserializeObject<string>(result);
    if(!NikId.Equals("-1"))
        Console.WriteLine($"Sms has been Sent. NikId is: {NikId}");
    else
        Console.WriteLine($"Error occured.");
}

```


### Get Sender Numbers
<p>If you want to get the list of your private numbers that you use for sending SMS, you can use GetSenderNumbers method.</p>

```c#

string BaseUrl = "http://api.niksms.com/";
string apiKey = "Your Api Key";
	
string url = BaseUrl + $"GetSenderNumbers?apiKey={apiKey}";

HttpWebRequest request = (HttpWebRequest)WebRequest.Create(url);
request.AutomaticDecompression = DecompressionMethods.GZip | DecompressionMethods.Deflate;

using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
using (Stream stream = response.GetResponseStream())
using (StreamReader reader = new StreamReader(stream))
{
    string result = reader.ReadToEnd();
    List<string> senderNumbers = JsonConvert.DeserializeObject<List<string>>(result);
}

```

### Get Credit
<p>You can get you credit balance with bellow code.</p>

```c#

string BaseUrl = "http://api.niksms.com/";
string apiKey = "Your Api Key";
	
string url = BaseUrl + $"GetCredit?apiKey={apiKey}";

HttpWebRequest request = (HttpWebRequest)WebRequest.Create(url);
request.AutomaticDecompression = DecompressionMethods.GZip | DecompressionMethods.Deflate;

using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
using (Stream stream = response.GetResponseStream())
using (StreamReader reader = new StreamReader(stream))
{
    string result = reader.ReadToEnd();
    string credit = int.Parse(JsonConvert.DeserializeObject<string>(result));
}

```

### Get Expire Date
<p>You can get your account expiration date with bellow code.</p>

```c#


string BaseUrl = "http://api.niksms.com/";
string apiKey = "Your Api Key";
	
string url = BaseUrl + $"GetExpireDate?apiKey={apiKey}";

HttpWebRequest request = (HttpWebRequest)WebRequest.Create(url);
request.AutomaticDecompression = DecompressionMethods.GZip | DecompressionMethods.Deflate;

using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
using (Stream stream = response.GetResponseStream())
using (StreamReader reader = new StreamReader(stream))
{
    string result = reader.ReadToEnd();
    DateTime expireTime = DateTime.Parse(JsonConvert.DeserializeObject<string>(result));
}

```

### Get Server time
<p>You can get nik SMS server time using bellow code.</p>

```c#

string BaseUrl = "http://api.niksms.com/";
string apiKey = "Your Api Key";
	
string url = BaseUrl + $"GetServertime?apiKey={apiKey}";

HttpWebRequest request = (HttpWebRequest)WebRequest.Create(url);
request.AutomaticDecompression = DecompressionMethods.GZip | DecompressionMethods.Deflate;

using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
using (Stream stream = response.GetResponseStream())
using (StreamReader reader = new StreamReader(stream))
{
    string result = reader.ReadToEnd();
    DateTime ServerTime = DateTime.Parse(JsonConvert.DeserializeObject<string>(result));
}

```


### Get SMS Delivery
<p>You can get results of sent messages using bellow code.</p>

```c#


string BaseUrl = "http://api.niksms.com/";
string apiKey = "Your Api Key";
	
List<string> nikIdsList = new List<string>();
nikIdsList.Add(""); // Add the Id which is related to Sent Sms

string nikIds = "";
nikIdsList.ForEach(item => nikIds += item + ",");
nikIds = nikIds.Substring(0, nikIds.Length - 1);

string url = BaseUrl + $"GetSmsDelivery?apiKey={apiKey}&nikIds={nikIds}";

HttpWebRequest request = (HttpWebRequest)WebRequest.Create(url);
request.AutomaticDecompression = DecompressionMethods.GZip | DecompressionMethods.Deflate;

using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
using (Stream stream = response.GetResponseStream())
using (StreamReader reader = new StreamReader(stream))
{
    string result = reader.ReadToEnd();
    string[] smsResults = JsonConvert.DeserializeObject<string[]>(result);

    foreach(var item in result) {
        if (result.Equals("3"))
            Console.WriteLine('sent successfully');
        else 
        if(result.Equals("2") || result.Equals("3"))
            Console.WriteLine("waiting to be sent");
        else
            Console.WriteLine('message not sent')
        }
    }

}


```


### Get SMS Delivery With ClientId
<p>You can get results of sent messages with ids which you used before, using bellow code.</p>

```c#

string BaseUrl = "http://api.niksms.com/";
string apiKey = "Your Api Key";
	
List<string> yourIdsList = new List<string>();
yourIdsList.Add(""); // Add your Id which is related to Sent Sms

string yourIds = "";
yourIdsList.ForEach(item => yourIds += item + ",");
yourIds = yourIds.Substring(0, yourIds.Length - 1);
string url = BaseUrl + $"GetSmsDeliveryWithClientId?apiKey={apiKey}&yourIds={yourIds}";

HttpWebRequest request = (HttpWebRequest)WebRequest.Create(url);
request.AutomaticDecompression = DecompressionMethods.GZip | DecompressionMethods.Deflate;

using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
using (Stream stream = response.GetResponseStream())
using (StreamReader reader = new StreamReader(stream))
{
    string result = reader.ReadToEnd();
    List<string> smsResults = JsonConvert.DeserializeObject<List<string>>(result);

    foreach(var item in result) {
        if (result.Equals("3"))
            Console.WriteLine('sent successfully');
        else 
        if(result.Equals("2") || result.Equals("3"))
            Console.WriteLine("waiting to be sent");
        else
            Console.WriteLine('message not sent')
        }
    }
}

```


### Get Received Sms
<p>You can get received SMS to your private line using bellow code.</p>

```c#
    public class ReceivedMessage  // You can use this class to deserialize json result
    {
        public string Id { get; set; }
        public string SenderNumber { get; set; }
        public string ReceiveNumber { get; set; }
        public string Message { get; set; }
        public string ReceiveDate { get; set; }
        public bool IsRelayed { get; set; }
    }
```

```c#

string BaseUrl = "http://api.niksms.com/";
string apiKey = "Your Api Key";
	
string url = BaseUrl + $"GetReceivedSms?apiKey={apiKey}";

HttpWebRequest request = (HttpWebRequest)WebRequest.Create(url);
request.AutomaticDecompression = DecompressionMethods.GZip | DecompressionMethods.Deflate;

using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
using (Stream stream = response.GetResponseStream())
using (StreamReader reader = new StreamReader(stream))
{
    string result = reader.ReadToEnd();
    string result = reader.ReadToEnd();
    if (result.Contains("[]"))
        Console.WriteLine("No Message Received");
    else
    {
        List<ReceivedMessage> listOfMessages = JsonConvert.DeserializeObject<List<ReceivedMessage>>(result);
    }
}

```




<hr/>

<div dir='rtl'>

# راهنمای زبان برنامه نویسی DotNet.Core

### معرفی سرویس پیامکی نیک اس ام اس
<p>شما می توانید با استفاده از سرویس ارسال پیامک <a target='_blank' href='https://niksms.com'>نیک اس ام اس</a> به راحتی پیامک های خود را ارسال نمایید.</p>

### ساخت حساب کاربری
<p>برای استفاده از سرویس پیامکی و API باید یک حساب کاربری در<a target='_blank' href='https://niksms.com/fa/main/register'>بخش ثبت نام نیک اس ام اس</a> ساخته و آن را فعال نمایید.</p>

### مستندات
شما می توانید برای مشاهده کامل مستندات وب سرویس به <a target='_blank' href='https://niksms.com/fa/documentation'>بخش برنامه نویسان</a> سایت مراجعه فرمایید.

### اطلاعات بیشتر
برای کسب اطلاعات بیشتر به وب سایت <a target='_blank' href='https://niksms.com'>نیک اس ام اس</a> مراجعه فرمایید.
</div>
