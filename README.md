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
using System.Text;
using System.Net;
using System.Collections.Specialized;
using Newtonsoft.Json;

```
## Usage

### Send Single SMS
<p>You can Send Single SMS using bellow Code</p>

```c#

string url =  "http://niksms.com/SingleSms";
using (var client = new WebClient())
{
    var values = new NameValueCollection();
    values["apiKey"] = "Your Api Key";
    values["message"] = "Yout Text Message To Send";
    values["senderNumber"] = ""; // Your private line to send SMS Or Niksms public lines
    values["mobile"] = ""; // Reciever phone number
	
    var response = client.UploadValues(url, values);
	
    var responseString = Encoding.Default.GetString(response);
    if(int.Parse(responseString) > 0)
        Console.WriteLine("SMS Successfully Sent");
    else
        Console.WriteLine("Can not send Sms");
}

```


### Send Bulk SMS
<p>You can Send Bulk Sms using bellow Code</p>

```c#

string url =  "http://niksms.com/GroupSms";
using (var client = new WebClient())
{
    var values = new NameValueCollection();
    values["apiKey"] = "Your Api Key";
    values["message"] = "Yout Text Message To Send";
    values["senderNumber"] = ""; // Your private line to send SMS Or Niksms public lines
    values["mobiles"] = ""; // Recievers phone number sepereated by , (comma)
	
    var response = client.UploadValues(url, values);
	
    var responseString = Encoding.Default.GetString(response);
    if(int.Parse(responseString) > 0)
        Console.WriteLine("SMS Successfully Sent");
    else
        Console.WriteLine("Can not send Sms");
}


```

### Send point to point SMS
<p>If you want to send different SMS messages to diffrerent numbers in one request you can use PTPsend method.</p>

```c#

string url =  "http://niksms.com/PtpSms";
using (var client = new WebClient())
{
    var values = new NameValueCollection();
    values["apiKey"] = "Your Api Key";
    values["senderNumber"] = ""; // Your private line to send SMS Or Niksms public lines
    values["mobiles"] = ""; // Recievers phone number sepereated by , (comma)
    values["messages"] = ""; // Messages sepreated by | (vertical bar)
	
    var response = client.UploadValues(url, values);
	
    var responseString = Encoding.Default.GetString(response);
    if(int.Parse(responseString) > 0)
        Console.WriteLine("SMS Successfully Sent");
    else
        Console.WriteLine("Can not send Sms");
}

```


### Get Sender Numbers
<p>If you want to get the list of your private numbers that you use for sending SMS, you can use GetSenderNumbers method.</p>

```c#

string url =  "http://niksms.com/GetSenderNumbers";
using (var client = new WebClient())
{
    var values = new NameValueCollection();
    values["apiKey"] = "Your Api Key";
	
    var response = client.UploadValues(url, values);

    var responseString = Encoding.Default.GetString(response);
    var listOfNumbers = JsonConvert.DeserializeObject<List<string>>(responseString);
}

```

### Get Credit
<p>You can get you credit balance with bellow code.</p>

```c#

string url =  "http://niksms.com/GetCredit";
using (var client = new WebClient())
{
    var values = new NameValueCollection();
    values["apiKey"] = "Your Api Key";
	
    var response = client.UploadValues(url, values);
	
    var yourCredit = Encoding.Default.GetString(response);
}

```

### Get Expire Date
<p>You can get your account expiration date with bellow code.</p>

```c#

string url =  "http://niksms.com/GetExpireDate";
using (var client = new WebClient())
{
    var values = new NameValueCollection();
    values["apiKey"] = "Your Api Key";
	
    var response = client.UploadValues(url, values);
	
    var expireDate = Encoding.Default.GetString(response);
}

```

### Get Server time
<p>You can get nik SMS server time using bellow code.</p>

```c#

string url =  "http://niksms.com/GetServertime";
using (var client = new WebClient())
{
    var values = new NameValueCollection();
    values["apiKey"] = "Your Api Key";
	
    var response = client.UploadValues(url, values);
	
    var serverTime = Encoding.Default.GetString(response);
}

```


### Get SMS Delivery
<p>You can get results of sent messages using bellow code.</p>

```c#

string url =  "http://niksms.com/GetSmsDelivery";
using (var client = new WebClient())
{
    var values = new NameValueCollection();
    
    List<int> nikIds = new List<int>();
    nikIds.Add(); // Add the Id which is related to Sent Sms

    values["apiKey"] = "Your Api Key";
    values["nikIds"] = nikIds; // Array of ids related to each SMS that you sent. This Ids has been sent to you as response of sendSingle or group SMS

    var response = client.UploadValues(url, values);
	
    var resultString = Encoding.Default.GetString(response);
    List<string> result = JsonConvert.DeserializeObject<List<string>>(responseString);
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

string url =  "http://niksms.com/GetSmsDeliveryWithClientId";
using (var client = new WebClient())
{
    var values = new NameValueCollection();
    
    List<int> yourIds = new List<int>();
    yourIds.Add(); // Add the Id which is related to Sent Sms

    values["apiKey"] = "Your Api Key";
    values["yourIds"] = yourIds; // Array of ids related to each SMS that you sent. This Ids are numbers which you used in sending SMS.

    var response = client.UploadValues(url, values);
	
    var resultString = Encoding.Default.GetString(response);
    List<string> result = JsonConvert.DeserializeObject<List<string>>(responseString);
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
    public class ReceivedMessage  // You can use this classs to deserilize result
    {
        public string SenderNumber{ get; set;}
        public string Message{ get; set;}
        public string ReceiveDate{ get; set;}
    }
```

```c#

string url =  "http://niksms.com/GetReceivedSms";
using (var client = new WebClient())
{
    var values = new NameValueCollection();
    values["apiKey"] = "Your Api Key";
	
    var response = client.UploadValues(url, values);
	
    var responseString = Encoding.Default.GetString(response);
    var listOfMessages = JsonConvert.DeserializeObject<List<ReceivedMessage>>(responseString);

    foreach(var item in listOfMessages){
        Console.WriteLine($"Sender number is {item.SenderNumber}");
        Console.WriteLine($"Message is {item.Message}");
        Console.WriteLine($"Receive time is {item.ReceiveDate}");
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



