# Chaboksms Objective-C

<div dir='rtl'>

### معرفی وب سرویس چابک اس ام اس
چابک اس ام اس یک وب سرویس کامل برای ارسال و دریافت پیامک و پیامک صوتی و مدیریت کامل خدمات دیگر است که براحتی میتوانید از آن استفاده کنید.

<hr>

### نصب

<p>قبل از نصب نیاز به ثبت نام در سایت چابک اس ام اس دارید.</p>

[**ثبت نام به همراه دریافت 200 پیامک هدیه جهت تست وبسرویس**](https://chaboksms.ir/)

</div>

<div dir='rtl'>
  
#### نحوه استفاده

نمونه کد برای ارسال پیامک

</div>


```js
NSString *username = @"username";
NSString *password = @"password";
NSString *to = @"9123456789";
NSString *from = @"5000...";
NSString *message = @"تست وب سرویس چابک اس ام اس";
BOOL isFlash = false;
SoapClient *soapClient = [[SoapClient alloc] initCred:username password:password];
[soapClient SendSimpleSMS2:to sender:from msg:message flash:isFalse];
```

<div dir='rtl'>

از آنجا که وب سرویس چابک اس ام اس تنها محدود به ارسال پیامک نیست شما از طریق زیر میتوانید به وب سرویس ها دسترسی کامل داشته باشید:
</div>

```js
// وب سرویس پیامک
RestClient *restClient = [[RestClient alloc] initCred:username password:password];
SoapClient *soapClient = [[SoapClient alloc] initCred:username password:password];
```

<div dir='rtl'>
  
#### تفاوت های وب سرویس پیامک rest و soap

از آنجا که چابک اس ام اس وب سرویس کاملی رو در اختیار توسعه دهندگان میگزارد برای راحتی کار با وب سرویس پیامک علاوه بر وب سرویس اصلی soap وب سرویس rest رو هم در اختیار توسعه دهندگان گزاشته شده تا راحتتر بتوانند با وب سرویس کار کنند. تفاوت اصلی این دو در تعداد متد هاییست که میتوانید با آن کار کنید. برای کار های پایه میتوان از وب سرویس rest استفاده کرد برای دسترسی بیشتر و استفاده پیشرفته تر نیز باید از وب سرویس باید از وب سرویس soap استفاده کرد. جهت مطالعه بیشتر وب سرویس ها به قسمت وب سرویس پنل خود مراجعه کنید.

<hr/>


###  اطلاعات بیشتر

برای مطالعه بیشتر و دریافت راهنمای وب سرویس ها و آشنایی با پارامتر های ورودی و خروجی وب سرویس به صفحه معرفی
[وب سرویس چابک اس ام اس](https://github.com/Chaboksms/Webservices)
مراجعه نمایید .
در تمامی متدها فرض گرفته ایم ARC در محیط کاربری شما فعال است. بنابراین از آزاد سازی حافظه بصورت دستی صرف نظر نمودیم.

<hr/>

</div>


<div dir='rtl'>

### وب سرویس پیامک

متدهای وب سرویس:

</div>

#### ارسال

```js
[restClient Send:to sender:from msg:message flash:isFlash];
[soapClient SendSimpleSMS2:to sender:from msg:message flash:isFlash];
```
<div dir='rtl'>
  در آرگومان سوم روش soap میتوانید از هر تعداد مخاطب به عنوان آرایه استفاده کنید
</div>

#### ارسال از خط خدماتی اشتراکی

```js
[restClient SendByBaseNumber:text to:toNum bodyId:bid];
[soapClient SendByBaseNumber2:text to:toNum bodyId:bid];
```

#### دریافت وضعیت ارسال
```js
[restClient GetDelivery:recId];
[soapClient GetDelivery:recId];
[soapClient GetDeliveries:array];
```

#### لیست پیامک ها

```js
[restClient GetMessages:location from:from index:index count:count];
[soapClient getMessages:location from:from index:index count:count];
// جهت دریافت به صورت رشته ای
[soapClient GetMessagesByDate:location from:from index:index count:count dateFrom:dFrom dateTo:dTo];
//جهت دریافت بر اساس تاریخ
[soapClient GetUsersMessagesByDate:location from:from index:index count:count dateFrom:dFrom dateTo:dTo];
// جهت دریافت پیام های کاربران بر اساس تاریخ 
```

#### موجودی
```js
[restClient GetCredit];
[soapClient GetCredit];
```

#### تعرفه پایه / دریافت قیمت قبل از ارسال
```js
[restClient GetBasePrice];
[soapClient GetSmsPrice:irancellCount mtnCnt:mtnCount from:from msg:text];
```
#### لیست شماره اختصاصی
```js
[soapClient GetUserNumbers];
```

#### بررسی تعداد پیامک های دریافتی
```js
[soapClient GetInboxCount:isRead];
//پیش فرض خوانده نشده 
```

#### ارسال پیامک پیشرفته
```js
[soapClient SendSms:arrayOfTo from:from msg:text flash:isFlash uhd:uhd arrayOfRecId:array arrayOfStatus:stArray];
```

#### مشاهده مشخصات پیام
```js
[soapClient GetMessagesReceptions:msgId fromrows:from];
```


#### حذف پیام دریافتی
```js
[soapClient RemoveMessages2:location arrayOfMsgId:msgIds];
```


#### ارسال زماندار
```js
[soapClient AddSchedule:to from:from msg:text isFlash:isflash sdt:scheduleDateTime prd:period];
```

#### ارسال زماندار متناظر
```js
[soapClient AddMultipleSchedule:arrayOfTo from:from arrayOfMsg:msgs isFlash:isflash arrayOfSt:stArray period:period];
```


#### ارسال سررسید
```js
[soapClient AddUsance:to from:from msg:text isFlash:isflash ss:scheduleStartDateTime rpt:repeat se: scheduleEndDateTime];
```

#### مشاهده وضعیت ارسال زماندار
```js
[soapClient GetScheduleStatus:schId];
```

#### حذف پیامک زماندار
```js
[soapClient RemoveSchedule:schId];
```

<div dir='rtl'>
  
### وب سرویس پیامک صوتی

</div>

####  ارسال پیامک همراه با تماس صوتی
```js
[soapClient SendSMSWithSpeechText:smsBody spch:speechBody from:from to:to];
```

####  ارسال پیامک همراه با تماس صوتی به صورت زمانبندی
```js
[soapClient SendSMSWithSpeechTextBySchduleDate:smsBody spch:speechBody from:from to:to sche:scheduleDate];
```

####  دریافت وضعیت پیامک همراه با تماس صوتی 
```js
[soapClient GetSendSMSWithSpeechTextStatus:recId];
```

#### تماس انبوه زماندار
```js
[soapClient SendBulkSpeechText:title body:body receivers:receivers DateToSend:DateToSend repeatCount:repeatCount];
```


#### تماس انبوه زماندار با انتخاب فایل
```js
[soapClient SendBulkVoiceSMS:title voiceFileId:voiceFileId receivers:receivers DateToSend:DateToSend repeatCount:repeatCount];
```


#### آپلود فایل صوتی
```js
[soapClient UploadVoiceFile:title base64StringFile:base64StringFile];
```

<div dir='rtl'>
  
### وب سرویس ارسال انبوه/منطقه ای

</div>

#### دریافت شناسه شاخه های بانک شماره
```js
[soapClient GetBranchs:owner];
```


#### اضافه کردن یک بانک شماره جدید
```js
[soapClient AddBranch:branchName owner:owner];
```

#### اضافه کردن شماره به بانک
```js
[soapClient AddNumber:branchId arrayOfNum:Numbers];
```

#### حذف یک بانک
```js
[soapClient RemoveBranch:branchId];
```

#### ارسال انبوه از طریق بانک
```js
[soapClient AddBulk:from branch:branch bulkType:bulkType title:title msg:message rangeF:rangeFrom rangeT:rangeTo date:DateToSend reqCnt:requestCount rowFrom:rowFrom];
```

#### تعداد شماره های موجود
```js
[soapClient GetBulkCount:branch rangeF:rangeFrom rangeT:rangeTo];
```

#### گزارش گیری از ارسال انبوه
```js
[soapClient GetBulkReceptions:bulkId fromRows:fromRows];
```


#### تعیین وضعیت ارسال 
```js
[soapClient GetBulkStatus:bulkId sent:sent failed:failed status:status];
```

#### تعداد ارسال های امروز
```js
[soapClient GetTodaySent];
```

#### تعداد ارسال های کل

```js
[soapClient GetTotalSent];
```

#### حذف ارسال منطقه ای
```js
[soapClient RemoveBulk:bulkId];
```

#### ارسال متناظر
```js
[soapClient SendMultipleSMS:arrayOfTo from:from arrayOfMsg:Messages isFlash:isflash uhd:udh arrayOfRecIds:Ids status:status];
```

#### نمایش دهنده وضعیت گزارش گیری

```js
[soapClient UpdateBulkDelivery:bulkId];
```
<div dir='rtl'>
  
### وب سرویس تیکت

</div>

#### ثبت تیکت جدید
```js
[soapClient AddTicket:title content:content alert:aletWithSms];
```

#### جستجو و دریافت تیکت ها

```js
[soapClient GetReceivedTickets:ticketOwner type:ticketType keyword:keyword];
```

#### دریافت تعداد تیکت های کاربران
```js
[soapClient GetReceivedTicketsCount:ticketType];
```

#### دریافت تیکت های ارسال شده
```js
[soapClient GetSentTickets:ticketOwner type:ticketType keyword:keyword];
```

#### دریافت تعداد تیکت های ارسال شده
```js
[soapClient GetSentTicketsCount:ticketType];
```


#### پاسخگویی به تیکت
```js
[soapClient ResponseTicket:ticketId type:type content:content alert:alertWithSms];
```
<div dir='rtl'>
  
### وب سرویس دفترچه تلفن

</div>

#### اضافه کردن گروه جدید
```js
[soapClient AddGroup:groupName desc:Descriptions show:showToChilds];
```

#### اضافه کردن کاربر جدید
```js
[soapClient AddContact:options];

```

#### بررسی موجود بودن شماره در دفترچه تلفن
```js
[soapClient CheckMobileExistInContact:mobileNumber];
```

#### دریافت اطلاعات دفترچه تلفن
```js
[soapClient GetContacts:groupId keyword:keyword count:cnt];
```
#### دریافت گروه ها
```js
[soapClient GetGroups];
```
#### ویرایش مخاطب
```js
[soapClient ChangeContact:options];
```

#### حذف مخاطب
```js
[soapClient RemoveContact:mobilenumber];
```
#### دریافت اطلاعات مناسبت های فرد
```js
[soapClient GetContactEvents:contactId];
```

<div dir='rtl'>

### وب سرویس کاربران

</div>

#### ثبت فیش واریزی
```js
[soapClient AddPayment:options];
```

#### اضافه کردن کاربر جدید در سامانه
```js
[soapClient AddUser:options];

```

#### اضافه کردن کاربر جدید در سامانه(کامل)
```js
[soapClient AddUserComplete:options];
```

#### اضافه کردن کاربر جدید در سامانه(WithLocation)
```js
[soapClient AddUserWithLocation:options];
```
#### بدست آوردن ID کاربر
```js
[soapClient AuthenticateUser];
```
#### تغییر اعتبار
```js
[soapClient ChangeUserCredit:amount desc:description user:targetUsername gTax:GetTax];
```

#### فراموشی رمز عبور
```js
[soapClient ForgotPassword:mobileNumber email:emailAddress user:targetUsername];
```
#### دریافت تعرفه پایه کاربر
```js
[soapClient GetUserBasePrice:targetUsername];
```

#### دریافت اعتبار کاربر
```js
[soapClient GetUserCredit:targetUsername];
```

#### دریافت مشخصات کاربر
```js
[soapClient GetUserDetails:targetUsername];
```

#### دریافت شماره های کاربر
```js
[soapClient GetUserNumbers];
```

#### دریافت تراکنش های کاربر
```js
[soapClient GetUserTransactions:targetUsername creditType:creditType dateF:dateFrom dateT:dateTo keyword:keyword];
```

#### دریافت اطلاعات  کاربران
```js
[soapClient GetUsers];
```


#### دریافت اطلاعات  فیلترینگ
```js
[soapClient HasFilter:text]
```


####  حذف کاربر
```js
[soapClient RemoveUser:targetUsername];
```


#### مشاهده استان ها
```js
[soapClient GetProvinces];
```

#### مشاهده کد شهرستان 
```js
[soapClient GetCities:provinceId];
```


#### مشاهده تاریخ انقضای کاربر 
```js
[soapClient GetExpireDate]
```
